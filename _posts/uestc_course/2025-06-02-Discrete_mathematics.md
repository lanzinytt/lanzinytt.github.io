---
layout:     post
title:      "离散数学梳理.25"
subtitle:   " \"Math learning\""
date:       2025-06-02 15:00:00
author:     "LanZinYtt"
header-img: ""
catalog: true
tags:
    - Computer_Science_Specialized_Courses
---

<p id = "build"></p>

>希望大伙都能考出好成绩叭😘

# 离散数学

<div class="mermaid">
flowchart LR
    A[离散数学] --> B[预备知识]
    A --> C[数理逻辑]
    A --> D[二元关系]
    A --> E[图论]
    
    B --> B1[集合论]
    B --> B2[计数问题]
    
    C --> C1[命题逻辑]
    C --> C2[谓词逻辑]
    
    D --> D1[二元关系]
    D --> D2[特殊关系]
    
    E --> E1[图]
    E --> E2[树]
    E --> E3[特殊图]
</div>

## 预备知识

### 集合论

- **集合**
    - 集合是不能精确定义的基本数学概念。
    - 通常，集合是由指定范围内的满足给定条件的所有对象聚集在一起构成的。
    - 指定范围内的每一个对象称为元素。
- **集合的表示**
    - 集合是由他所包含的元素完全确定的。
    - 枚举法(显示法)
        - $A = \{a,b,c,d\}$;
        - $B = \{1,3,5,7,...,2n+1,...\}$
    - 叙述法(隐式法)
        - 通过刻画集合中元素所具备的某种特性来表示集合，常记为 $\{x|P(x)\}$
        - $S = \{x|x \in \mathbb{Z} ,x^2+1=0 \}$
    - 归纳法
        - 通过归纳定义集合，一般包括：基础(最基本的元素构成)、归纳(构造新元素的方法)、极小性(规定集合的界限)。
    - 递归指定集合法
        - $a_0=1,a_{i+1}=2a_i(i \geq 0),S=\{a_k|k \geq 0\}$
    - 文氏图(Venn diagram)
- 集合与元素的关系
    - 元素与集合之间的 $ \in $ 关系是明确的
    - 在离散数学中仅仅对界限清楚、无二义性的描述进行讨论。
- 集合与集合的关系
    - 集合相等
        - 当两个集合中包含的元素完全相同，称集合相等。
        - (外延性原理)
    - 集合包含
        - 被包含和包含
        - 子集与真子集
- **特殊的集合及概念**
    - 空集
        - 不包含任何元素的集合称为空集，记作 $ \emptyset$
        - 也可符号化为 $\emptyset = \{x|x \not= x \}$
        - 空集是一切集合的子集
        - **空集是绝对唯一的**
    - 全集
        - 在一个相对固定的范围内，包含此范围内所有元素的集合，称为全集或论集，记作 U或 E
    - 基数
        - 集合中的元素个数称为集合的基数，记作 $ |A| $
        - 如果一个集合的基数是有限的，则称该集合为有限集
        - 如果一个集合的基数是无限的，则称该集合为无限集
    - n元(子)集
        - 如果一个集合A含有n个元素，则称集合A为n元集
        - 如果一个n元集合A存在一个子集含有m个$(n \geq m \geq 0)$元素
        - 一般来说n元集共有 $2^n$ 个不同的子集
    - **幂集**
        - 设A为任意集合，把A的所有不同子集构成的集合称为A的幂集，记作 $ P(A) $ 或 $2^A$ 
        - 也可符号化为 $P(A)=\{x|x \subseteq A \}$
    - 集族
        - 把集合作为元素而构成的集合称为集族
        - 幂集是集族
