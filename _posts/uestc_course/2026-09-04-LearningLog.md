---
layout:     post
title:      "学习记录.26.9"
subtitle:   " \"LearningLog\""
date:       2026-09-04 20:00:00
author:     "LanZinYtt"
header-img: "img/in-post/"
catalog: true
tags:

---

>目的是简记，希望效果能好叭

# 26九月学习记录

## 9.4

### 研究生调研
- 还是想回到江浙沪，对于这个阶段主要调研的院校是本校、浙大和南大

- 浙软学长的聊天【】

- 浙江大学硕博导师方向【】

### Rec

- 频域序列推荐的了解（师兄任务）

- 了解了下Rec方面的期刊，这里浅列几个
    - ACM RecSys 推荐系统 B
    - ACM SIGIR 信息检索 A
    - AAAI 人工智能 A
    - IJCAI 人工智能 A
    - WWW 网络与推荐系统 A
    - NeurIPS / ICML / ICLR 机器学习 A

- 对于ACM RecSys 2025，搜寻了下主流热门方向的部分文章，预计详读
    - 生成式推荐
        - GRACE
        - Prompt-to-Slate
        - GenSAR
    - LLM4Rec
        - LLM-RecG
        - USB-Rec
    - 图神经网络
        - NLGCL
        - MDSBR
    - 跨域推荐
        - TA-DTCDR
    - 工业界
        - LONGER
        - PinFM
    - 多模态
        - VL-CLIP
- GRACE
    - 创新点: 
        1. CoT 使用外接PKG作为semantic码本的提升
        2. JSA 编码代替全自注意力，通过压缩与筛选优化效果与效率
    
    - 流程:
        - 物品元数据通过BERT做embedding再用RQ-VAE做semantic ID，并拼接PKG提供的属性路径为行为令牌
        - JSA
            根据行为令牌获取QKV，分批加权融合
            - KV通过MLP分块压缩拼接再做注意力
            - 计算KV的重要性分数，选择top-k做注意力
            - 保留粗粒度令牌区做注意力
            - 保留精细令牌区做注意力
        - transformer+MoE 通过束搜索得到目标长度的令牌
        - 根据semantic IDs查找最符合的物品
    - 训练:
        - loss: 直接的令牌交叉熵

- 补充：semantic ID常通过RQ-VAE将物品embedding逐层分解为特征序列，相比于原特征做码本会更有效
 
- diffusion模型
    - 曾经做超分光场比赛时就遇到有人用diffusion，没想到这个方法这么有趣
    - 对目标序列做高斯模糊，并将模糊作为输入原图作为输出加进训练集中，通过学习这种“score function”（专业名词，即无序扩散的反方向有向场）
    - 后续生成图片只需要采用多轮迭代去噪，可以从任意原型有方向的去生成
## 9.5
- DIT
    - 对于常规diffusion模型，使用的是U-net
    - transformer的强势出现，它能更好的捕捉特征与图像结构

## 9.6

