---
layout: post
title: "Developer Documentation"
subtitle: ' "DeveloperDoc"'
date: 2026-04-13 16:00:00
author: "LanZinYtt"
header-img: ""
catalog: true
tags:
---

> 遇到一些好文包含不错的见解或者是优质的原理的整理性文章

# 互联网开发学习文档

## Nginx设计原理剖析
- 参考博客-[通俗易懂的Nginx工作原理](https://cloud.tencent.com/developer/article/1427219)

- Nginx的一些应用与指令可以详见[官方文档](https://nginx.org/en/docs/)

- 众所周知，nginx是广为使用的反向代理服务器，它以短小精悍著称，不过它能做的并非只有反向代理，还包括正向代理等，不过这不是本段落重点

### 简化工作流程
- 用户通过域名发出访问Web服务器的请求，该域名被DNS服务器解析为反向代理服务器的IP地址；
- 反向代理服务器接受用户的请求；
- 反向代理服务器在本地缓存中查找请求的内容，找到后直接把内容发送给用户；
- 如果本地缓存里没有用户所请求的信息内容，反向代理服务器会代替用户向源服务器请求同样的信息内容，并把信息内容发给用户，如果信息内容是缓存的还会把它保存到缓存中。

### 优点与缺点

**优点：**
- **事件驱动模型**：采用 IO 多路复用（epoll/kqueue）而非多进程/多线程，单进程可处理成千上万的并发连接，内存占用极低
- **非阻塞 I/O**：请求处理期间不会阻塞其他请求，充分利用 CPU 时间片
- **模块化设计**：功能通过模块扩展，核心精简，可按需编译
- **内存效率高**：缓存池、共享内存等机制减少内存分配和回收开销
- **配置简洁**：高度可配置，不需重启即可动态调整某些参数（通过 reload）

**缺点：**
- **单进程无法充分利用多核**：需通过 `worker_processes` 配置多个工作进程来弥补
- **调试复杂**：事件驱动模型不直观，问题排查难度大
- **编程模式陌生**：扩展模块需要理解异步非阻塞编程
- **缓存策略固定**：LRU 缓存策略简单，不如专业缓存系统灵活

### 模块分析

Nginx 的模块化架构是其高性能的基础。请求处理流程中，每个阶段都可插入对应的模块进行处理。

**核心思想**：既然请求处理是流水线式的，每个环节就设计成一个"钩子"（phase），让模块可以在关键点介入，而不必修改核心代码。


TCP 连接建立 → 读请求数据 → [模块处理] → 后端转发 → [模块处理] → 响应客户端
                    ↑                    ↑                   ↑
                   解析           多个处理阶段              过滤

#### 模块划分

根据功能范围分为三类：

1. **核心模块**（Core Modules）
   - `ngx_core_module`：进程管理、信号处理
   - `ngx_event_module`：事件驱动框架
   - 作用：管理生命周期和 I/O 多路复用

2. **标准模块**（Standard Modules）
   - **HTTP 模块**：`ngx_http_*_module`（处理 HTTP 请求）
     - `ngx_http_proxy_module`：反向代理、转发
     - `ngx_http_gzip_module`：压缩
     - `ngx_http_cache_module`：缓存
   - **Stream 模块**（处理 TCP/UDP）：`ngx_stream_*_module`
   - **Mail 模块**（处理邮件协议）

3. **第三方模块**
   - 由社区开发，按需编译集成

#### 模块处理

模块在请求生命周期中按**阶段**（Phase）处理：

请求进入 → [11 个处理阶段，模块依次执行]
          ↓
    POST_READ        (读取请求行/头后)
          ↓
    SERVER_REWRITE   (server 级重定向)
          ↓
    FIND_CONFIG      (匹配 location 块)
          ↓
    REWRITE          (location 级重定向)
          ↓
    POST_REWRITE     (重定向后检查)
          ↓
    PREACCESS        (访问前准备，如限流)
          ↓
    ACCESS           (权限检查)
          ↓
    POST_ACCESS      (访问检查后处理)
          ↓
    TRY_FILES        (尝试文件)
          ↓
    CONTENT          (生成响应体，核心处理)
          ↓
    LOG              (日志记录)

**关键点**：每个模块在对应阶段执行，返回状态码决定流程走向（继续 → 中止 → 跳过）。

例如，反向代理模块在 `CONTENT` 阶段将请求转发给后端服务器，然后由过滤模块（Filter Module）在响应阶段处理返回的内容（压缩、修改头等）。

## kubenets部署踩坑指北

### 谨慎设置Node健康检查时间

Node的健康检查（包括livenessProbe和readinessProbe）参数设置至关重要。**过短的检查间隔和超时时间极容易导致Node初始化启动成功前被杀掉**。

- **问题根源**：Kubernetes会根据健康检查失败的次数决定是否重启Pod。如果在应用启动过程中（特别是涉及复杂初始化的应用），健康检查超时设置过短，应用还未完全启动就会被判定为不健康，进而被重启，形成启动失败的恶性循环。

- **最佳实践**：
  - `initialDelaySeconds`要预留充足的启动时间，建议至少30-60秒以上（具体取决于应用复杂度）
  - `periodSeconds`不要设置过短，通常10-15秒为宜
  - `timeoutSeconds`要给予足够宽松的响应时间，避免误判
  - `failureThreshold`设置3-5次失败重试，给应用充足的恢复机会

### 部分应用比较吃内存，内存限制要合理

某些应用（如Nacos、Elasticsearch等中间件）对内存敏感，**过低的内存上限会导致应用频繁GC、性能下降甚至OOMKill**。

- **问题根源**：当容器内存使用超过限制时，Kubernetes会直接Kill该Pod，应用被强制终止，无法正常关闭。同时，小的内存空间会导致频繁的垃圾回收，造成高延潮。

- **最佳实践**：
  - 了解应用的实际内存需求，不要盲目压低
  - 使用`requests`和`limits`分层设置：`requests`是Kubernetes调度的依据，`limits`是硬上限
  - 为Java应用合理配置堆内存：`-Xms`和`-Xmx`要预留JVM本身运行空间
  - 监控生产环境实际内存消耗，持续优化

### 启动流程慢不止要考虑资源分配

应用启动慢通常表表现为多个方面的综合问题，**不能只盯着CPU和内存，还要关注服务启动顺序和Node自身配置**。

- **资源分配层面**：
  - 确保Pod有足够的CPU Request和内存Request以换取调度优先级
  - 在Node节点本身资源充足的情况下执行测试

- **启动顺序层面**：
  - 利用`InitContainer`或依赖关系（如数据库迁移要在应用启动前完成）确保依赖先启动
  - 避免多个应用同时启动竞争资源，导致雪崩效应
  - 关注应用间的启动依赖，合理安排启动顺序

- **Node节点自身配置**：
  - 检查kubelet的资源预留是否过高，挤压可分配资源
  - 确保Node没有过载，运行的Pod数量不要过多
  - 启用CPU Manager和TopologyManager来优化资源分配，减少上下文切换
  - 关注系统进程（如kubelet、docker daemon）是否占用过多资源

- 请时刻关注kube中缓存的**docker镜像**是哪套
  - 如果镜像更新，请一定要设置imagePullPolicy: Always
  - kube不会检测本地和hub上是否相同，只会确认是否存在而否定拉取镜像（吃大瘪）


## 消息队列的事务实现

消息队列实现最终一致性事务，核心是"可靠投递"。

**常用方案**：
1. **本地事务表 + 异步投递**：业务操作与消息记录在同一事务中写入数据库，异步线程拉取并投递到MQ。优点是消息不丢失，缺点是复杂度高。
2. **MQ事务消息**（RocketMQ/Kafka）：[发送半消息](https://developer.aliyun.com/article/783796?utm_content=g_1000267146) → 执行本地事务 → 提交/回滚消息。更简洁但依赖MQ支持。
3. **死信队列 + 重试**：失败消息重试3-5次后进入DLQ，人工处理。

**关键点**：
- 消费端必须实现**幂等性**（消息可能被重复消费）
- 重试使用指数退避策略（如10s, 30s, 60s）
- 消费超时要合理设置，避免消息重复


## Nacos的动态配置使用

Nacos是配置中心，通过 Namespace（环境）→ Group（分组）→ DataId（配置标识）三层结构管理配置。

**集成步骤**：
```yaml
# bootstrap.yml
spring.cloud.nacos.config:
  server-addr: 127.0.0.1:8848
  namespace: dev-namespace-id
  refresh-enabled: true  # 启用动态刷新
```

**应用层用法**：
```java
@RefreshScope  // 标记为可刷新
@Component
public class MyConfig {
    @Value("${feature.enabled:false}")
    private Boolean featureEnabled;
    
    @NacosConfigListener(dataId = "my-app", groupId = "DEFAULT_GROUP")
    public void onConfigChange(String newConfig) {
        // 配置变更时回调
    }
}
```

**常见场景**：功能开关、限流阈值、连接池参数、业务规则等，实时生效无需重启。

踩坑内容：
      nacos默认会向微服务查询/actuator/health，请保证不被任何拦截器或者配置导致无法正确返回健康心跳，不然nacos会断开连接导致服务log中看起来是连接上但是总控的注册却没有看见的情况。

**注意**：
- 重要配置变更应审批，避免误操作
- 配置值需校验，异常时使用默认值
- 离线应用要配置本地缓存文件作为降级方案

## Nacos + Seata Docker 部署踩坑实录

> 以下内容基于 Nacos v2.2.3 / Seata 2.x 的 Docker 部署实践，结合源码级分析整理而成。
> 三个问题的共同本质：**都是官方文档没有覆盖到的隐式约定**——问题①是 MySQL 生态常识但 Nacos 没说，问题②是 Shell/Properties 特殊字符转义问题，问题③是概念误解但官方示例其实正确，问题④是完全靠翻源码才能知道的内部实现细节。

对于部署问题，首先参考两者的 docker 部署参考文档，因为他们自家配置很多隐性问题只有他们知道。
- [Nacos Docker 部署文档](https://nacos.io/docs/latest/quickstart/quick-start-docker/)
- [Seata Docker 部署文档](https://seata.apache.org/zh-cn/docs/ops/deploy-by-docker-compose)

---

### ① MySQL 认证插件 caching_sha2_password（Nacos 侧）

**现象**：Nacos 启动时报 `Unable to load authentication plugin 'caching_sha2_password'`。

**根因**：MySQL 8.0 将默认认证插件从 `mysql_native_password` 改为 `caching_sha2_password`。Nacos Docker 镜像内置的 MySQL Connector/J 版本决定能否兼容。

- **v2.2.3（当前版本）**：Nacos 官方镜像内置的 JDBC 驱动较老，若 MySQL 服务端的用户认证插件是 `caching_sha2_password`，驱动无法识别，必现报错。
- **latest（如 Nacos 2.4.x+）**：Nacos 跟随内置 JDBC 驱动升级，较新的 MySQL Connector/J（8.0.x+）原生支持 `caching_sha2_password`。但问题并未彻底消失——只要 MySQL 8.0 服务端默认使用 `caching_sha2_password`，而 Nacos 镜像（尤其是自定义构建的旧版镜像）或某些默认配置仍使用旧驱动版本，就会复现。

**本质判断**：这不是 Nacos 的 Bug，而是 MySQL 8.0 与 JDBC 驱动的版本兼容性问题。任何用 MySQL 8.0 作为后端数据库的 Java 应用都可能遇到。

**解决方案**：

创建 MySQL 用户时明确指定 `mysql_native_password` 插件：

```sql
CREATE USER 'nacos'@'%' IDENTIFIED WITH mysql_native_password BY 'nacos';
ALTER USER 'nacos'@'%' IDENTIFIED WITH mysql_native_password BY 'nacos';
```

或者升级 JDBC 驱动版本。

> **文档缺失**：Nacos 官方部署文档只说需要 "MySQL 5.6.5+"，只字未提认证插件问题——这是隐坑。

---

### ② init.d/application.properties 数据库连接硬编码

**现象**：通过环境变量配置的数据库连接参数在 Nacos 容器启动后被错误解析，导致连接字符串损坏（如 `&` 特殊字符被截断）。

**根因**：官方 `init.d/application.properties` 与 Nacos 默认 `application.properties` 的配置机制不同。

**官方写法 — 硬编码，不依赖环境变量**：
```properties
db.url.0=jdbc:mysql://mysql:3306/nacos_devtest?characterEncoding=utf8&connectTimeout=1000...
db.user.0=nacos
db.password.0=nacos
```

**Nacos 默认写法 — 依赖环境变量模板**：
```properties
db.url.0=jdbc:mysql://${MYSQL_SERVICE_HOST}:${MYSQL_SERVICE_PORT:3306}/${MYSQL_SERVICE_DB_NAME}?${MYSQL_SERVICE_DB_PARAM:characterEncoding=utf8&connectTimeout=1000...}
```

**问题链**：
1. `MYSQL_SERVICE_DB_PARAM` 变量中的 `&` 特殊字符被 Shell 解释，导致连接字符串损坏
2. 默认值中的 `&` 在 `application.properties` 里也可能被 Spring 解析为 Properties 的特殊字符，导致连接 URL 被截断
3. 如果使用 `init.d/application.properties` 覆盖默认配置，其中的数据库连接是硬编码的，无法通过环境变量灵活配置

**解决方案**：
- 使用 Docker Compose 时，确保环境变量中的 `&` 被正确转义（用双引号包裹）
- 或者直接在 `init.d/application.properties` 中硬编码正确的数据库连接信息
- 避免在环境变量中使用包含 `&` 的默认值，显式指定每个参数

---

### ③ store.db.datasource 值必须为 druid（Seata 侧）

**现象**：Seata 配置文件（如 `config.txt`）中设置 `store.db.datasource=mysql` 或其它非连接池类型值时，Seata 启动报错 `No DataSourceProvider implementation found`。

**根因**：通过阅读 Seata 2.x 分支（即最新开发分支）的源码，这是**架构层面的硬编码**：

Seata 的 `store.db.datasource` 是通过 **SPI 机制**（`EnhancedServiceLoader.load(DataSourceProvider.class, name)`）加载的，只识别以下三个值：

| 数据源提供者 | `@LoadLevel(name = ...)` | 引入方式 |
|---|---|---|
| `DruidDataSourceProvider` | `"druid"` | 内置，**默认** |
| `HikariDataSourceProvider` | `"hikari"` | 内置 |
| `DbcpDataSourceProvider` | `"dbcp"` | 内置 |

**关键源码逻辑**（`AbstractDataSourceProvider.java`）：
- `datasource=druid` → Druid 连接池
- `datasource=mysql` → 报错 `No DataSourceProvider implementation found`
- 不存在 `name = "mysql"` 的 `DataSourceProvider` 实现，将来也不会加（因为 `"mysql"` 是数据库类型，不是连接池类型）

**结论**：
- `datasource=mysql` 这个写法**在任何 Seata 版本（从 1.x 到最新的 2.x）都不对**
- 这不是版本问题，是**概念理解问题**——`datasource` 指的是**连接池类型**而非数据库类型
- `config.txt`（官方配置模板）中明确写着 `store.db.datasource=druid`，这是唯一正确的值

> **解决方案**：配置文件始终保持 `store.db.datasource=druid`（或 `hikari`/`dbcp`），切勿填数据库类型名。

---

### ④ JDBC 驱动必须挂载到 /lib/jdbc/（Seata 侧）

**现象**：Seata Docker 容器使用 MySQL 数据库存储模式启动时，报找不到 JDBC 驱动类。

**根因**：通过源码分析 `AbstractDataSourceProvider.java` 的 `createMysqlDriverClassLoaders()` 方法，明确的逻辑链如下：

MySQL 驱动加载策略（Seata 源码硬编码）：
1. 从 loader.path（默认 /seata-server/libs）下加载
2. 然后从 loader.path/jdbc/ 子目录下额外加载
3. 两个路径的 URLClassLoader 合并后用于加载 MySQL JDBC 驱动


验证方法中也明确：MySQL 驱动 JAR 必须放置在 `/libs/jdbc/` 子目录下才会被扫描到。

**关键结论**：
- 这是 **Seata 设计上的硬编码约定**，任何版本（包括 `latest`）都一样
- **只对 MySQL 驱动有这个要求**——Oracle、PostgreSQL 等其他数据库不需要 `jdbc` 子目录
- Docker 部署下，`loader.path` 对应 `/seata-server/libs`，所以 JDBC 驱动必须挂载到 **`/seata-server/libs/jdbc/`**（或 `/lib/jdbc/` 取决于容器内 `loader.path` 的环境变量设置）

**Docker Compose 挂载示例**：
```yaml
volumes:
  - ./seata-config:/seata-server/resources  # 配置文件
  - ./mysql-connector-java-8.0.x.jar:/seata-server/libs/jdbc/mysql-connector-java.jar  # JDBC 驱动
```

> **文档缺失**：Seata 官方 Docker 部署文档对此没有明确说明，要靠读源码或踩坑才能发现，属于严重文档缺失。

---

### 问题矩阵总结

| 问题 | v2.2.0（你的版本） | latest | 官方文档是否覆盖 |
|---|---|---|---|
| ① `caching_sha2_password` | ✅ 必现（驱动旧） | ⚠️ 可能不现（驱动新），但 MySQL 8 默认行为不变 | ❌ 未提及 |
| ② `init.d/application.properties` 硬编码 | ✅ 必现 | ✅ 必现 | ❌ 未提及 |
| ③ `datasource=mysql` 报错 | ✅ 必现 | ✅ 必现（永远如此） | ✅ `config.txt` 明确写 `druid` |
| ④ JDBC 驱动 `/lib/jdbc/` | ✅ 必现 | ✅ 必现（硬编码在源码中） | ❌ 未提及 |


## Spring Boot `config.import` 导致 Nacos 地址为 null

### 问题现象

Spring Boot 应用启动报错：`Application failed to connect to Nacos server: "null"`，但 Nacos 地址明明已配置在 `application-local.yml` 中。

### 根本原因

Spring Boot 配置文件的加载顺序如下：

application.yml → 处理 config.import → application-{profile}.yml

当 `application.yml` 中存在：

```yaml
spring:
  config:
    import: "optional:nacos:xxx.yml"
```

Spring 会在加载 `application-{profile}.yml` **之前**就尝试连接 Nacos 拉取远程配置，而此时 Nacos 的 `server-addr` 尚未从 Profile 文件中读取，值为 `null`，连接自然失败。

### 解决方案

将 Nacos 地址提到 `application.yml` 中，推荐配合环境变量兜底，兼容多套环境：

```yaml
spring:
  config:
    import: "optional:nacos:xxx.yml"
  cloud:
    nacos:
      config:
        server-addr: ${NACOS_ADDR:127.0.0.1:8848}  # 本地默认，生产通过环境变量注入
```

### 关键结论

> 只要用了 `config.import` 从 Nacos 拉取配置，Nacos 的连接地址就**必须在 `application.yml` 中能直接读取**，不能依赖任何 Profile 专属配置文件。