- 集合的运算
    - **并集(Union)**
        - 设A、B为两个集合，由所有属于A或属于B的元素构成的集合称为A与B的并集
        - 记作 $A \cup B = \{x | x \in A \text{ 或 } x \in B\}$
    - **交集(Intersection)**
        - 设A、B为两个集合，由所有既属于A又属于B的元素构成的集合称为A与B的交集
        - 记作 $A \cap B = \{x | x \in A \text{ 且 } x \in B\}$
    - **差集(Difference)**
        - 设A、B为两个集合，由所有属于A但不属于B的元素构成的集合称为A与B的差集
        - 记作 $A - B = \{x | x \in A \text{ 且 } x \notin B\}$
    - **补集(Complement)**
        - 设A为全集U的子集，由所有属于U但不属于A的元素构成的集合称为A的补集
        - 记作 $\overline{A} = \{x | x \in U \text{ 且 } x \notin A\}$
        - 也可记作 $A^c$ 或 $\sim A$
    - **对称差(Symmetric Difference)**
        - 设A、B为两个集合，由所有属于A但不属于B或属于B但不属于A的元素构成的集合称为A与B的对称差
        - 记作 $A \oplus B = (A - B) \cup (B - A) = (A \cup B) - (A \cap B)$
- **可数集合和不可数集合**
    - **可数集合(Countable Set)**
        - 如果一个集合是有限的，或者与自然数集合 $\mathbb{N}$ 等势，则称该集合为可数集合
        - 例子：
            - 自然数集 $\mathbb{N} = \{0,1,2,3,...\}$
            - 整数集 $\mathbb{Z} = \{...,-2,-1,0,1,2,...\}$
            - 有理数集 $\mathbb{Q}$
            - 偶数集 $\{0,2,4,6,...\}$
    - **不可数集合(Uncountable Set)**
        - 如果一个无限集合不是可数的，则称其为不可数集合
        - 不可数集合的基数严格大于自然数集合的基数
        - 例子：
            - 实数集 $\mathbb{R}$
            - 区间 $(0,1)$ 中的所有实数
            - 幂集 $P(\mathbb{N})$（自然数集的幂集）

### 计数问题
- 乘法原理
- 加法原理
- 排列问题
- 组合问题
- **容斥原理**
    - 计算数目时，排斥不应包含在这个计数中的数目，又要包含错误地排斥的数目作为补偿。 
- **鸽笼原理**
    - n+1只鸽子住进n个鸽笼，则**存在**一个鸽笼至少住进2只鸽子
## 数理逻辑
### 命题逻辑
- 命题与命题连接词
    - **命题(Proposition)**
        - 命题是具有确切真值的陈述句
        - 命题只能有两个真值：真(T/1)或假(F/0)
        - 例如：
            - "3 > 2" 是真命题
            - "5 是偶数" 是假命题
            - "今天天气好吗？" 不是命题（疑问句）
    - **原子命题与复合命题**
        - 原子命题：不能再分解的简单命题
        - 复合命题：由原子命题通过连接词构成的命题
    - **命题连接词**
        - **否定(Negation)** $\neg$
            - $\neg p$：p的否定，当p为真时$\neg p$为假，当p为假时$\neg p$为真
        - **合取(Conjunction)** $\land$
            - $p \land q$：p与q，只有当p和q都为真时才为真
        - **析取(Disjunction)** $\lor$
            - $p \lor q$：p或q，只有当p和q都为假时才为假
        - **蕴含(Implication)** $\rightarrow$
            - $p \rightarrow q$：如果p则q，只有当p为真且q为假时才为假
        - **等价(Equivalence)** $\leftrightarrow$
            - $p \leftrightarrow q$：p当且仅当q，当p和q真值相同时为真
        - 优先级如下：
            - 否定>合取>析取>蕴含>等价
            - 同级按照从左到右的次序
    - 真值表(Truth Table)
        - 用表格形式列出命题公式在所有可能真值指派下的真值
- 命题公式
    - 命题演算的**合式公式**称作命题公式
    - 生成规则
        - 命题变元本身是一个公式
        - 如果G是公式，则 $(\neg G)$ 也是公式
        - 如果G，H是公式，则 $(G \land H)$ $(G \lor H)$ $(G \rightarrow H)$ $(G \leftrightarrow H)$ 也是命题公式
        - 仅通过有限步使用上述规则得到的符号串才是命题公式。
    - **命题公式没有真值**，只有在对其命题变元进行真值指派后，才可确定命题公式的真值
