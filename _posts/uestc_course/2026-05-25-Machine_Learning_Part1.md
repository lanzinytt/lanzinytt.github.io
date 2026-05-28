---
layout:     post
title:      "机器学习_Part1.26"
subtitle:   " \"Machine_Learning\""
date:       2026-5-25 14:00:00
author:     "LanZinYtt"
header-img: "img/in-post/"
catalog: true
tags:

---

>本文为对机器学习课程PPT的梳理式文档记录

# 机器学习_Part1

##  机器学习方法概论

### 机器学习定义与历史

机器学习定义：
- 对人类：（百度百科）学习是透过教授或体验而获得知识、技术、态度或价值的过程，从而导致可量度的稳定的行为变化，更准确一点来说是建立新的精神结构或视过去的精神结构。
学习必须倚赖经验才能有长远的成效。
- 对系统：（ H. A. Simon ）如果一个系统能够通过执行某个过程改进它的性能，这就是学习。
- 对计算机系统：（ T. M. Mitchell ）以性能度量进行衡量，如果一个计算机程序在某类任务上的性能，随着经验而提升，那么我们称这个计算机程序从经验中学习。

机器学习可以通过有无标记信息分为：
- 监督学习：分类、回归
- 无监督学习：聚类
- 半监督学习：两者结合
- 另外还有半监督学习、弱监督学习、自监督学习

机器学习的历史：
- 略

### 机器学习基本概念

**机器学习的数据划分方式**：
- **留出法**：
    - 直接将数据集划分为两个互斥的集合
    - 划分要尽可能保持数据分布的一致性
- **交叉验证法**：
    - 将数据分层采样划分成k个大小相似的互斥子集，每次使用k-1个进行训练，1个用于测试，并取k个训练测试结果的均值。
    - 一般因为开销较大效果一般而不会使用这种方法
- **自助法**：
    - 对数据有放回的采集m此得到训练集，剩余作为测试集
    - 根据数学极限可以得知$ \frac{1}{e} $的数据可用作测试集，这在数据集较小时能作为非常有效的划分

**机器学习的估计方法**：
- 性能度量是衡量模型泛化能力的评价标准，反映了任务需求
- 对于二分类问题，常用**混淆矩阵**描述分类结果：

| 实际类别 / 预测类别 | 预测为正例 | 预测为反例 |
| --- | --- | --- |
| 实际为正例 | TP（True Positive，真正例） | FN（False Negative，假反例） |
| 实际为反例 | FP（False Positive，假正例） | TN（True Negative，真反例） |

其中：
- **TP**：实际是正例，模型也预测为正例
- **FN**：实际是正例，但模型预测为反例
- **FP**：实际是反例，但模型预测为正例
- **TN**：实际是反例，模型也预测为反例

由混淆矩阵可以引出若干常见评价指标：
- **P（Precision，查准率）**：预测为正的样本中，真正为正的比例
- $ P = \frac{TP}{TP + FP} $
- **R（Recall，召回率）**：实际为正的样本中，被正确预测为正的比例
- $ R = \frac{TP}{TP + FN} $
![alt text](/img/in-post/Machine_Learning/P-R_curve_and_equilibrium_point_schematic_diagram.jpg)
- **TPR（True Positive Rate，真正例率）**：本质上与召回率相同
- $ TPR = \frac{TP}{TP + FN} = R $
- **FPR（False Positive Rate，假正例率）**：实际为反的样本中，被错误预测为正的比例
- $ FPR = \frac{FP}{FP + TN} $
![alt text](/img/in-post/Machine_Learning/C_curve.jpg)
![alt text](/img/in-post/Machine_Learning/How_To_Draw_C_curve.png)
- **F1 值**：查准率与召回率的调和平均，更适合综合衡量二者
- $ F1 = \frac{2PR}{P + R} = \frac{2TP}{2TP + FP + FN} $

- 若模型需要尽量减少“误报”，则应关注 **Precision / FPR**
- 若模型需要尽量减少“漏报”，则应关注 **Recall / TPR**
- **F1** 常用于类别不均衡时综合评价分类器表现

