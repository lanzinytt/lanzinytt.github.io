---
layout: post
title: "Cloudflare_R2"
subtitle: ' "Cloudflare_R2"'
date: 2026-04-30 11:00:00
author: "LanZinYtt"
header-img: ""
catalog: true
tags:
---

# Cloudflare_R2使用
## 基本api使用


## PreSigned URL
预签名 URL 是 S3 的一个概念，用于授予对对象的临时访问，同时不暴露你的 API 凭证。预签名的 URL 在 URL 本身包含签名参数，授权任何拥有该 URL 的人对特定对象执行特定操作（如 GetObject 或 PutObject），直到 URL 过期,[官方文档如是说](https://developers.cloudflare.com/r2/api/s3/presigned-urls/)。

### 适用场景
- 给前端/移动端直接上传文件到 R2。
- 生成有时效的下载链接。
- 临时开放单个对象的读、写、删权限，而不暴露 `Access Key`。

### 和 Temporary Credentials 的区别
- **PreSigned URL**：只针对**单个对象的一次类操作授权**，适合浏览器直传、下载分享。
- **Temporary Credentials**：适合一段时间内执行**多个 S3 操作**，通常配合标准 S3 Client / SDK 使用。

如果只是让用户上传/下载某一个文件，优先用 PreSigned URL。

### 核心特点
- 签名在本地生成，**不需要先请求 R2**。
- 依赖 [**AWS Signature Version 4**](https://docs.aws.amazon.com/zh_cn/IAM/latest/UserGuide/reference_sigv.html) 签名算法。
- 需要 R2 的 S3 API 凭证：`Access Key ID` 和 `Secret Access Key`。
- 有效期范围：**1 秒到 7 天**，即 `1 ~ 604800` 秒。

### 生成时需要确定的 3 个要素
1. **资源**：`Account ID`、`Bucket`、对象路径 `Key`
2. **操作**：如 `GET`、`PUT`、`HEAD`、`DELETE`
3. **过期时间**：链接可使用多久

### 前置条件
- Cloudflare `Account ID`
- R2 S3 API Token（即 `Access Key ID` / `Secret Access Key`）
- 一个支持 S3 签名的 SDK 或兼容客户端

### 支持的操作
R2 当前支持以下预签名方法：
- `GET`：下载对象
- `HEAD`：获取对象元数据
- `PUT`：上传对象
- `DELETE`：删除对象

不支持：
- `POST` 表单上传（即浏览器 HTML Form 的 multipart upload）

### JavaScript / TypeScript 示例
常见做法是在你的服务端生成 URL，再发给前端使用：

```js
import { S3Client, GetObjectCommand, PutObjectCommand } from "@aws-sdk/client-s3";
import { getSignedUrl } from "@aws-sdk/s3-request-presigner";

const s3 = new S3Client({
	region: "auto",
	endpoint: "https://<ACCOUNT_ID>.r2.cloudflarestorage.com",
	credentials: {
		accessKeyId: "<ACCESS_KEY_ID>",
		secretAccessKey: "<SECRET_ACCESS_KEY>",
	},
});

// 下载链接
const getUrl = await getSignedUrl(
	s3,
	new GetObjectCommand({
		Bucket: "my-bucket",
		Key: "image.png",
	}),
	{ expiresIn: 3600 }
);

// 上传链接
const putUrl = await getSignedUrl(
	s3,
	new PutObjectCommand({
		Bucket: "my-bucket",
		Key: "image.png",
		ContentType: "image/png",
	}),
	{ expiresIn: 3600 }
);
```

### Java 后端示例
下面是一版适合 Spring Boot 的精简示例。

#### 1. 配置类

```java
@Configuration
public class R2Config {

	@Bean
	public S3Presigner s3Presigner(R2Properties properties) {
		String endpoint = "https://" + properties.getAccountId() + properties.getEndpointDomain();

		return S3Presigner.builder()
				.region(Region.of("auto"))
				.endpointOverride(URI.create(endpoint))
				.credentialsProvider(StaticCredentialsProvider.create(
						AwsBasicCredentials.create(
								properties.getAccessKeyId(),
								properties.getSecretAccessKey())))
				.serviceConfiguration(S3Configuration.builder()
						.pathStyleAccessEnabled(false)
						.build())
				.build();
	}
}
```

#### 2. 上传服务

```java
@Service
@RequiredArgsConstructor
public class R2UploadService {

	private final R2Properties r2Properties;
	private final S3Presigner s3Presigner;

	public PresignedUrlVO generateUploadUrl(String originalFilename, String contentType) {
		String key = "books/" + System.currentTimeMillis() + "-" + UUID.randomUUID() + "." + getExtension(originalFilename);

		PutObjectRequest putObjectRequest = PutObjectRequest.builder()
				.bucket(r2Properties.getBucketName())
				.key(key)
				.contentType(contentType)
				.build();

		PutObjectPresignRequest presignRequest = PutObjectPresignRequest.builder()
				.signatureDuration(Duration.ofSeconds(r2Properties.getPresignedUrlExpiration()))
				.putObjectRequest(putObjectRequest)
				.build();

		String uploadUrl = s3Presigner.presignPutObject(presignRequest).url().toString();

		return PresignedUrlVO.builder()
				.uploadUrl(uploadUrl)
				.expiresIn(r2Properties.getPresignedUrlExpiration())
				.build();
	}

	private String getExtension(String filename) {
		if (filename == null || !filename.contains(".")) {
			return "bin";
		}
		return filename.substring(filename.lastIndexOf('.') + 1).toLowerCase();
	}
}
```

#### 3. 返回对象

```java
@Data
@Builder
public class PresignedUrlVO {

	private String uploadUrl;

	@JsonProperty("expires_in")
	private Integer expiresIn;
}
```

#### 4. 配置示例

```yaml
r2:
  account-id: your-account-id
  access-key-id: your-access-key-id
  secret-access-key: your-secret-access-key
  bucket-name: your-bucket-name
  endpoint-domain: .r2.cloudflarestorage.com
  presigned-url-expiration: 600
```

核心思路很简单：把 `S3Presigner` 交给 Spring 管理，业务层只负责生成对象路径和预签名 URL，代码会比每次手动创建客户端更清晰。

### 如何使用
生成后，它本质上就是普通 HTTP URL，不需要再额外带认证头。

```bash
# 下载
curl "https://my-bucket.<ACCOUNT_ID>.r2.cloudflarestorage.com/image.png?X-Amz-Algorithm=..."

# 上传
curl -X PUT "https://my-bucket.<ACCOUNT_ID>.r2.cloudflarestorage.com/image.png?X-Amz-Algorithm=..." \
	--data-binary @image.png
```

同一个预签名 URL 在**过期前可重复使用**。

### URL 中常见参数
一个典型的预签名 URL 会包含这些参数：
- `X-Amz-Algorithm`：签名算法
- `X-Amz-Credential`：参与签名的凭证信息
- `X-Amz-Date`：签名生成时间
- `X-Amz-Expires`：有效期（秒）
- `X-Amz-Signature`：签名值
- `X-Amz-SignedHeaders`：参与签名的请求头

这些参数一旦生成，**不能随意修改**。如果改了对象路径、方法、时间或相关参数，通常会返回：

```text
403 SignatureDoesNotMatch
```

### 最佳实践
#### 1. 服务端生成，不要前端直出密钥
预签名 URL 应在你自己的后端或 Worker 中生成，前端只拿最终 URL。

#### 2. 有效期尽量短
- 上传：几分钟到几十分钟通常足够
- 下载：按业务需求设置，不要默认给太长

#### 3. 对上传限制 `Content-Type`
如果签名时指定了 `ContentType`，客户端上传时必须一致，否则可能报：

```text
403 SignatureDoesNotMatch
```

这样可以减少滥用，例如本来只允许上传图片，却被拿去传别的文件。

#### 4. 浏览器场景要配 CORS
如果预签名 URL 要在浏览器中直接调用，需要给对应 R2 Bucket 配置 CORS，否则可能被浏览器拦截。

#### 5. 把它当作 Bearer Token
谁拿到 URL，谁就在过期前拥有该操作权限。因此：
- 不要公开暴露在日志、页面源码、分享链接中
- 敏感操作使用更短过期时间
- 尽量一对象一链接

### 限制与注意事项
#### 1. 只能用于 S3 API 域名
预签名 URL 只适用于：

```text
https://<ACCOUNT_ID>.r2.cloudflarestorage.com
```

或 Bucket 子域形式，不支持自定义域名直接套用预签名签名结果。

#### 2. 自定义域名不是这个方案
如果你是通过自定义域名公开访问 Bucket，预签名 URL 不是直接对应的认证方式。Cloudflare 文档更推荐结合其他鉴权方案处理，例如 WAF 的 HMAC 校验能力。

#### 3. 它只授权单个对象和单次类型操作
例如一个 `PUT` 预签名 URL 只对应某个具体对象路径，不是整个 Bucket 的通行证。

### 一般工作流
1. 客户端向你的服务端请求上传/下载授权
2. 服务端校验用户身份与对象路径是否合法
3. 服务端生成 PreSigned URL
4. 客户端直接与 R2 通信
5. URL 过期后自动失效

### 什么时候用它
- **用 PreSigned URL**：单文件上传、单文件下载、临时分享链接
- **用 Public Bucket**：完全公开读，不需要鉴权
- **用 Worker/R2 Binding**：服务端代理访问、复杂权限控制
- **用 Temporary Credentials**：需要多次、多对象、会话级 S3 操作

### 小结
PreSigned URL 是 R2 中最实用的临时授权方式之一：
- 简单
- 安全性比直接暴露密钥高很多
- 非常适合前端直传和限时下载

但要注意它本质上是“**带时效的令牌链接**”，所以生成端必须放在可信服务端，并配合短时效、CORS 和类型限制一起使用。