- 命题公式的解释与真值表
    - **解释(Interpretation)**
        - 解释是给命题公式中的每个命题变元指定一个真值（T或F）
        - 一个含有n个命题变元的公式共有 $2^n$ 种不同的解释
        - 例如：公式 $p \land q$ 有4种解释：
            - $p=1, q=1$
            - $p=1, q=0$
            - $p=0, q=1$
            - $p=0, q=0$
        - 一组解释常记作 $I$
    - **真值表(Truth Table)**
        - 真值表是列举公式在所有可能解释下的真值的表格
        - 例如：$(p \land q) \lor \neg r$ 的真值表
            
            | p | q | r | $p \land q$ | $\neg r$ | $(p \land q) \lor \neg r$ |
            |:-:|:-:|:-:|:-----------:|:--------:|:-------------------------:|
            | 1 | 1 | 1 |      1      |    0     |            1              |
            | 1 | 1 | 0 |      1      |    1     |            1              |
            | 1 | 0 | 1 |      0      |    0     |            0              |
            | 1 | 0 | 0 |      0      |    1     |            1              |
            | 0 | 1 | 1 |      0      |    0     |            0              |
            | 0 | 1 | 0 |      0      |    1     |            1              |
            | 0 | 0 | 1 |      0      |    0     |            0              |
            | 0 | 0 | 0 |      0      |    1     |            1              |
- 命题公式的分类
    - 永真公式(**重言式**)
    - 永假公式(矛盾式)
    - **可满足**
        - 如果不是永假
- 命题公式的基本等价关系
    - **1. 幂等律**
        - $p \land p \equiv p$
        - $p \lor p \equiv p$
    - **2. 交换律**
        - $p \land q \equiv q \land p$
        - $p \lor q \equiv q \lor p$
    - **3. 结合律**
        - $(p \land q) \land r \equiv p \land (q \land r)$
        - $(p \lor q) \lor r \equiv p \lor (q \lor r)$
    - **4. 同一律**
        - $p \land T \equiv p$
        - $p \lor F \equiv p$
    - **5. 零律**
        - $p \land F \equiv F$
        - $p \lor T \equiv T$
    - **6. 分配律**
        - $p \land (q \lor r) \equiv (p \land q) \lor (p \land r)$
        - $p \lor (q \land r) \equiv (p \lor q) \land (p \lor r)$
    - **7. 吸收律**
        - $p \land (p \lor q) \equiv p$
        - $p \lor (p \land q) \equiv p$
    - **8. 矛盾律**
        - $p \land \neg p \equiv F$
    - **9. 排中律**
        - $p \lor \neg p \equiv T$
    - **10. 双重否定律**
        - $\neg\neg p \equiv p$
    - **11. 德摩根律**
        - $\neg(p \land q) \equiv \neg p \lor \neg q$
        - $\neg(p \lor q) \equiv \neg p \land \neg q$
    - **12. 蕴含式**
        - $p \rightarrow q \equiv \neg p \lor q$
    - **13. 假言易位**
        - $p \rightarrow q \equiv \neg q \rightarrow \neg p$
    - **14. 等价式**
        - $p \leftrightarrow q \equiv (p \rightarrow q) \land (q \rightarrow p)$
        - $p \leftrightarrow q \equiv (p \land q) \lor (\neg p \land \neg q)$
    - **15. 归谬论**
        - $(p \rightarrow F) \equiv \neg p$
- 联结词的完备集
    - **联结词完备集**是对任一个命题公式,都能由其中的联结词表示出来的命题公式与之等价的联结词集合
    - 对于一共完备集的联结词集合S,从S中任意删去一种联结词后,得到的一个新的联结词集合 $ S_1 $ 至少有一共公式不等价于仅包含 $ S_1 $ 中联结词所表示的任意公式,则称S位极小完备的联结词集合