机器学习统计假设检验：
- 和概率论一样，做某种假设并计算假设是否能在置信度$ /alpha $内成立
- 对于多次流出或者交叉检验法可使用“t检验”
- Friedman检验：一种非参数检验方法，常用于比较多个学习器在多个数据集上的总体性能是否存在显著差异
- Nemenyi后续检验：通常在Friedman检验拒绝原假设后使用，用于进一步两两比较各学习器，判断具体哪些模型之间存在显著差异
**需要关注的名词**：
- **特征选择**：
    - 在早期机器学习发展过程中，常常对不同问题的实际内容进行特征选择，虽然产生的模型并非通用模型，但是在效果上在当时已经算是不错。
    - 新兴的模型结构普遍不依赖于特征选择，但是模型学习特征这点并没有改变，特征选择也为我们改进和训练模型带来启发。
- **决策边界**：
    - 对于部分模型（分类、决策等），会存在一个边界在两边做出不同判断，对于这类模型训练过程就是不断优化这个决策边界
- **分类**：
    - 根据观测数据预测对象的类别
- **回归**：
    - 根据观测数据预测对象的某个连续属性的数值
- **聚类**：
    - 将观测数据分为由相似组成的多个类别
- **生成模型与判别模型**：
    - 生成模型的目标是学习数据分布，理解数据的本质后针对性的生成内容
    - 判别模型的目标是直接学习输入特征和目标之间的映射关系，并做出判别
    - 部分机器学习类型并不能简单的划分到生成和判别中，生成和判别本身只是一种按任务划分的功能型描述
- **人工智能的三大流派**：
    - 符号主义
    - 连接主义
    - 行为主义
- 实例、特征向量和特征空间
    - 实例是一个对象
    - 特征向量是把一个实例的多个特征按特定顺序排列成的向量
    - 特征空间是特征向量所有可能性的集合
- **模式和假设空间**：
    - 模式是样本的规律，或者说你要识别和区分的对象的规律
    - 假设空间是你所创建的模型的所有可能表示（模式的集合也是假设空间）
- **机器学习三要素**：
    - 模型：定义具体计算的流程与方法
    - 策略：定义模型评价的标准的方法，在机器学习通常指损失策略
    - 方法：定义模型优化的方法，尤其常用的是梯度下降法
- 模型学习相关用语：
    - 泛化能力：指模型对于没有训练过的新数据的识别能力
    - 过拟合：学习器过于捕捉驯良样本的特征，忽视样本更一般的性质，导致泛化能力下降
    - 欠拟合：对训练样本的一般性质都尚未学习好，一般来讲泛化性能也会较差
    - 正则化：为模型增加约束以达到各种用途，尤其是防止过拟合（其实就是通过阻碍学习器过于专注于提分而导致的各种过拟合）
## 线性系统和感知机

### 线性模型

**基础线性模型**

- 一般形式：
    - $ f(x) = w_1 x_1 + w_2 x_2 + \cdots + w_d x_d + b $
- 向量形式：
    - $ f(\mathbf{x}) = \mathbf{w}^T \mathbf{x} + b $
    其中 $\mathbf{x} = (x_1, x_2, \dots, x_d)^T$，$\mathbf{w} = (w_1, w_2, \dots, w_d)^T$，$b$ 为偏置项。

线性模型的优点：
- 形式简单，计算开销小，训练效率较高
- 可解释性强，参数含义较直观
- 在一些近似线性问题上效果较好，是许多复杂模型的基础

线性模型的缺点：
- 表达能力有限，难以刻画复杂的非线性关系
- 对特征工程较为依赖
- 当数据分布较复杂时，模型效果可能较差

**最小二乘法**

设样本真实值为 $y_i$，预测值为 $f(x_i)$，则最小二乘法的目标是最小化平方误差和：

- $ \min_{\mathbf{w}, b} \sum_{i=1}^{m} \left( f(x_i) - y_i \right)^2 $

在线性模型下可写为：

- $ \min_{\mathbf{w}, b} \sum_{i=1}^{m} \left( \mathbf{w}^T \mathbf{x}_i + b - y_i \right)^2 $

- 等价于欧式距离的平分，易于理解
- 凸函数，有全局最优解
- 导数形式简单，有封闭解

**回归**
- **正则化的多元线性回归（岭回归）**

在最小二乘法基础上加入 $L_2$ 正则项：