- 一些机器学习可能用到的简写名词（这块让AI补全了下释意，并删除了无意义的冗余解释）
    - **ODE**（Ordinary Differential Equation，常微分方程）：常见于神经ODE和扩散模型采样过程。
    - **SDE**（Stochastic Differential Equation，随机微分方程）
    - **SFT**（Supervised Fine-Tuning，监督微调）：使用带有标签数据，对预训练模型进行有监督训练。
    - **ML**（Machine Learning，机器学习）
    - **DL**（Deep Learning，深度学习）
    - **NLP**（Natural Language Processing，自然语言处理）
    - **CV**（Computer Vision，计算机视觉）
    - **RL**（Reinforcement Learning，强化学习）：智能体通过与环境交互，根据奖励信号学习决策策略。
    - **SL**（Supervised Learning，监督学习）
    - **UL**（Unsupervised Learning，无监督学习）
    - **SSL**（Self-Supervised Learning，自监督学习）：从数据本身构造监督信号进行学习；在部分文献中也可能表示 Semi-Supervised Learning（半监督学习）。
    - **LLM**（Large Language Model，大语言模型）
    - **DNN**（Deep Neural Network，深度神经网络）：具有多个隐藏层的神经网络。
    - **CNN**（Convolutional Neural Network，卷积神经网络）
    - **RNN**（Recurrent Neural Network，循环神经网络）
    - **GNN**（Graph Neural Network，图神经网络）
    - **MLP**（Multi-Layer Perceptron，多层感知机）
    - **AE**（Autoencoder，自编码器）
    - **VAE**（Variational Autoencoder，变分自编码器）
    - **GAN**（Generative Adversarial Network，生成对抗网络）
    - **DM**（Diffusion Model，扩散模型）
    - **DDPM**（Denoising Diffusion Probabilistic Model，去噪扩散概率模型）
    - **SGD**（Stochastic Gradient Descent，随机梯度下降）
    - **Adam**（Adaptive Moment Estimation，自适应矩估计）
    - **LR**（Learning Rate，学习率）
    - **BN**（Batch Normalization，批归一化）：按小批量对中间激活进行归一化，以改善训练稳定性。
    - **LN**（Layer Normalization，层归一化）：在单个样本的特征维度上进行归一化
    - **MHA**（Multi-Head Attention，多头注意力）
    - **FFN**（Feed-Forward Network，前馈网络）
    - **RAG**（Retrieval-Augmented Generation，检索增强生成）：先从外部知识库检索相关内容，再将其提供给生成模型作答。
    - **CoT**（Chain of Thought，思维链）：让模型按中间推理步骤组织答案的方法或提示方式。
    - **PEFT**（Parameter-Efficient Fine-Tuning，参数高效微调）：只训练少量附加参数或部分参数，以降低微调成本。
    - **LoRA**（Low-Rank Adaptation，低秩适配）：用低秩矩阵增量替代直接更新全部权重的参数高效微调方法。
    - **RLHF**（Reinforcement Learning from Human Feedback，基于人类反馈的强化学习）：利用人类偏好训练奖励模型，再优化语言模型。
    - **DPO**（Direct Preference Optimization，直接偏好优化）：直接利用偏好数据优化模型策略、无需单独训练强化学习奖励模型的方法。
    - **BPE**（Byte Pair Encoding，字节对编码）：通过反复合并高频子词单元进行文本分词的方法。
    - **CTR**（Click-Through Rate，点击率）：推荐或广告中点击次数与展示次数之比。
    - **CF**（Collaborative Filtering，协同过滤）：根据用户或物品之间的交互相似性进行推荐。
    - **MF**（Matrix Factorization，矩阵分解）：将用户—物品交互矩阵分解为低维潜在因子矩阵的推荐方法。

- 周末还是太摆了..

## 9.7

- KL散度
    - KL散度又名相对熵，用来衡量两个概率分布之间的“差异”
    - 它表示使用一种分布Q去近似另一种分布P会损失多少信息
    - 这里的散度一遍是信息论里的，和微积分里的向量场源汇不一样
- 交叉熵、熵和KL散度
    - **KL散度**：
        - $D_{KL}(P\parallel Q)=\sum_x P(x)\log\frac{P(x)}{Q(x)}$
    - **交叉熵**：
        - $H(P,Q)=-\sum_x P(x)\log Q(x)$
    - **熵**：
        - $H(P)=-\sum_x P(x)\log P(x)$
    - 三者关系：
        - $H(P,Q)=H(P)+D_{KL}(P\parallel Q)$
- tokenizer
    - BPE:根据概率拼凑字符对
    - WordPiece:使用点互信息（相当于一种拼凑提供的信息值）拼凑字符对
    - Unigram:在一定词表基础上做删减
    - BBPE:字节级BPE，防止[UNK]错误情况
- 码本
    - 可学习的向量查询矩阵
    - 常用于VQ-VAE及其变体，用于将VAE编码出来的属性ID转换为具体的嵌入特征
    - 一般在训练模型时，采用“直通估计器”直接传递梯度，防止梯度截断
    - 学习过程中一般通过离散的加上batch中分类到该码字下的样本的均值
- Prompt-to-Slate
    - 创新点:
        - 纯prompt生成的物品集
        - 使用固定的预训练编码器，这是对于物品增删改时唯一需要改变的结构，不需要重新训练前置模型
        - diffusion内在的随机性可能带来推荐的多样性
    - 流程
        - 将文本提示y通过文本编码器（Transformer）映射为上下文向量c 
        - 向量c通过diffusion获得潜变量x
        - x通过固定的预训练编码器转为w
- GenSAR
    - 