- 析取范式和合取范式
    - **文字**:命题变元或命题变元的否定称为文字
    - **析取式**:有限个文字的析取称为析取式,也称**子句**
    - **合取式**:有限个文字的合取称为合取式,也称**短语**
    - **互补对**:P与 $ \neg P$ 称为互补对
    - **析取范式**：有限个短语的析取式
    - **合取范式**：有限个子句的合取式
    - 由于析取\合取式和文字的判定比较变态，所以有很多反直觉的例子，例如：
        - $P$ 是文字、析取式、合取式、析取范式、合取范式
        - $P \lor Q \lor \neg R$ 是子句、析取范式、合取范式
        - $(P \lor Q \lor \neg R)$ 仅是子句、合取范式
        - $ \neg (Q \lor R)$ 什么都不是，但转换为 $ \neg Q \land \neg R$ 就是析取范式、合取范式
- 主析取范式和主合取范式
    - **极小项和极大项**
        - **极小项(Minterm)**：n个命题变元的所有文字的合取式，每个变元恰好出现一次（或原变元或否定）
            - 对于2个变元p,q，有4个极小项：$p \land q$, $p \land \neg q$, $\neg p \land q$, $\neg p \land \neg q$
            - 记作 $m_0, m_1, m_2, m_3$，下标对应真值指派的二进制编码
        - **极大项(Maxterm)**：n个命题变元的所有文字的析取式，每个变元恰好出现一次（或原变元或否定）
            - 对于2个变元p,q，有4个极大项：$p \lor q$, $p \lor \neg q$, $\neg p \lor q$, $\neg p \lor \neg q$
            - 记作 $M_0, M_1, M_2, M_3$，下标对应使该极大项为假的真值指派
    - **主析取范式(Principal Disjunctive Normal Form, PDNF)**
        - 由极小项构成的析取范式称为主析取范式
        - 每个命题公式都有唯一的主析取范式
        - 构造方法：选择使公式为真的所有极小项进行析取
        - 例如：$p \rightarrow q$ 的主析取范式为 $m_0 \lor m_2 \lor m_3$
    - **主合取范式(Principal Conjunctive Normal Form, PCNF)**
        - 由极大项构成的合取范式称为主合取范式
        - 每个命题公式都有唯一的主合取范式
        - 构造方法：选择使公式为假的所有极大项进行合取
        - 例如：$p \rightarrow q$ 的主合取范式为 $M_1$
    - **性质**
        - 对于n个变元，共有 $2^n$ 个极小项和 $2^n$ 个极大项
        - $m_i \land m_j = F$ (当 $i \neq j$ 时)
        - $M_i \lor M_j = T$ (当 $i \neq j$ 时)
        - $m_i \lor M_i = T$, $m_i \land M_i = F$