- $ \min_{\mathbf{w}} \; (\mathbf{Xw} - \mathbf{y})^T (\mathbf{Xw} - \mathbf{y}) + \lambda \mathbf{w}^T \mathbf{w} $

对目标函数关于 $\mathbf{w}$ 求导并令其为 $0$：

- $ 2\mathbf{X}^T(\mathbf{Xw} - \mathbf{y}) + 2\lambda \mathbf{w} = 0 $

整理得：

- $ (\mathbf{X}^T\mathbf{X} + \lambda \mathbf{I})\mathbf{w} = \mathbf{X}^T\mathbf{y} $

故闭式解为：

- $ \mathbf{w} = (\mathbf{X}^T\mathbf{X} + \lambda \mathbf{I})^{-1} \mathbf{X}^T\mathbf{y} $

- 对数几率回归 - 极大似然法：

设
$$
P(y=1\mid\mathbf{x}) = \frac{1}{1 + e^{-(\mathbf{w}^T\mathbf{x}+b)}}
$$

则通过极大化训练数据的似然函数来估计参数，即：

- $ L(\mathbf{w},b) = \prod_{i=1}^{m} p_i^{y_i}(1-p_i)^{1-y_i} $

通常转为最大化对数似然：

- $ \ell(\mathbf{w},b) = \sum_{i=1}^{m} \left[y_i \ln p_i + (1-y_i) \ln(1-p_i)\right] $

其中 $p_i = P(y=1\mid\mathbf{x}_i)$。

**梯度下降**

- 基本思想：沿目标函数梯度的反方向迭代更新参数，使损失函数不断减小
更新公式：
- $ \mathbf{w} \leftarrow \mathbf{w} - \eta \nabla J(\mathbf{w}) $

- **批量梯度下降（BGD）**

每次使用全部训练样本计算梯度并更新参数
优点是下降方向稳定，缺点是计算开销较大

- **随机梯度下降（SGD）**

每次仅使用一个样本计算梯度并更新参数
优点是计算速度快，缺点是下降过程震荡较明显

**多分类扩展**

- 可将二分类器推广到多分类任务，常见方法有 **一对一（OvO）** 和 **一对其余（OvR）**
- 也可直接使用 **Softmax 回归**，对多个类别的概率进行统一建模
    - $ L = -\sum_{k=1}^{K} y_k \ln p_k $

**LDA**
- **LDA的思想**：寻找一个投影方向，使类内方差尽可能小、类间方差尽可能大，从而使不同类别在低维空间中尽量分开
- **LDA做降维**：将高维样本投影到更低维空间，同时尽量保留类别可分性，因此既可用于分类也可用于有监督降维
- **LDA推广多分类**：对于 $K$ 类问题，LDA 最多可降到 $K-1$ 维，并通过同时考虑多个类别的类内散度矩阵与类间散度矩阵实现多分类推广

### 感知机

- 感知机(perceptron)是二类分类的线性分类模型（linear classificationmodel）
- 其输入为实例的特征向量，输出为实例的类别，取+1和-1二值。
感知机对应于输入空间（特征空间）中的将实例划分为正负两类的分离超平面，属于判别模型。

**模型结构**

- 线性组合加符号函数构成：
    - $ f(\mathbf{x}) = \operatorname{sign}(\mathbf{w}^T\mathbf{x} + b) $
- 其中 $\mathbf{w}$ 为权重向量，$b$ 为偏置，$\mathbf{w}^T\mathbf{x} + b = 0$ 对应分类超平面

**训练策略**

- 基本思想：寻找能够将训练样本正确划分的超平面
- 只对误分类样本更新参数，若样本 $(\mathbf{x}_i, y_i)$ 被误分类，则
    - $ \mathbf{w} \leftarrow \mathbf{w} + \eta y_i \mathbf{x}_i $
    - $ b \leftarrow b + \eta y_i $
- 其中 $\eta > 0$ 为学习率；若训练集线性可分，感知机算法可在有限步内收敛（**迭代收敛性**）

**学习算法的对偶形式**

- 设每个样本被误分类的更新次数为 $\alpha_i$，则权重向量可表示为
    - $ \mathbf{w} = \sum_{i=1}^{m} \alpha_i y_i \mathbf{x}_i $
