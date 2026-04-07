---
layout: post
title: "推荐系统算法入门"
subtitle: ' "recommendation_system"'
date: 2026-01-19 16:00:00
author: "LanZinYtt"
header-img: ""
catalog: true
tags:
---


# 推荐系统算法入门


## 推荐系统基础

- 推荐系统算法的目的是从大量的数据中选出合适的数据推荐给用户

### 推荐系统的链路

- 推荐系统的链路包含：**召回、粗牌、精排、重排**

- **召回**

    - 推荐系统的链路的第一环是召回，他构建多条召回通道从大量的数据中召回合适的数据，大大降低数据量，避免后续排序的时间复杂度爆炸。召回后需要进一步去重和过滤，去掉重复和用户不喜欢的内容。

    - 常见的召回通道有：协同过滤、双塔模型、关注的作者等等。

- **排序**

    - 先进行粗排再进行精排，这样能有效的权衡准确率和时间复杂度之间的关系。

    - 重排从排序的集合中抽选并打散，让相同的内容不集中出现，防止内容的同质化，并插入运营和广告内容。

    - **粗排、精排**

        - 通过对全部物品特征加上用户特征和统计特征，输入到某种算法（通常是神经网络），并得到预估值（可能是一个排序分数或者预估的用户操作率），从而进行排序。
        
    - **重排**

        - 根据排序分数和多样性分数做多样性抽样，再用规则打散相似笔迹。
### A/B测试

- 所有对模型的改进都得使用A/B测速测算对真实指标的影响，一般在离散实验结果正向后进行。

- 同时，做A/B测试还可以帮助决策哪种参数效果最好，对模型层数进行选择。

- **分层实验**
    - 对于常规对照实验，实验组数十分有限，不能满足工程上对模型迭代速度的要求。
    - 分层实验通过在每个独立的层（召回、排序、用户界面、广告....）构建互不干扰的实验，以满足对模型迭代速度的追求。
    - 分层实验要求**同层互斥**与**不同层正交**。

- **holdout机制**
    - 对于业务指标的实际提升，需要有一个完全不受任何实验影响的分组作为对照，公平地评估各个算法组对业务的真实提升。

- **实验推全&反转实验**
        - 实验推全是指将实验组的算法或策略全面推送到所有用户, 验证其在全量环境下的实际效果。
        - 反转实验则是将原本的实验组和对照组身份互换，进一步确认实验结果的可靠性，排除偶然性和环境干扰；在存在滞后效应时也可用于验证长期影响。
        - 显著性检验（以CTR为例）：设两组样本量$n_1,n_2$，点击数$k_1,k_2$，比例$p_1=k_1/n_1,p_2=k_2/n_2$，合并比例
            $$
            p=\frac{k_1+k_2}{n_1+n_2}.
            $$
            z统计量为：
            $$
            z=\frac{p_1-p_2}{\sqrt{p(1-p)\left(\frac{1}{n_1}+\frac{1}{n_2}\right)}},
            $$
            若$|z|>z_{1-\alpha/2}$则在显著性水平$\alpha$下拒绝原假设。

## 召回

### 基于物品的协同过滤（ItemCF）

- 基本思想：若多个用户对物品$i$和$j$都发生过正向交互，则认为$i$与$j$相似，可以基于相似物品为用户推荐。
- 常用相似度：二元交互下的余弦相似度（或基于共现的相似度）
    $$
    	ext{sim}(i,j)=\frac{\sum_{u\in U} r_{u,i} r_{u,j}}{\sqrt{\sum_{u} r_{u,i}^2}\sqrt{\sum_{u} r_{u,j}^2}}
    $$
    在隐式反馈中，常把$r_{u,i}\in\{0,1\}$，此时可写成共现数归一化的形式：
    $$
    	ext{sim}(i,j)=\frac{|\{u:r_{u,i}>0, r_{u,j}>0\}|}{\sqrt{|\{u:r_{u,i}>0\}|\cdot|\{u:r_{u,j}>0\}|}}.
    $$
- 推荐分数（基于ItemCF的简单预测）：给用户$u$，预测物品$j$的得分为
    $$
    \hat{r}_{u,j}=\sum_{i\in I_u} \text{sim}(i,j) \cdot r_{u,i}
    $$

### Swing模型

- 用于稀疏场景，强调小规模共现的贡献并对大历史长度用户做抑制；一种常见定义为：
    $$
    	ext{Swing}(i,j)=\sum_{u\in U_{i,j}} \frac{1}{|I_u|-1}
    $$
    其中$U_{i,j}$为同时交互过$i$和$j$的用户集合，$I_u$为用户$u$的交互物品集合。