- **推理的基本概念和推理形式**
    - 推理定律(P86)
        - **附加律(Addition)**
            - $p \Rightarrow p \lor q$
            - 从 p 可以推出 p 或 q
        - **化简律(Simplification)**
            - $p \land q \Rightarrow p$
            - $p \land q \Rightarrow q$
            - 从 p 且 q 可以推出 p（或 q）
        - **假言推理(Modus Ponens)**
            - $p \rightarrow q, p \Rightarrow q$
            - 如果 p 蕴含 q，且 p 为真，则 q 为真
        - **拒取式(Modus Tollens)**
            - $p \rightarrow q, \neg q \Rightarrow \neg p$
            - 如果 p 蕴含 q，且 q 为假，则 p 为假
        - **析取三段论(Disjunctive Syllogism)**
            - $p \lor q, \neg p \Rightarrow q$
            - $p \lor q, \neg q \Rightarrow p$
            - 如果 p 或 q，且 p 为假，则 q 为真
        - **假言三段论(Hypothetical Syllogism)**
            - $p \rightarrow q, q \rightarrow r \Rightarrow p \rightarrow r$
            - 蕴含关系的传递性
        - **等价三段论(Equivalence)**
            - $p \leftrightarrow q, q \leftrightarrow r \Rightarrow p \leftrightarrow r$
            - 等价关系的传递性
        - **构造性二难(Constructive Dilemma)**
            - $p \rightarrow q, r \rightarrow s, p \lor r \Rightarrow q \lor s$
            - 如果两个条件都成立，且至少一个前提为真，则对应结论之一为真
        - **破坏性二难(Destructive Dilemma)**
            - $p \rightarrow q, r \rightarrow s, \neg q \lor \neg s \Rightarrow \neg p \lor \neg r$
            - 如果两个蕴含都成立，且至少一个结论为假，则对应前提之一为假
        - **合取律(Conjunction)**
            - $p, q \Rightarrow p \land q$
            - 如果 p 和 q 都为真，则 p 且 q 为真
    - 演绎法
        - **规则P(前提引用规则, Premise Rule)**
            - 在推理的任何步骤中，都可以引入前提作为推理的依据
            - 记作：前提 $p$ 可以在推理中的任何地方写下
            - 作用：允许我们在证明过程中随时使用已知的前提条件
        - **规则T(逻辑结果引用规则, Tautology Rule)**
            - 在推理的任何步骤中，都可以引入重言式(永真公式)作为推理的依据
            - 重言式在任何解释下都为真，因此可以作为有效的推理步骤
            - 例如：可以引入 $p \lor \neg p$、$(p \rightarrow q) \leftrightarrow (\neg p \lor q)$ 等
            - 作用：允许我们使用逻辑上必然为真的公式
        - **规则CP(附加条件规则, Conditional Proof Rule)**
            - 为了证明 $p \rightarrow q$，可以假设 $p$ 为真，然后推导出 $q$
            - 如果在假设 $p$ 的条件下能够推导出 $q$，则可以结论 $p \rightarrow q$
            - 作用：这是证明条件语句的标准方法，通过临时假设前件来证明后件
        - **推理示例**
            - 要证明：$(p \rightarrow q) \land (q \rightarrow r) \Rightarrow (p \rightarrow r)$
            - 证明过程：
                1. $p \rightarrow q$ (P)
                2. $q \rightarrow r$ (P)
                3. $p$ (CP)
                4. $q$ (T (1,3) I)
                5. $r$ (T (2,4) I)
                6. $p \rightarrow r$ (CP)
### 谓词逻辑
- **谓词**
    - 在原子命题中，可以独立存在的客体称为**个体词**；而用以刻画客体性质或客体之间关系的即是**谓词**。
    - 个体常量：表示具体或特定的个体词称为个体常量，一般用a，b，c等表示
    - 个体变量：表示抽象或泛指的个体词称为个体变量，一般用x，y，z等表示
    - 个体词的取值范围称为**个体域**(或论域)，常用D表示
    - 宇宙间的所有个体域聚集在一起所构成的个体域称为**全总个体域**
    - 设D为非空的个体域，定义 $D^n$ (表示n个个体都在个体域D上取值)上取值于{0，1}上的n元函数，称为**n元命题函数**或**n元谓词**，记为 $P(x_1,x_2,...x_n)$ 此时，个体变量 $(x_1,x_2,...x_n)$ 的定义域为D，$P(x_1,x_2,...x_n)$ 的值域为{0,1}。
    - 显然，**多元谓词中交换个体顺序往往是灾难的**
- **量词**
    - 全称量词(Universal Quantifier)
        - 符号：$\forall$（读作"对于所有"或"任意"）
        - 含义：表示个体域中的每一个个体都满足某种性质
        - 形式：$\forall x P(x)$ 表示"对于个体域中的任意个体x，P(x)都为真"
        - 例子：$\forall x (x > 0)$ 表示"所有的x都大于0"
    - 存在量词(Existential Quantifier)
        - 符号：$\exists$（读作"存在"）
        - 含义：表示个体域中至少存在一个个体满足某种性质
        - 形式：$\exists x P(x)$ 表示"在个体域中存在个体x，使得P(x)为真"
        - 例子：$\exists x (x^2 = 4)$ 表示"存在x使得x的平方等于4"
    - **唯一存在量词**
        - 符号：$\exists!$ 或 $\exists_1$
        - 含义：表示个体域中存在唯一一个个体满足某种性质
        - 形式：$\exists! x P(x)$ 表示"存在唯一的x使得P(x)为真"
        - 可以表示为：$\exists x (P(x) \land \forall y (P(y) \rightarrow x = y))$
    - **多重量词**
        - 当公式中含有多个量词时，量词的顺序很重要
        - $\forall x \exists y P(x,y)$：对每个x，都存在某个y使得P(x,y)成立
        - $\exists y \forall x P(x,y)$：存在某个y，对所有x都使得P(x,y)成立
        - 一般情况下：$\forall x \exists y P(x,y) \not\equiv \exists y \forall x P(x,y)$
    - **谓词符号化的两条规则**
        - 对于全称量词，刻画其对应个体域的特性谓词作为蕴含式之前件加入
        - 对应存在量词，刻画其对应个体域的特性谓词作为合取式之合取项加入
        - 例如：
            - "所有鸟都会飞"：$\forall x (Bird(x) \rightarrow Fly(x))$
            - "存在不会飞的鸟"：$\exists x (Bird(x) \land \neg Fly(x))$
            - "所有整数都大于0"：$\forall x (Integer(x) \rightarrow x > 0)$
            - "存在小于5的正整数"：$\exists x (PositiveInteger(x) \land x < 5)$
        - **注意**
            - 全称量词用蕴含($\rightarrow$)，因为我们不要求所有个体都满足特性谓词
            - 存在量词用合取($\land$)，因为我们要求存在的个体同时满足特性谓词和目标谓词