- 因此判别函数可写为
    - $ f(\mathbf{x}) = \operatorname{sign}\left(\sum_{i=1}^{m} \alpha_i y_i (\mathbf{x}_i^T\mathbf{x}) + b\right) $
- 对偶形式的特点是参数更新只依赖样本之间的内积，适合结合 Gram 矩阵进行计算

## 支持向量机

一般地，当训练数据集线性可分时，存在无穷多个分离超平面，可将两类数据正确分开。

线性可分支持向量机利用**间隔最大化**求最优分离超平面（解是唯一的）。当训练数据近似线性可分时，通过软间隔最大化可以学习到软间隔支持向量机。

设分类超平面为：

- $ \mathbf{w}^T\mathbf{x} + b = 0 $

其中，$\mathbf{w}$ 为法向量，决定超平面的方向；$b$ 为偏置，决定超平面与原点的距离。

对于任一样本 $(\mathbf{x}_i, y_i)$，其中 $y_i \in \{+1,-1\}$，分类决策函数可写为：

- $ f(\mathbf{x}) = \operatorname{sign}(\mathbf{w}^T\mathbf{x} + b) $

SVM约束优化问题（三要素）
- **优化条件**：决策面方程如何定义，即用超平面
    - $ \mathbf{w}^T\mathbf{x} + b = 0 $
    作为分类边界。
- **目标函数**：分类间隔最大化。几何间隔可写为
    - $ \gamma = \frac{y_i(\mathbf{w}^T\mathbf{x}_i+b)}{\lVert \mathbf{w} \rVert} $
    当采用规范化条件 $y_i(\mathbf{w}^T\mathbf{x}_i+b) \ge 1$ 时，间隔最大化等价于最小化
    - $ \frac{1}{2}\lVert \mathbf{w} \rVert^2 $
- **约束条件**：所有样本被正确分类，即满足
    $ y_i(\mathbf{w}^T\mathbf{x}_i+b) \ge 1, \quad i=1,2,\dots,m $

因此，**线性可分支持向量机（硬间隔）** 的优化问题可写为：

$ \begin{aligned}
\min_{\mathbf{w},b} \quad & \frac{1}{2}\|\mathbf{w}\|^2 \\
    ext{s.t.} \quad & y_i(\mathbf{w}^T\mathbf{x}_i+b) \ge 1, \quad i=1,2,\dots,m
\end{aligned} $

其含义是：在保证训练样本被正确分类的前提下，使分类间隔最大。

**如何用拉格朗日对偶性求解**

- 由于 SVM 是一个带不等式约束的凸二次规划问题，直接求解原始问题有时不够方便，因此常将它转化为对偶问题来求解。
- 对硬间隔 SVM，引入拉格朗日乘子 $\alpha_i \ge 0$，构造拉格朗日函数：
    - $ L(\mathbf{w},b,\boldsymbol{\alpha}) = \frac{1}{2}\lVert \mathbf{w} \rVert^2 - \sum_{i=1}^{m} \alpha_i \left[y_i(\mathbf{w}^T\mathbf{x}_i+b)-1\right] $
- 分别对 $\mathbf{w}$ 和 $b$ 求偏导并令其为 $0$：
    - $ \frac{\partial L}{\partial \mathbf{w}} = \mathbf{w} - \sum_{i=1}^{m} \alpha_i y_i \mathbf{x}_i = 0 $
    - $ \frac{\partial L}{\partial b} = -\sum_{i=1}^{m}\alpha_i y_i = 0 $
- 因而可得：
    - $ \mathbf{w} = \sum_{i=1}^{m}\alpha_i y_i \mathbf{x}_i, \qquad \sum_{i=1}^{m}\alpha_i y_i = 0 $
- 将其代回原式，可得到对偶问题：
    $ \begin{aligned}
    \max_{\boldsymbol{\alpha}} \quad & \sum_{i=1}^{m}\alpha_i - \frac{1}{2}\sum_{i=1}^{m}\sum_{j=1}^{m}\alpha_i\alpha_j y_i y_j\mathbf{x}_i^T\mathbf{x}_j \\
    	ext{s.t.} \quad & \alpha_i \ge 0, \quad i=1,2,\dots,m \\
    & \sum_{i=1}^{m}\alpha_i y_i = 0
    \end{aligned} $

**SMO 算法的使用**