### 基于用户的协同过滤（UserCF）

- 思路：找到与目标用户$u$相似的用户集合$N(u)$，再综合这些用户的喜好为$u$推荐。
- 用户相似度（余弦）:
    $$
    	ext{sim}(u,v)=\frac{\sum_{i} r_{u,i} r_{v,i}}{\sqrt{\sum_i r_{u,i}^2}\sqrt{\sum_i r_{v,i}^2}}
    $$
- 预测分数：
    $$
    \hat{r}_{u,j}=\frac{\sum_{v\in N(u)} \text{sim}(u,v)\, r_{v,j}}{\sum_{v\in N(u)} |\text{sim}(u,v)|}.
    $$

### 离散特征处理

- 离散特征(如category、user_id)常用方法：One-hot、Hashing、Embedding。
- Embedding将离散索引映射为$d$维向量$\mathbf{e}\in\mathbb{R}^d$，便于在神经网络中计算内积、concat等操作。

### 矩阵分解与优化（矩阵补全）

- 目标：给定部分观测的评分矩阵$R\in\mathbb{R}^{m\times n}$，寻找低秩近似
    $$
    R\approx P Q^T,\quad P\in\mathbb{R}^{m\times k},\ Q\in\mathbb{R}^{n\times k}.
    $$
- 优化目标（平方损失+正则化）：
    $$
    \min_{P,Q}\sum_{(u,i)\in\Omega}(r_{u,i}-p_u^T q_i)^2+\lambda(\|p_u\|^2+\|q_i\|^2).
    $$
- 常用求解：随机梯度下降（SGD）或交替最小二乘（ALS）。SGD更新示例：
    $$
    e_{u,i}=r_{u,i}-p_u^T q_i;\quad p_u\leftarrow p_u+\eta(e_{u,i} q_i-\lambda p_u),\quad q_i\leftarrow q_i+\eta(e_{u,i} p_u-\lambda q_i).
    $$

### 最近邻查找与近似（ANN）

- 对于向量检索，常用距离/相似度：余弦、欧氏距离、内积。大规模召回常使用ANN算法：LSH、HNSW、Annoy等。

### 双塔模型（Two-Tower）——训练与正负样本

- 结构：用户塔$f_u(\cdot)$和物品塔$g_i(\cdot)$分别编码为向量$\mathbf{u}=f_u(x_u)$和$\mathbf{v}=g_i(x_i)$，匹配分数常用内积或余弦：$s(u,i)=\mathbf{u}^T\mathbf{v}$。
- 对比学习/软最大化损失（InfoNCE）：对一个正样本$i^+$与若干负样本$\{j\}$，损失为
    $$
    \mathcal{L}=-\log\frac{\exp(\mathbf{u}^T\mathbf{v}_{i^+}/\tau)}{\exp(\mathbf{u}^T\mathbf{v}_{i^+}/\tau)+\sum_{j\in N} \exp(\mathbf{u}^T\mathbf{v}_j/\tau)}.
    $$
- 负采样策略直接影响训练效果：随机负采样、动态采样、基于流行度的采样、硬负样本等。

## 排序

### 排序问题形式化

- 给定候选集合$C$，排序器对每个候选$i\in C$输出分数$\hat{y}_i$，最后按$\hat{y}$降序展示。排序可以看成点估计、对比学习或列表学习问题。

### 常见损失与优化

- 二分类交叉熵（点式）：
    $$
    \mathcal{L}_{\text{BCE}}(y,\hat{y})=-y\log\hat{y}-(1-y)\log(1-\hat{y}).
    $$
- Pairwise（排序对）：给正样本$i^+$和负样本$i^-$，定义
    $$
    \mathcal{L}_{\text{pair}}=-\log\sigma(\hat{y}_{i^+}-\hat{y}_{i^-}).
    $$
- Listwise（Softmax over list）：对一组候选用softmax归一化预测概率，最小化交叉熵：
    $$
    p_i=\frac{\exp(\hat{y}_i)}{\sum_j \exp(\hat{y}_j)},\quad \mathcal{L}=-\sum_i y_i \log p_i.
    $$