- 谓词的合式公式
    - 谓词逻辑中的**项**，被递归地定义为：
        - 任意的常量符号或任意的变量符号是项
        - 若 $f(x_1,x_2,...x_n)$ 是n元函数符号  $x_1,x_2,...x_n$ 是项，则 $f(x_1,x_2,...x_n)$ 也是项。
        - 由有限次使用上述规则产生的符号串是项
    - **原子公式**
        - 若 $P(x_1,x_2,...x_n)$ 是n元谓词，$x_1,x_2,...x_n$ 是项，则称 $P(x_1,x_2,...x_n)$ 是原子公式
    - **合式公式**
        - 原子公式是合式公式
        - 若 G，H是合式公式，则这两个公式经过单次逻辑变换依旧是合式公式
        - 若G是合式公式。x是个体变元则 $ (\forall x)G$， $(\exists x)G$ 也是合式公式
        - 由有限次使用上述规则产生的表达式是合式公式
        - **命题公式是谓词合式公式的一种特例**
- **量词的辖域(Scope)**
    - 量词作用的范围称为量词的辖域
    - 在辖域内，相应的个体变量称为**约束变量**
    - 不在任何量词辖域内的个体变量称为**自由变量**
    - **若量词后有括号，则括号内的子公式就算该量词的辖域**
    - **若量词后无括号，则与量词邻接的子公式为该量词的辖域**
- 谓词合式公式的解释
    - 谓词逻辑中公式G的每一个解释 $I$ 由如下四部分组成
        - 非空的个体域集合 $D$
        - 公式G中的每个变量符号。指定D中的某个特定的元素
        - 公式G中的每个n元函数符号，指定 $D^n$ 到D中的某个特定的函数
        - 公式G中的每个n元谓词符号，指定， $D^n$ 到{0,1}中的某个特定的谓词
    - 例题(建议直接看P113，很绕)
- 谓词合式公式的分类
    - 如果公式在它的所有解释下都为真，则公式G称为**有效公式**
    - 如果取值都为假，则称为**矛盾公式**
    - 如果不是矛盾公式，则称为**可满足公式**
- 谓词合式公式的基本等价关系
    - 如果公式 $G \leftrightarrow H$,则公式G，H称为**等价的**，记为G=H
    - 设 $G(P_1,P_2,...,P_n)$ 是命题演算中的命题公式 $P_1,P_2,...,P_n$ 是出现在G中的命题变元，当用任意的谓词公式 $G_i$ 分别带入 $P_i$ 后，得到新的谓词公式 $G(G_1,G_2,...,G_n)$ 称为原公式的代入实例。
    - 永真公式的任意一共代入实例必为有效公式
    - 基本等价关系(P116)
- 前束范式
    - 称公式G是一个前束范式，如果G中的一切量词都位于该公式最前端(不含否定词)且这些量词的辖域都延申到公式的末端
        - 前束范式的标准形式为： $(Q_1 x_1)(Q_2 x_2)...(Q_n x_n) M(x_1, x_2, ..., x_n)$