- 上述对偶问题本质上是一个二次规划问题。若直接调用通用二次规划方法，在样本较多时计算代价较高。
- **SMO（Sequential Minimal Optimization，序列最小最优化）** 是 SVM 中最经典的求解算法之一，它的核心思想是：**每次只选择两个拉格朗日乘子 $\alpha_i, \alpha_j$ 进行优化，其余变量保持不变**。
- 之所以每次选两个变量，是因为对偶问题存在约束
    $ \sum_{i=1}^{m}\alpha_i y_i = 0 $
    若只更新一个变量，很难同时满足该等式约束；更新两个变量则可以在满足约束的同时进行局部解析求解。
- SMO 的基本流程可以概括为：
    - 先选取一个违反 KKT 条件的样本对应的 $\alpha_i$；
    - 再选择第二个变量 $\alpha_j$ 与它配对更新；
    - 在约束区间内求出新的 $\alpha_i, \alpha_j$；
    - 再同步更新阈值 $b$；
    - 不断重复，直到所有变量基本满足 KKT 条件。
- 因此，SMO 可以理解为：**把一个大规模二次规划问题分解成许多个只含两个变量的小问题逐个求解**。
- 在实际应用中，SMO 特别适合核支持向量机，因为对偶问题本身只依赖核函数值，便于直接结合核技巧实现训练。

**KKT 条件与支持向量**

- SVM 是凸优化问题，满足条件时原问题与对偶问题最优值相等，因此可通过解对偶问题得到原问题最优解。
- 最优解需满足 KKT 条件：
    - $ \alpha_i \ge 0, \qquad y_i(\mathbf{w}^T\mathbf{x}_i+b)-1 \ge 0 $
    - $ \alpha_i\left[y_i(\mathbf{w}^T\mathbf{x}_i+b)-1\right] = 0 $
- 这说明只有部分样本对应的 $\alpha_i > 0$，这些样本就是**支持向量**；也就是说，最终分类超平面只由少数关键样本决定。

当训练集不是完全线性可分时，引入松弛变量 $\xi_i \ge 0$，允许少量样本不满足硬间隔约束，这就得到**软间隔支持向量机**：

$ \begin{aligned}
\min_{\mathbf{w},b,\boldsymbol{\xi}} \quad & \frac{1}{2}\|\mathbf{w}\|^2 + C\sum_{i=1}^{m}\xi_i \\
    ext{s.t.} \quad & y_i(\mathbf{w}^T\mathbf{x}_i+b) \ge 1-\xi_i, \quad i=1,2,\dots,m \\
& \xi_i \ge 0, \quad i=1,2,\dots,m
\end{aligned} $

其中，$C>0$ 为惩罚参数：
- $C$ 较大时，对分类错误惩罚更强，模型更强调训练集上的正确分类；
- $C$ 较小时，允许一定误分类，模型更注重泛化能力。

软间隔情形下，也可以通过拉格朗日对偶得到类似的二次规划问题，只不过约束会变为：

$$
0 \le \alpha_i \le C, \quad i=1,2,\dots,m
$$

这说明惩罚参数 $C$ 同时限制了每个样本对应乘子的取值范围。

**核支持向量机**

- 当样本在原始空间中线性不可分时，可以将输入从原空间映射到更高维特征空间：
    - $ \phi(\mathbf{x}) $
    再在高维空间中构造线性分类面。
- 此时分类函数写为：
    - $ f(\mathbf{x}) = \operatorname{sign}(\mathbf{w}^T\phi(\mathbf{x}) + b) $
- 由于对偶问题中只涉及样本间内积，因此只要把内积
    - $ \mathbf{x}_i^T\mathbf{x}_j $
    替换成核函数
    - $ K(\mathbf{x}_i,\mathbf{x}_j) = \phi(\mathbf{x}_i)^T\phi(\mathbf{x}_j) $
    就能避免显式计算高维映射，这称为**核技巧**。

于是，核支持向量机的决策函数可写为：

- $ f(\mathbf{x}) = \operatorname{sign}\left(\sum_{i=1}^{m}\alpha_i y_i K(\mathbf{x}_i,\mathbf{x}) + b\right) $

常见核函数有：
- **线性核**
    - $ K(\mathbf{x},\mathbf{z}) = \mathbf{x}^T\mathbf{z} $