- LambdaRank：对样本对加权，权重与指标变化(如$\Delta$NDCG)相关，优化最终排序指标。
- LambdaRank：对样本对加权，权重与指标变化(如$\Delta$NDCG)相关，优化最终排序指标。

    具体地，对于在位置$p$和$q$上的两个文档$i,j$，交换它们对DCG的变化量为：
    $$
    \Delta_{i,j}=\left|\frac{2^{rel_i}-1}{\log_2(p+1)}+\frac{2^{rel_j}-1}{\log_2(q+1)}-\frac{2^{rel_i}-1}{\log_2(q+1)}-\frac{2^{rel_j}-1}{\log_2(p+1)}\right|.
    $$
    LambdaRank将该变化量作为pairwise损失的权重：
    $$
    \mathcal{L}=\sum_{(i,j)} \Delta_{i,j}\cdot -\log\sigma(\hat{y}_i-\hat{y}_j).
    $$

### 多目标学习与MMoE

- 多目标总损失：
    $$
    \mathcal{L}=\sum_{t=1}^T \lambda_t \mathcal{L}_t.
    $$
- MMoE（Multi-gate Mixture-of-Experts）结构：$E$个专家输出$e_k(x)$，第$t$任务的门控$g_t(x)$给出专家加权：
    $$
    o_t(x)=\sum_{k=1}^E g_{t,k}(x) e_k(x),\quad g_{t,k}(x)=\frac{\exp(w_{t,k}^T x)}{\sum_{k'}\exp(w_{t,k'}^T x)}.
    $$

### 预估分数融合

- 多模型分数融合常用线性加权：
    $$
    s=\sum_{m} \alpha_m s^{(m)},\quad \sum_m \alpha_m=1.
    $$
- 若需概率校准，可对分数做Platt Scaling或温度缩放：$\hat{p}=\sigma(\beta s+\gamma)$。

### 视频播放与停留建模

- 目标可能是预测播放概率$P(\text{play})$、播放完比例$R$或期望观看时长$T$。
- 若预测观看时长为实值回归，常用平方损失或Poisson回归；若预测离散抵达/离开事件，可用生存分析：
    $$
    S(t)=P(T>t),\quad h(t)=\frac{f(t)}{S(t)}.
    $$

### 排序模型的特征与粗排

- 排序特征包括：用户特征$u$、物品特征$v$、上下文$c$、交互统计$s$等。模型输入可构成向量$x=[u,v,c,s]$。
- 粗排模型常用轻量模型（LR、GBDT、浅层NN），目标是高召回、低延迟，通常对时间复杂度$O(|C|)$有严格要求。

## 特征交叉

### FM（因式分解机）详细推导

- 预测式：
    $$
    \hat{y}=w_0+\sum_{i=1}^n w_i x_i+\sum_{i=1}^n\sum_{j=i+1}^n \langle v_i,v_j\rangle x_i x_j.
    $$
- 二阶交互项可以用$O(nk)$的方式计算（避免$O(n^2)$）：
    $$
    \sum_{i=1}^n\sum_{j=i+1}^n \langle v_i,v_j\rangle x_i x_j=\frac{1}{2}\left(\sum_{f=1}^k\left(\sum_{i=1}^n v_{i,f} x_i\right)^2-\sum_{i=1}^n v_{i,f}^2 x_i^2\right).
    $$

### DCN（Deep & Cross Network）

- 交叉层定义（第$l$层）：
    $$
    x^{(l+1)}=x^{(0)}(x^{(l)})^T w^{(l)}+b^{(l)}+x^{(l)}.
    $$
    这显式构造了高阶交叉特征而参数量较小。

### LHUC、SENet与Bilinear交叉

- LHUC（类似可学习的通道缩放）：对神经元输出$h$乘以可学习的缩放$s=2\cdot\sigma(a)$，得到$h'=s\odot h$。
- SENet通过学习通道重要性权重$w_c$来重标定特征：$\tilde{x}_c=w_c x_c$。
- Bilinear交叉:
    $$
    y=x^T W y\quad(\text{或}\; x^T W x)
    $$

## 行为序列

### 序列建模目标

- 给定历史$H=[i_1,i_2,\dots,i_T]$，任务是预测对候选$c$的响应$\hat{y}=f(H,c)$。

### RNN/GRU（序列基础）

- GRU单元更新：
    $$
    z_t=\sigma(W_z x_t+U_z h_{t-1}),\quad r_t=\sigma(W_r x_t+U_r h_{t-1})
    $$
    $$
    	ilde{h}_t=\tanh(W x_t+U(r_t\odot h_{t-1})),\quad h_t=(1-z_t)\odot h_{t-1}+z_t\odot\tilde{h}_t.
    $$

