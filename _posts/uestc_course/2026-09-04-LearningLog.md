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

- Prompt-to-Slate
    - 
- diffusion模型
    - 曾经做超分光场比赛时就遇到有人用diffusion，没想到这个方法这么有趣
    - 对目标序列做高斯模糊，并将模糊作为输入原图作为输出加进训练集中，通过学习这种“score function”（专业名词，即无序扩散的反方向有向场）
    - 后续生成图片只需要采用多轮迭代去噪，可以从任意原型有方向的去生成

- tokenizer