- **多项式核**
    - $ K(\mathbf{x},\mathbf{z}) = (\mathbf{x}^T\mathbf{z} + c)^p $
- **高斯核 / RBF 核**
    - $ K(\mathbf{x},\mathbf{z}) = \exp\left(-\frac{\lVert \mathbf{x}-\mathbf{z} \rVert^2}{2\sigma^2}\right) $
- **Sigmoid 核**
    - $ K(\mathbf{x},\mathbf{z}) = \tanh(\beta\mathbf{x}^T\mathbf{z} + \theta) $

核方法的关键意义在于：即使原始空间线性不可分，也能通过核函数隐式地在高维空间完成线性分类。

**多分类 SVM**

- 标准 SVM 本质上是一个**二分类模型**，当类别数超过 $2$ 时，通常需要将多分类问题拆分为多个二分类问题来处理。
- 常见策略有：
    - **一对其余（OvR, One vs Rest）**：对于 $K$ 个类别，训练 $K$ 个二分类器。第 $k$ 个分类器把第 $k$ 类视为正类，其余所有类视为负类。预测时选择输出分数最大的类别。
    - **一对一（OvO, One vs One）**：对于 $K$ 个类别，两两构造二分类器，共需要训练
        - $ \frac{K(K-1)}{2} $
        个分类器。预测时采用投票法，得票最多的类别作为最终结果。
- 二者特点：
    - OvR 训练分类器数量较少，结构较简单；
    - OvO 每个分类器只处理两类样本，单个子问题规模较小，实践中常与核 SVM 配合使用。
- 因此，多分类 SVM 的核心思想不是直接改变 SVM 的基本原理，而是**把多类任务转化为若干个二类 SVM 子问题分别求解**。

**支持向量回归（SVR）**

- 支持向量机不仅可以做分类，也可以推广到回归问题，这就是**支持向量回归（Support Vector Regression, SVR）**。
- 在回归任务中，不再要求样本被分到正负两类，而是希望预测函数
    - $ f(\mathbf{x}) = \mathbf{w}^T\mathbf{x} + b $
    尽可能逼近真实输出 $y$。
- SVR 的基本思想是引入一个容忍范围 $\varepsilon$，若预测值与真实值之差不超过 $\varepsilon$，则认为这部分误差可以接受，不计入损失；只有超出 $\varepsilon$ 的部分才进行惩罚，这对应 **$\varepsilon$-不敏感损失函数**。

其优化问题可写为：

$ \begin{aligned}
\min_{\mathbf{w},b,\xi_i,\xi_i^*} \quad & \frac{1}{2}\|\mathbf{w}\|^2 + C\sum_{i=1}^{m}(\xi_i+\xi_i^*) \\
    ext{s.t.} \quad & y_i - (\mathbf{w}^T\mathbf{x}_i+b) \le \varepsilon + \xi_i \\
& (\mathbf{w}^T\mathbf{x}_i+b) - y_i \le \varepsilon + \xi_i^* \\
& \xi_i,\xi_i^* \ge 0, \quad i=1,2,\dots,m
\end{aligned} $

其中：
- $\varepsilon$ 表示可容忍误差范围；
- $\xi_i,\xi_i^*$ 表示超出容忍区间的松弛量；
- $C$ 用于控制模型复杂度与误差惩罚之间的权衡。

- 与 SVM 类似，SVR 也可以通过拉格朗日对偶方法求解，并且同样能够引入核函数，从而得到非线性回归模型。
- SVR 的最终回归函数可写为：
    - $ f(\mathbf{x}) = \sum_{i=1}^{m}(\alpha_i-\alpha_i^*)K(\mathbf{x}_i,\mathbf{x}) + b $
- 其中只有部分样本对应的乘子不为零，这些样本同样称为**支持向量**。

可以把 SVR 理解为：SVM 在分类中追求“最大间隔”，而在回归中追求“在尽量平滑的前提下，让大多数样本点落入宽度为 $2\varepsilon$ 的回归带中”。

最终得到的分类函数仍可写为：

- $ f(\mathbf{x}) = \operatorname{sign}(\mathbf{w}^T\mathbf{x} + b) $

距离分类超平面最近的那些样本点称为**支持向量**，它们决定了最终的最优分离超平面。