### 注意力与DIN

- 注意力权重：
    $$
    \alpha_i=\frac{\exp(f_{att}(q,k_i))}{\sum_j\exp(f_{att}(q,k_j))},\quad \mathbf{h}=\sum_i \alpha_i \mathbf{k}_i.
    $$

### Transformer/Self-Attention（长序列）

- 自注意力：
    $$
    	ext{Attention}(Q,K,V)=\text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V.
    $$
- 序列推荐（如SASRec）将位置编码加入并用多头注意力学习时序依赖。

### 长序列采样与SIM类方法

- 面对超长序列，常用分段池化、重要性采样或压缩表示（例如将近期行为全保留、远期行为做统计摘要）。

## 重排

### 物品相似性与多样性

- 相似度可用余弦或核函数$K(i,j)=\phi(i)^T\phi(j)$。

### MMR（最大边际相关）

- 迭代选择策略：
    $$
    d^*=\arg\max_{d\in D\setminus S} [\lambda \text{Rel}(d) - (1-\lambda) \max_{s\in S} \text{Sim}(d,s)].
    $$

### DPP（确定性点过程）复述

- 选择集合$Y$的概率与$K_Y$的行列式成正比，常把核$K$分解为质量与多样性的乘积：$L_{ij}=q_i S_{ij} q_j$，其中$q_i$为质量分数，$S_{ij}$为相似度。
 
 - DPP的边际增益（将元素$i$加入已有集合$S$时的条件概率比率）可写成：
     $$
     \frac{\det(L_{S\cup\{i\}})}{\det(L_S)}=L_{ii}-L_{i,S}L_S^{-1}L_{S,i},
     $$
     其中$L$为$L$-核（与$K$有关联），$L_{i,S}$为第$i$行对应$S$列的向量，公式显示加入项目$i$的边际增益等于该元素相对于已选集合的一阶条件互信息量。

## 物品冷启动

### 内容基召回与相似度

- 文本/标签向量化后，计算余弦相似度用于召回：
    $$
    	ext{sim}(a,b)=\frac{t_a^T t_b}{\|t_a\|\|t_b\|}.
    $$

### 聚类与look-alike

- $k$-means目标：
    $$
    \min_{C}\sum_{k=1}^K\sum_{x_i\in C_k} \|x_i-\mu_k\|^2.
    $$

### 流量控制

- 新策略/新物品的曝光控制通常采用分阶段放量或贝叶斯优化控制曝光比例，以减少对整体线上指标的风险。

## 优化目标与评价指标（补充）

- Precision@K:
    $$
    	ext{Precision@}K=\frac{1}{K}\sum_{i=1}^K \mathbf{1}\{\text{item}_i\in R_u\}.
    $$
- Recall@K:
    $$
    	ext{Recall@}K=\frac{|\{\text{推荐前}K\}\cap R_u|}{|R_u|}.
    $$
- MAP@K:
    $$
    	ext{AP@}K=\frac{1}{\min(|R_u|,K)}\sum_{k=1}^K P(k)\cdot \mathbf{1}\{\text{item}_k\in R_u\}.
    $$
- DCG/NDCG@K:
    $$
    	ext{DCG@}K=\sum_{i=1}^K \frac{2^{rel_i}-1}{\log_2(i+1)},\quad \text{NDCG@}K=\frac{\text{DCG@}K}{\text{IDCG@}K}.
    $$
- AUC:
    $$
    	ext{AUC}=P(\hat{y}_{+}>\hat{y}_{-}).
    $$

## 实践建议（简要）

- 正则化、早停、分层实验设计、离线线下指标对齐与线上验证（holdout）是工程化过程中的关键环节。

---

如需对某一部分（例如完整导出ALS推导、FM的参数更新细节、或给出PyTorch/TF的示例实现）进行代码化示例，我可以继续生成并运行验证示例。 

## 特征交叉

### FM因式分解机

### DCN深度交叉网络

### LHUC（PPNet）

### SENet和Bilinear交叉

## 行为序列

### 用户历史行为序列建模

### DIN模型（注意力机制）

### SIM模型（长序列建模）

## 重拍

### 物品相似性的度量


### MMR多样性算法

### 业务规则约束下在多样性算法

### DPP多样性算法

## 物品冷启动

### 优化目标&评价指标

### 简单的召回通道

### 聚类召回

### look-alike 召回

### 流量控制

### 冷启动的AB测试

