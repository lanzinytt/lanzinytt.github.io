---
layout:     post
title:      "离散数学梳理.25"
subtitle:   " \"Math learning\""
date:       2025-06-02 15:00:00
author:     "LanZinYtt"
header-img: "img/in-post/Discrete_mathematics/Dismath_header.jpg"
catalog: true
tags:
    - Computer_Science_Specialized_Courses
---
<p id = "build"></p>

>希望大伙都能考出好成绩叭😘

# 离散数学

<div class="mermaid">
graph TD
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
    - $ A = \{a,b,c,d\} $ ;
    - $ B = \{1,3,5,7,...,2n+1,...\} $
  - 叙述法(隐式法)
    - 通过刻画集合中元素所具备的某种特性来表示集合，常记为 $$\{ x \mid P(x) \}$$
    - $$S = \{x\mid x \in \mathbb{Z} ,x^2+1=0 \}$$
  - 归纳法
    - 通过归纳定义集合，一般包括：基础(最基本的元素构成)、归纳(构造新元素的方法)、极小性(规定集合的界限)。
  - 递归指定集合法
    - $$a_0=1,a_{i+1}=2a_i(i \geq 0),S=\{a_k\mid k \geq 0\}$$
  - 文氏图(Venn diagram)
- 集合与元素的关系
  - 元素与集合之间的 $$ \in $$ 关系是明确的
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
    - 不包含任何元素的集合称为空集，记作 $$ \emptyset$$
    - 也可符号化为 $$\emptyset = \{x\mid x \not= x \}$$
    - 空集是一切集合的子集
    - **空集是绝对唯一的**
  - 全集
    - 在一个相对固定的范围内，包含此范围内所有元素的集合，称为全集或论集，记作 U或 E
  - 基数
    - 集合中的元素个数称为集合的基数，记作 $$ \mid A\mid  $$
    - 如果一个集合的基数是有限的，则称该集合为有限集
    - 如果一个集合的基数是无限的，则称该集合为无限集
  - n元(子)集
    - 如果一个集合A含有n个元素，则称集合A为n元集
    - 如果一个n元集合A存在一个子集含有m个$$(n \geq m \geq 0)$$元素
    - 一般来说n元集共有 $$2^n$$ 个不同的子集
  - **幂集**
    - 设A为任意集合，把A的所有不同子集构成的集合称为A的幂集，记作 $$ P(A) $$ 或 $$2^A$$
    - 也可符号化为 $$P(A)=\{x\mid x \subseteq A \}$$
  - 集族
    - 把集合作为元素而构成的集合称为集族
    - 幂集是集族
- 集合的运算
  - **并集(Union)**
    - 设A、B为两个集合，由所有属于A或属于B的元素构成的集合称为A与B的并集
    - 记作 $$A \cup B = \{x \mid x \in A \text{ 或 } x \in B\}$$
  - **交集(Intersection)**
    - 设A、B为两个集合，由所有既属于A又属于B的元素构成的集合称为A与B的交集
    - 记作 $$A \cap B = \{x \mid x \in A \text{ 且 } x \in B\}$$
  - **差集(Difference)**
    - 设A、B为两个集合，由所有属于A但不属于B的元素构成的集合称为A与B的差集
    - 记作 $$A - B = \{x \mid x \in A \text{ 且 } x \notin B\}$$
  - **补集(Complement)**
    - 设A为全集U的子集，由所有属于U但不属于A的元素构成的集合称为A的补集
    - 记作 $$\overline{A} = \{x \mid x \in U \text{ 且 } x \notin A\}$$
    - 也可记作 $$A^c$$ 或 $$\sim A$$
  - **对称差(Symmetric Difference)**
    - 设A、B为两个集合，由所有属于A但不属于B或属于B但不属于A的元素构成的集合称为A与B的对称差
    - 记作 $$A \oplus B = (A - B) \cup (B - A) = (A \cup B) - (A \cap B)$$
- **可数集合和不可数集合**
  - **可数集合(Countable Set)**
    - 如果一个集合是有限的，或者与自然数集合 $$\mathbb{N}$$ 等势，则称该集合为可数集合
    - 例子：
      - 自然数集 $$\mathbb{N} = \{0,1,2,3,...\}$$
      - 整数集 $$\mathbb{Z} = \{...,-2,-1,0,1,2,...\}$$
      - 有理数集 $$\mathbb{Q}$$
      - 偶数集 $$\{0,2,4,6,...\}$$
  - **不可数集合(Uncountable Set)**
    - 如果一个无限集合不是可数的，则称其为不可数集合
    - 不可数集合的基数严格大于自然数集合的基数
    - 例子：
      - 实数集 $$\mathbb{R}$$
      - 区间 $$(0,1)$$ 中的所有实数
      - 幂集 $$P(\mathbb{N})$$（自然数集的幂集）

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
    - **否定(Negation)** $$\neg$$
      - $$\neg p$$：p的否定，当p为真时$$\neg p$$为假，当p为假时$$\neg p$$为真
    - **合取(Conjunction)** $$\land$$
      - $$p \land q$$：p与q，只有当p和q都为真时才为真
    - **析取(Disjunction)** $$\lor$$
      - $$p \lor q$$：p或q，只有当p和q都为假时才为假
    - **蕴含(Implication)** $$\rightarrow$$
      - $$p \rightarrow q$$：如果p则q，只有当p为真且q为假时才为假
    - **等价(Equivalence)** $$\leftrightarrow$$
      - $$p \leftrightarrow q$$：p当且仅当q，当p和q真值相同时为真
    - 优先级如下：
      - 否定>合取>析取>蕴含>等价
      - 同级按照从左到右的次序
  - 真值表(Truth Table)
    - 用表格形式列出命题公式在所有可能真值指派下的真值
- 命题公式
  - 命题演算的**合式公式**称作命题公式
  - 生成规则
    - 命题变元本身是一个公式
    - 如果G是公式，则 $$(\neg G)$$ 也是公式
    - 如果G，H是公式，则 $$(G \land H)$$ $$(G \lor H)$$ $$(G \rightarrow H)$$ $$(G \leftrightarrow H)$$ 也是命题公式
    - 仅通过有限步使用上述规则得到的符号串才是命题公式。
  - **命题公式没有真值**，只有在对其命题变元进行真值指派后，才可确定命题公式的真值
- 命题公式的解释与真值表
  - **解释(Interpretation)**
    - 解释是给命题公式中的每个命题变元指定一个真值（T或F）
    - 一个含有n个命题变元的公式共有 $$2^n$$ 种不同的解释
    - 例如：公式 $$p \land q$$ 有4种解释：
      - $$p=1, q=1$$
      - $$p=1, q=0$$
      - $$p=0, q=1$$
      - $$p=0, q=0$$
    - 一组解释常记作 $$I$$
  - **真值表(Truth Table)**
    - 真值表是列举公式在所有可能解释下的真值的表格
    - 例如：$$(p \land q) \lor \neg r$$ 的真值表

            | p | q | r | $$p \land q$$ | $$\neg r$$ | $$(p \land q) \lor \neg r$$ |
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
    - $$p \land p \equiv p$$
    - $$p \lor p \equiv p$$
  - **2. 交换律**
    - $$p \land q \equiv q \land p$$
    - $$p \lor q \equiv q \lor p$$
  - **3. 结合律**
    - $$(p \land q) \land r \equiv p \land (q \land r)$$
    - $$(p \lor q) \lor r \equiv p \lor (q \lor r)$$
  - **4. 同一律**
    - $$p \land T \equiv p$$
    - $$p \lor F \equiv p$$
  - **5. 零律**
    - $$p \land F \equiv F$$
    - $$p \lor T \equiv T$$
  - **6. 分配律**
    - $$p \land (q \lor r) \equiv (p \land q) \lor (p \land r)$$
    - $$p \lor (q \land r) \equiv (p \lor q) \land (p \lor r)$$
  - **7. 吸收律**
    - $$p \land (p \lor q) \equiv p$$
    - $$p \lor (p \land q) \equiv p$$
  - **8. 矛盾律**
    - $$p \land \neg p \equiv F$$
  - **9. 排中律**
    - $$p \lor \neg p \equiv T$$
  - **10. 双重否定律**
    - $$\neg\neg p \equiv p$$
  - **11. 德摩根律**
    - $$\neg(p \land q) \equiv \neg p \lor \neg q$$
    - $$\neg(p \lor q) \equiv \neg p \land \neg q$$
  - **12. 蕴含式**
    - $$p \rightarrow q \equiv \neg p \lor q$$
  - **13. 假言易位**
    - $$p \rightarrow q \equiv \neg q \rightarrow \neg p$$
  - **14. 等价式**
    - $$p \leftrightarrow q \equiv (p \rightarrow q) \land (q \rightarrow p)$$
    - $$p \leftrightarrow q \equiv (p \land q) \lor (\neg p \land \neg q)$$
  - **15. 归谬论**
    - $$(p \rightarrow F) \equiv \neg p$$
- 联结词的完备集
  - **联结词完备集**是对任一个命题公式,都能由其中的联结词表示出来的命题公式与之等价的联结词集合
  - 对于一共完备集的联结词集合S,从S中任意删去一种联结词后,得到的一个新的联结词集合 $$ S_1 $$ 至少有一共公式不等价于仅包含 $$ S_1 $$ 中联结词所表示的任意公式,则称S位极小完备的联结词集合
- 析取范式和合取范式
  - **文字**:命题变元或命题变元的否定称为文字
  - **析取式**:有限个文字的析取称为析取式,也称**子句**
  - **合取式**:有限个文字的合取称为合取式,也称**短语**
  - **互补对**:P与 $$ \neg P$$ 称为互补对
  - **析取范式**：有限个短语的析取式
  - **合取范式**：有限个子句的合取式
  - 由于析取\合取式和文字的判定比较变态，所以有很多反直觉的例子，例如：
    - $P$ 是文字、析取式、合取式、析取范式、合取范式
    - $P \lor Q \lor \neg R$ 是子句、析取范式、合取范式
    - $(P \lor Q \lor \neg R)$ 仅是子句、合取范式
    - $$ \neg (Q \lor R)$$ 什么都不是，但转换为 $$ \neg Q \land \neg R$$ 就是析取范式、合取范式
- 主析取范式和主合取范式
  - **极小项和极大项**
    - **极小项(Minterm)**：n个命题变元的所有文字的合取式，每个变元恰好出现一次（或原变元或否定）
      - 对于2个变元p,q，有4个极小项：$$p \land q$$, $$p \land \neg q$$, $$\neg p \land q$$, $$\neg p \land \neg q$$
      - 记作 $$m_0, m_1, m_2, m_3$$，下标对应真值指派的二进制编码
    - **极大项(Maxterm)**：n个命题变元的所有文字的析取式，每个变元恰好出现一次（或原变元或否定）
      - 对于2个变元p,q，有4个极大项：$$p \lor q$$, $$p \lor \neg q$$, $$\neg p \lor q$$, $$\neg p \lor \neg q$$
      - 记作 $$M_0, M_1, M_2, M_3$$，下标对应使该极大项为假的真值指派
  - **主析取范式(Principal Disjunctive Normal Form, PDNF)**
    - 由极小项构成的析取范式称为主析取范式
    - 每个命题公式都有唯一的主析取范式
    - 构造方法：选择使公式为真的所有极小项进行析取
    - 例如：$$p \rightarrow q$$ 的主析取范式为 $$m_0 \lor m_2 \lor m_3$$
  - **主合取范式(Principal Conjunctive Normal Form, PCNF)**
    - 由极大项构成的合取范式称为主合取范式
    - 每个命题公式都有唯一的主合取范式
    - 构造方法：选择使公式为假的所有极大项进行合取
    - 例如：$$p \rightarrow q$$ 的主合取范式为 $$M_1$$
  - **性质**
    - 对于n个变元，共有 $$2^n$$ 个极小项和 $$2^n$$ 个极大项
    - $$m_i \land m_j = F$$ (当 $$i \neq j$$ 时)
    - $$M_i \lor M_j = T$$ (当 $$i \neq j$$ 时)
    - $$m_i \lor M_i = T$$, $$m_i \land M_i = F$$
- **推理的基本概念和推理形式**
  - 推理定律(P86)
    - **附加律(Addition)**
      - $$p \Rightarrow p \lor q$$
      - 从 p 可以推出 p 或 q
    - **化简律(Simplification)**
      - $$p \land q \Rightarrow p$$
      - $$p \land q \Rightarrow q$$
      - 从 p 且 q 可以推出 p（或 q）
    - **假言推理(Modus Ponens)**
      - $$p \rightarrow q, p \Rightarrow q$$
      - 如果 p 蕴含 q，且 p 为真，则 q 为真
    - **拒取式(Modus Tollens)**
      - $$p \rightarrow q, \neg q \Rightarrow \neg p$$
      - 如果 p 蕴含 q，且 q 为假，则 p 为假
    - **析取三段论(Disjunctive Syllogism)**
      - $$p \lor q, \neg p \Rightarrow q$$
      - $$p \lor q, \neg q \Rightarrow p$$
      - 如果 p 或 q，且 p 为假，则 q 为真
    - **假言三段论(Hypothetical Syllogism)**
      - $$p \rightarrow q, q \rightarrow r \Rightarrow p \rightarrow r$$
      - 蕴含关系的传递性
    - **等价三段论(Equivalence)**
      - $$p \leftrightarrow q, q \leftrightarrow r \Rightarrow p \leftrightarrow r$$
      - 等价关系的传递性
    - **构造性二难(Constructive Dilemma)**
      - $$p \rightarrow q, r \rightarrow s, p \lor r \Rightarrow q \lor s$$
      - 如果两个条件都成立，且至少一个前提为真，则对应结论之一为真
    - **破坏性二难(Destructive Dilemma)**
      - $$p \rightarrow q, r \rightarrow s, \neg q \lor \neg s \Rightarrow \neg p \lor \neg r$$
      - 如果两个蕴含都成立，且至少一个结论为假，则对应前提之一为假
    - **合取律(Conjunction)**
      - $$p, q \Rightarrow p \land q$$
      - 如果 p 和 q 都为真，则 p 且 q 为真
  - 演绎法
    - **规则P(前提引用规则, Premise Rule)**
      - 在推理的任何步骤中，都可以引入前提作为推理的依据
      - 记作：前提 $$p$$ 可以在推理中的任何地方写下
      - 作用：允许我们在证明过程中随时使用已知的前提条件
    - **规则T(逻辑结果引用规则, Tautology Rule)**
      - 在推理的任何步骤中，都可以引入重言式(永真公式)作为推理的依据
      - 重言式在任何解释下都为真，因此可以作为有效的推理步骤
      - 例如：可以引入 $$p \lor \neg p$$、$$(p \rightarrow q) \leftrightarrow (\neg p \lor q)$$ 等
      - 作用：允许我们使用逻辑上必然为真的公式
    - **规则CP(附加条件规则, Conditional Proof Rule)**
      - 为了证明 $$p \rightarrow q$$，可以假设 $$p$$ 为真，然后推导出 $$q$$
      - 如果在假设 $$p$$ 的条件下能够推导出 $$q$$，则可以结论 $$p \rightarrow q$$
      - 作用：这是证明条件语句的标准方法，通过临时假设前件来证明后件
    - **推理示例**
      - 要证明：$$(p \rightarrow q) \land (q \rightarrow r) \Rightarrow (p \rightarrow r)$$
      - 证明过程：
                1. $$p \rightarrow q$$ (P)
                2. $$q \rightarrow r$$ (P)
                3. $$p$$ (CP)
                4. $$q$$ (T (1,3) I)
                5. $$r$$ (T (2,4) I)
                6. $$p \rightarrow r$$ (CP)

### 谓词逻辑

- **谓词**
  - 在原子命题中，可以独立存在的客体称为**个体词**；而用以刻画客体性质或客体之间关系的即是**谓词**。
  - 个体常量：表示具体或特定的个体词称为个体常量，一般用a，b，c等表示
  - 个体变量：表示抽象或泛指的个体词称为个体变量，一般用x，y，z等表示
  - 个体词的取值范围称为**个体域**(或论域)，常用D表示
  - 宇宙间的所有个体域聚集在一起所构成的个体域称为**全总个体域**
  - 设D为非空的个体域，定义 $$D^n$$ (表示n个个体都在个体域D上取值)上取值于{0，1}上的n元函数，称为**n元命题函数**或**n元谓词**，记为 $$P(x_1,x_2,...x_n)$$ 此时，个体变量 $$(x_1,x_2,...x_n)$$ 的定义域为D，$$P(x_1,x_2,...x_n)$$ 的值域为{0,1}。
  - 显然，**多元谓词中交换个体顺序往往是灾难的**
- **量词**
  - 全称量词(Universal Quantifier)
    - 符号：$$\forall$$（读作"对于所有"或"任意"）
    - 含义：表示个体域中的每一个个体都满足某种性质
    - 形式：$$\forall x P(x)$$ 表示"对于个体域中的任意个体x，P(x)都为真"
    - 例子：$$\forall x (x > 0)$$ 表示"所有的x都大于0"
  - 存在量词(Existential Quantifier)
    - 符号：$$\exists$$（读作"存在"）
    - 含义：表示个体域中至少存在一个个体满足某种性质
    - 形式：$$\exists x P(x)$$ 表示"在个体域中存在个体x，使得P(x)为真"
    - 例子：$$\exists x (x^2 = 4)$$ 表示"存在x使得x的平方等于4"
  - **唯一存在量词**
    - 符号：$$\exists!$$ 或 $$\exists_1$$
    - 含义：表示个体域中存在唯一一个个体满足某种性质
    - 形式：$$\exists! x P(x)$$ 表示"存在唯一的x使得P(x)为真"
    - 可以表示为：$$\exists x (P(x) \land \forall y (P(y) \rightarrow x = y))$$
  - **多重量词**
    - 当公式中含有多个量词时，量词的顺序很重要
    - $\forall x \exists y P(x,y)$ ：对每个x，都存在某个y使得P(x,y)成立
    - $\exists y \forall x P(x,y)$ ：存在某个y，对所有x都使得P(x,y)成立
    - 一般情况下：$$\forall x \exists y P(x,y) \not\equiv \exists y \forall x P(x,y)$$
  - **谓词符号化的两条规则**
    - 对于全称量词，刻画其对应个体域的特性谓词作为蕴含式之前件加入
    - 对应存在量词，刻画其对应个体域的特性谓词作为合取式之合取项加入
    - 例如：
      - "所有鸟都会飞"：$$\forall x (Bird(x) \rightarrow Fly(x))$$
      - "存在不会飞的鸟"：$$\exists x (Bird(x) \land \neg Fly(x))$$
      - "所有整数都大于0"：$$\forall x (Integer(x) \rightarrow x > 0)$$
      - "存在小于5的正整数"：$$\exists x (PositiveInteger(x) \land x < 5)$$
    - **注意**
      - 全称量词用蕴含($\rightarrow$)，因为我们不要求所有个体都满足特性谓词
      - 存在量词用合取($\land$)，因为我们要求存在的个体同时满足特性谓词和目标谓词
- 谓词的合式公式
  - 谓词逻辑中的**项**，被递归地定义为：
    - 任意的常量符号或任意的变量符号是项
    - 若 $$f(x_1,x_2,...x_n)$$ 是n元函数符号  $$x_1,x_2,...x_n$$ 是项，则 $$f(x_1,x_2,...x_n)$$ 也是项。
    - 由有限次使用上述规则产生的符号串是项
  - **原子公式**
    - 若 $$P(x_1,x_2,...x_n)$$ 是n元谓词，$$x_1,x_2,...x_n$$ 是项，则称 $$P(x_1,x_2,...x_n)$$ 是原子公式
  - **合式公式**
    - 原子公式是合式公式
    - 若 G，H是合式公式，则这两个公式经过单次逻辑变换依旧是合式公式
    - 若G是合式公式。x是个体变元则 $$ (\forall x)G$$， $$(\exists x)G$$ 也是合式公式
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
  - 如果公式 $$G \leftrightarrow H$$,则公式G，H称为**等价的**，记为G=H
  - 设 $$G(P_1,P_2,...,P_n)$$ 是命题演算中的命题公式 $$P_1,P_2,...,P_n$$ 是出现在G中的命题变元，当用任意的谓词公式 $$G_i$$ 分别带入 $$P_i$$ 后，得到新的谓词公式 $$G(G_1,G_2,...,G_n)$$ 称为原公式的代入实例。
  - 永真公式的任意一共代入实例必为有效公式
  - 基本等价关系(P116)
- 前束范式
  - 称公式G是一个前束范式，如果G中的一切量词都位于该公式最前端(不含否定词)且这些量词的辖域都延申到公式的末端
    - 前束范式的标准形式为： $$(Q_1 x_1)(Q_2 x_2)...(Q_n x_n) M(x_1, x_2, ..., x_n)$$
- 谓词的演绎与推理(P121)
  - **全称量词消去规则(Universal Instantiation, US)**
    - 如果 $$\forall x P(x)$$ 为真，则对个体域中的任意个体c，$$P(c)$$ 为真
    - 形式：$$\forall x P(x) \Rightarrow P(c)$$（c是个体域中的任意个体）
    - 例如：从"所有人都会死"可以推出"苏格拉底会死"
  - **全称量词引入规则(Universal Generalization, UG)**
    - 如果对个体域中的任意个体c，$$P(c)$$ 为真，则 $$\forall x P(x)$$ 为真
    - 形式：$$P(c) \Rightarrow \forall x P(x)$$（c是任意选取的个体）
    - **限制条件**：c必须是任意选取的，不能是特定的个体
  - **存在量词消去规则(Existential Instantiation, ES)**
    - 如果 $$\exists x P(x)$$ 为真，则存在个体域中的某个个体c使得 $$P(c)$$ 为真
    - 形式：$$\exists x P(x) \Rightarrow P(c)$$（c是一个新引入的个体常量）
    - **限制条件**：c必须是在推理过程中首次出现的新个体常量
  - **存在量词引入规则(Existential Generalization, EG)**
    - 如果对个体域中的某个个体c，$$P(c)$$ 为真，则 $$\exists x P(x)$$ 为真
    - 形式：$$P(c) \Rightarrow \exists x P(x)$$
    - 例如：从"苏格拉底是人"可以推出"存在人"
  - **量词否定规则**
    - $$\neg \forall x P(x) \equiv \exists x \neg P(x)$$
    - $$\neg \exists x P(x) \equiv \forall x \neg P(x)$$
  - **推理示例**
    - **前提**：
            1. $$\forall x (Human(x) \rightarrow Mortal(x))$$ （所有人都会死）
            2. $$Human(Socrates)$$ （苏格拉底是人）
    - **结论**：$$Mortal(Socrates)$$ （苏格拉底会死）
    - **证明过程**：
            1. $$\forall x (Human(x) \rightarrow Mortal(x))$$ (P)
            2. $$Human(Socrates)$$ (P)
            3. $$Human(Socrates) \rightarrow Mortal(Socrates)$$ (US (1))
            4. $$Mortal(Socrates)$$ (T (2,3) I)
  - **注意事项**
    - 使用UG规则时，个体必须是任意选取的
    - 使用ES规则时，引入的个体常量必须是新的
    - 量词的辖域必须正确理解
    - 约束变量和自由变量要严格区分

## 二元关系

### 二元关系

- 序偶合笛卡尔积
  - **序偶(Ordered Pair)**
    - 由两个元素a和b按一定顺序组成的二元组，记作 $$\langle a, b \rangle$$ 或 $$(a, b)$$
    - 特点：$$\langle a, b \rangle = \langle c, d \rangle$$ 当且仅当 $$a = c$$ 且 $$b = d$$
    - 序偶具有顺序性：一般情况下 $$\langle a, b \rangle \neq \langle b, a \rangle$$
    - 第一个元素a称为**第一分量**，第二个元素b称为**第二分量**
  - **笛卡尔积(Cartesian Product)**
    - 设A、B为两个集合，由所有以A中元素为第一分量、B中元素为第二分量的序偶构成的集合称为A与B的笛卡尔积
    - 记作：$$A \times B = \{\langle a, b \rangle \mid a \in A \land b \in B\}$$
    - 例如：$$A = \{1, 2\}$$，$$B = \{a, b\}$$，则 $$A \times B = \{\langle 1, a \rangle, \langle 1, b \rangle, \langle 2, a \rangle, \langle 2, b \rangle\}$$
  - **n元组(n-tuple)**
    - 由n个元素按一定顺序组成的有序组合，记作 $$\langle a_1, a_2, ..., a_n \rangle$$
    - 2元组就是序偶，3元组称为三元组，依此类推
  - **笛卡尔积的性质**
    - **基数性质**：$$\mid A \times B\mid = \mid A \mid \times \mid B \mid$$
    - **不满足交换律**：一般情况下 $$A \times B \neq B \times A$$
    - **不满足结合律**：$$(A \times B) \times C \neq A \times (B \times C)$$
    - **基数性质**： $|A \times B| = |A| \times |B|$
    - **不满足交换律**：一般情况下 $A \times B \neq B \times A$
    - **不满足结合律**：$(A \times B) \times C \neq A \times (B \times C)$
    - **对并运算的分配律**：
      - $$A \times (B \cup C) = (A \times B) \cup (A \times C)$$
      - $$(A \cup B) \times C = (A \times C) \cup (B \times C)$$
    - **对交运算的分配律**：
      - $$A \times (B \cap C) = (A \times B) \cap (A \times C)$$
      - $$(A \cap B) \times C = (A \times C) \cap (B \times C)$$
    - **对差运算的分配律**：
      - $$A \times (B - C) = (A \times B) - (A \times C)$$
      - $$(A - B) \times C = (A \times C) - (B \times C)$$
  - **特殊情况**
    - 若A或B为空集，则 $$A \times B = \emptyset$$
    - $$A \times A$$ 记作 $$A^2$$，称为A的2次笛卡尔幂
    - 一般地，$$A^n = A \times A \times ... \times A$$（n个A的笛卡尔积）
  - **几何解释**
    - 实数集R上的笛卡尔积 $$\mathbb{R} \times \mathbb{R} = \mathbb{R}^2$$ 对应平面上所有点的集合
    - 区间 $$[a,b] \times [c,d]$$ 对应平面上的矩形区域
- 关系的定义
  - 设A，B为两个非空集合，称$$(A \times B)$$的任意子集R为从A到B的一个**二元关系**
  - 如果$$\langle a, b \rangle \in R$$，则称a与b有关系R，记作$$aRb$$
  - 如果$$\langle a, b \rangle \notin R$$，则称a与b没有关系R，记作$$a\overline{R}b$$
  - **特殊的二元关系**
    - **空关系(Empty Relation)**
      - 空集$$\emptyset$$称为从A到B的空关系
      - 记作：$$R = \emptyset$$
      - 性质：对于任意$$a \in A, b \in B$$，都有$$a\overline{R}b$$
      - 含义：A中任何元素都与B中任何元素没有关系
    - **全关系(Universal Relation)**
      - 笛卡尔积$$A \times B$$称为从A到B的全关系
      - 记作：$$R = A \times B$$
      - 性质：对于任意$$a \in A, b \in B$$，都有$$aRb$$
      - 含义：A中每个元素都与B中每个元素有关系
    - **恒等关系(Identity Relation)**
      - 当$$A = B$$时，集合 $$I_A = \{\langle a, a \rangle \mid  a \in A\}$$ 称为A上的恒等关系
      - 记作：$$I_A$$或$$\Delta_A$$
      - 性质：$$aI_Ab$$当且仅当$$a = b$$
      - 当 $ A = B $ 时，集合 $I_A = \{\langle a, a \rangle | a \in A\}$ 称为A上的恒等关系
      - 记作：$I_A$或$\Delta_A$
      - 性质：$aI_Ab$当且仅当$a = b$
      - 含义：只有相同的元素之间才有关系
      - 例如：若$$A = \{1, 2, 3\}$$，则$$I_A = \{\langle 1, 1 \rangle, \langle 2, 2 \rangle, \langle 3, 3 \rangle\}$$
- 关系的表示方法
  - **集合表示法：列出所有序偶**
    - 直接列举关系中的所有有序对
    - 例如：设$$A = \{1, 2, 3\}$$，关系$$R = \{\langle 1, 2 \rangle, \langle 2, 3 \rangle, \langle 3, 1 \rangle\}$$
    - 例如：设 $A = \{1, 2, 3\}$ ，关系 $R = \{\langle 1, 2 \rangle, \langle 2, 3 \rangle, \langle 3, 1 \rangle\}$
  - **关系矩阵：用0-1矩阵表示关系**
    - 设$$A = \{a_1, a_2, ..., a_m\}$$，$$B = \{b_1, b_2, ..., b_n\}$$
    - 关系矩阵$$M_R = (m_{ij})_{m \times n}$$，其中$$m_{ij} = 1$$当且仅当$$\langle a_i, b_j \rangle \in R$$
    - 例如：上述关系R的矩阵为$$\begin{pmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ 1 & 0 & 0 \end{pmatrix}$$
    - 设 $A = \{a_1, a_2, ..., a_m\}$ ，$B = \{b_1, b_2, ..., b_n\}$
    - 关系矩阵 $M_R = (m_{ij})_{m \times n}$ ，其中 $m_{ij} = 1$ 当且仅当$\langle a_i, b_j \rangle \in R$
    - 例如：上述关系R的矩阵为 $\begin{pmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ 1 & 0 & 0 \end{pmatrix}$
    - **关系矩阵的布尔积运算**
      - **定义**：两个关系矩阵$$A = (a_{ij})_{m \times p}$$和$$B = (b_{jk})_{p \times n}$$的布尔积记作$$A \odot B$$
      - **计算公式**：$$(A \odot B)_{ik} = \bigvee_{j=1}^{p} (a_{ij} \land b_{jk})$$
      - **定义**：两个关系矩阵 $A = (a_{ij})_{m \times p}$和$B = (b_{jk})_{p \times n}$ 的布尔积记作 $A \odot B$
      - **计算公式**：$(A \odot B)_{ik} = \bigvee_{j=1}^{p} (a_{ij} \land b_{jk})$
      - **具体步骤**：
        - 第i行第k列的元素 = (第i行与第k列对应元素相与)的析取
        - 即：$$c_{ik} = (a_{i1} \land b_{1k}) \lor (a_{i2} \land b_{2k}) \lor ... \lor (a_{ip} \land b_{pk})$$
      - **应用**：关系复合运算的矩阵表示
        - 若$$R_1: A \rightarrow B$$，$$R_2: B \rightarrow C$$
        - 则复合关系$$R_1 \circ R_2$$的矩阵为$$M_{R_1} \odot M_{R_2}$$
      - **例子**：
        - $$A = \begin{pmatrix} 1 & 0 & 1 \\ 0 & 1 & 1 \end{pmatrix}$$，$$B = \begin{pmatrix} 1 & 1 \\ 0 & 1 \\ 1 & 0 \end{pmatrix}$$
        - $$A \odot B = \begin{pmatrix} (1 \land 1) \lor (0 \land 0) \lor (1 \land 1) & (1 \land 1) \lor (0 \land 1) \lor (1 \land 0) \\ (0 \land 1) \lor (1 \land 0) \lor (1 \land 1) & (0 \land 1) \lor (1 \land 1) \lor (1 \land 0) \end{pmatrix}$$
        - $$= \begin{pmatrix} 1 \lor 0 \lor 1 & 1 \lor 0 \lor 0 \\ 0 \lor 0 \lor 1 & 0 \lor 1 \lor 0 \end{pmatrix} = \begin{pmatrix} 1 & 1 \\ 1 & 1 \end{pmatrix}$$
      - **性质**：
        - 布尔积满足结合律：$$(A \odot B) \odot C = A \odot (B \odot C)$$
        - 一般不满足交换律：$$A \odot B \neq B \odot A$$
        - 与普通矩阵乘法类似，但用$$\lor$$代替$$+$$，用$$\land$$代替$$\times$$
    - 优点：便于计算机处理和关系运算
  - **关系图：用有向图表示关系**
    - 用节点表示元素，用有向边表示关系
    - 如果$$\langle a, b \rangle \in R$$，则从节点a到节点b画一条有向边
    - 例如：关系R可表示为：$$1 \rightarrow 2 \rightarrow 3 \rightarrow 1$$
  - **特性描述法：用谓词公式描述关系**
    - 用逻辑公式描述关系的特征
    - 例如：$$ R = \{\langle x, y \rangle \mid x, y \in \mathbb{Z}, x < y\}$$ 表示整数上的小于关系
    - 例如：$$ R = \{\langle x, y \rangle \mid x, y \in \mathbb{R}, x^2 + y^2 = 1\}$$ 表示单位圆上的点
- 关系的运算
  - **关系的复合运算(Composition of Relations)**
    - **定义**：设$$R_1$$是从A到B的关系，$$R_2$$是从B到C的关系，则$$R_1$$与$$R_2$$的复合关系$$R_1 \circ R_2$$定义为：
      - $$R_1 \circ R_2 = \{\langle a, c \rangle \mid a \in A, c \in C, \exists b \in B (\langle a, b \rangle \in R_1 \land \langle b, c \rangle \in R_2)\}$$
    - **含义**：如果a通过$$R_1$$与某个b相关，且这个b通过$$R_2$$与c相关，则a通过复合关系与c相关
    - **例子**：
      - 设$$A = \{1, 2\}$$，$$B = \{a, b\}$$，$$C = \{x, y\}$$
      - $$R_1 = \{\langle 1, a \rangle, \langle 2, b \rangle\}$$
      - $$R_2 = \{\langle a, x \rangle, \langle b, y \rangle\}$$
      - 则$$R_1 \circ R_2 = \{\langle 1, x \rangle, \langle 2, y \rangle\}$$
    - **矩阵计算**：$$(M_{R_1 \circ R_2}) = M_{R_1} \odot M_{R_2}$$（布尔积）
    - **性质**：
      - **结合律**：$$(R_1 \circ R_2) \circ R_3 = R_1 \circ (R_2 \circ R_3)$$
      - **一般不满足交换律**：$$R_1 \circ R_2 \neq R_2 \circ R_1$$
      - **恒等关系的性质**：$$R \circ I_A = R$$，$$I_B \circ R = R$$
    - **关系的幂**：
      - $$R^1 = R$$
      - $$R^n = R^{n-1} \circ R$$（n > 1）
      - $$R^0 = I_A$$（A上的恒等关系）
  - **关系的逆运算(Inverse of Relations)**
    - **定义**：设R是从A到B的关系，则R的逆关系$$R^{-1}$$定义为：
      - $$R^{-1} = \{\langle b, a \rangle \mid \langle a, b \rangle \in R\}$$
    - **含义**：逆关系就是将原关系中所有序偶的顺序颠倒
    - **例子**：
      - 若$$R = \{\langle 1, a \rangle, \langle 2, b \rangle, \langle 3, a \rangle\}$$
      - 则$$R^{-1} = \{\langle a, 1 \rangle, \langle b, 2 \rangle, \langle a, 3 \rangle\}$$
    - **矩阵表示**：$$M_{R^{-1}} = (M_R)^T$$（矩阵转置）
    - **性质**：
      - $$(R^{-1})^{-1} = R$$
      - $$(R_1 \cup R_2)^{-1} = R_1^{-1} \cup R_2^{-1}$$
      - $$(R_1 \cap R_2)^{-1} = R_1^{-1} \cap R_2^{-1}$$
      - $$(R_1 \circ R_2)^{-1} = R_2^{-1} \circ R_1^{-1}$$（注意顺序颠倒）
      - $$I_A^{-1} = I_A$$（恒等关系的逆还是自己）
  - 关系的幂运算
    - **定义**：设R是集合A上的二元关系，则R的幂运算定义为：
      - $$R^0 = I_A$$（A上的恒等关系）
      - $$R^1 = R$$
      - $$R^2 = R \circ R$$
      - $$R^n = R^{n-1} \circ R$$（n ≥ 2）
    - **含义**：$$R^n$$表示通过关系R经过n步可以到达的所有序偶
      - $$R^2$$：如果$$\langle a, c \rangle \in R^2$$，则存在$$b$$使得$$aRb$$且$$bRc$$
      - $$R^3$$：如果$$\langle a, d \rangle \in R^3$$，则存在路径$$a \rightarrow b \rightarrow c \rightarrow d$$
    - **矩阵计算**：
      - $$M_{R^0} = I$$（单位矩阵）
      - $$M_{R^1} = M_R$$
      - $$M_{R^2} = M_R \odot M_R$$
      - $$M_{R^n} = M_R \odot M_{R^{n-1}}$$
    - **例子**：
      - 设$$A = \{1, 2, 3\}$$，$$R = \{\langle 1, 2 \rangle, \langle 2, 3 \rangle, \langle 3, 1 \rangle\}$$
      - $$R^0 = \{\langle 1, 1 \rangle, \langle 2, 2 \rangle, \langle 3, 3 \rangle\}$$
      - $$R^1 = \{\langle 1, 2 \rangle, \langle 2, 3 \rangle, \langle 3, 1 \rangle\}$$
      - $$R^2 = \{\langle 1, 3 \rangle, \langle 2, 1 \rangle, \langle 3, 2 \rangle\}$$
      - $$R^3 = \{\langle 1, 1 \rangle, \langle 2, 2 \rangle, \langle 3, 3 \rangle\} = R^0$$
    - **性质**：
      - **结合律**：$$R^m \circ R^n = R^{m+n}$$
      - **幂的幂**：$$(R^m)^n = R^{mn}$$
      - **分配律**：$$(R_1 \cup R_2)^n \supseteq R_1^n \cup R_2^n$$（一般不等）
      - **逆关系的幂**：$$(R^{-1})^n = (R^n)^{-1}$$
    - **传递闭包的定义**：
      - 关系R的传递闭包记作$$R^+$$，定义为：
      - $$R^+ = R^1 \cup R^2 \cup R^3 \cup ...$$
      - $$R^+ = \bigcup_{i=1}^{\infty} R^i$$
      - 含义：R的传递闭包包含所有通过R可以到达的序偶
    - **自反传递闭包**：
      - 记作$$R^*$$，定义为：
      - $$R^* = R^0 \cup R^+ = I_A \cup R^+$$
      - $$R^* = \bigcup_{i=0}^{\infty} R^i$$
      - 含义：既包含恒等关系，又包含传递闭包
    - **有限集上的计算**：
      - 对于有限集合A $$(\mid A \mid = n)$$，有：
      - $$R^+ = R^1 \cup R^2 \cup ... \cup R^n$$
      - 因为$$R^{n+1} \subseteq R^1 \cup R^2 \cup ... \cup R^n$$
      - 矩阵形式：$$M_{R^+} = M_R \lor M_{R^2} \lor ... \lor M_{R^n}$$
  - **其他关系运算**
    - **并运算**：$$R_1 \cup R_2 = \{\langle a, b \rangle \mid \langle a, b \rangle \in R_1 \text{ 或 } \langle a, b \rangle \in R_2\}$$
    - **交运算**：$$R_1 \cap R_2 = \{\langle a, b \rangle \mid \langle a, b \rangle \in R_1 \text{ 且 } \langle a, b \rangle \in R_2\}$$
    - **差运算**：$$R_1 - R_2 = \{\langle a, b \rangle \mid \langle a, b \rangle \in R_1 \text{ 且 } \langle a, b \rangle \notin R_2\}$$
    - **补运算**：$$\overline{R} = A \times B - R$$（相对于全关系的补集）
- 关系的性质
  - **自反性(Reflexivity)**
    - **定义**：设R是集合A上的二元关系，如果对于A中的每个元素a，都有$$\langle a, a \rangle \in R$$，则称R在A上是自反的
    - **符号表示**：$$\forall a \in A (aRa)$$
    - **矩阵特征**：关系矩阵的主对角线上的元素全为1
    - **图特征**：每个节点都有自环
    - **例子**：
      - 整数集上的"≤"关系是自反的（$$a \leq a$$）
      - 集合的包含关系"⊆"是自反的（$$A \subseteq A$$）
    - **反自反性**：如果对于A中的每个元素a，都有$$\langle a, a \rangle \notin R$$，则称R是反自反的
      - 例子：整数集上的"<"关系是反自反的
  - **对称性(Symmetry)**
    - **定义**：设R是集合A上的二元关系，如果对于A中的任意元素a, b，当$$\langle a, b \rangle \in R$$时，都有$$\langle b, a \rangle \in R$$，则称R在A上是对称的
    - **符号表示**：$$\forall a, b \in A (aRb \rightarrow bRa)$$
    - **矩阵特征**：关系矩阵是对称矩阵（$$M_R = M_R^T$$）
    - **图特征**：任意两个不同节点之间如果有边，则必须是双向边
    - **例子**：
      - 人群中的"兄弟姐妹"关系是对称的
      - 平面上的"垂直"关系是对称的
    - **反对称性**：如果对于A中的任意不同元素a, b，当$$\langle a, b \rangle \in R$$时，都有$$\langle b, a \rangle \notin R$$，则称R是反对称的
      - 更准确地：$$\forall a, b \in A (aRb \land bRa \rightarrow a = b)$$
      - 例子：整数集上的"≤"关系是反对称的
  - **传递性(Transitivity)**
    - **定义**：设R是集合A上的二元关系，如果对于A中的任意元素a, b, c，当$$\langle a, b \rangle \in R$$且$$\langle b, c \rangle \in R$$时，都有$$\langle a, c \rangle \in R$$，则称R在A上是传递的
    - **符号表示**：$$\forall a, b, c \in A (aRb \land bRc \rightarrow aRc)$$
    - **矩阵特征**：$$M_R \odot M_R \subseteq M_R$$（即$$M_{R^2} \leq M_R$$）
    - **图特征**：如果存在路径$$a \rightarrow b \rightarrow c$$，则必须存在直接边$$a \rightarrow c$$
    - **例子**：
      - 整数集上的"<"关系是传递的
      - 集合的包含关系"⊆"是传递的
      - 人群中的"祖先"关系是传递的
  - **关系性质的判定方法**
    - **矩阵方法**：
      - 自反性：主对角线全为1
      - 对称性：$$M_R = M_R^T$$
      - 传递性：$$M_R \odot M_R \subseteq M_R$$
    - **图方法**：
      - 自反性：每个节点都有自环
      - 对称性：所有边都是双向的
      - 传递性：任何间接路径都有对应的直接边
  - **性质的保持性**
    - **并运算**：
      - 自反性和对称性在并运算下保持
      - 传递性在并运算下不一定保持
    - **交运算**：
      - 所有三种性质在交运算下都保持
    - **复合运算**：
      - 传递性在复合运算下保持
      - 自反性和对称性在复合运算下不一定保持
    - **逆运算**：
      - 自反性和对称性在逆运算下保持
      - 反对称性在逆运算下保持
      - 传递性在逆运算下保持
  - **闭包运算**
    - **自反闭包**：$$r(R) = R \cup I_A$$
      - 最小的包含R的自反关系
    - **对称闭包**：$$s(R) = R \cup R^{-1}$$
      - 最小的包含R的对称关系
    - **传递闭包**：$$t(R) = R^+$$
      - 最小的包含R的传递关系
    - **性质**：
      - 闭包运算是幂等的：$$r(r(R)) = r(R)$$
      - 闭包运算满足单调性：若$$R_1 \subseteq R_2$$，则$$r(R_1) \subseteq r(R_2)$$
      - 不同闭包运算的顺序可能影响结果

### 特殊关系

- **等价关系(Equivalence Relation)**
  - **定义**：设R是集合A上的二元关系，如果R同时满足自反性、对称性和传递性，则称R为A上的等价关系
  - **等价关系的条件**：
    - **自反性**：$$\forall a \in A (aRa)$$
    - **对称性**：$$\forall a, b \in A (aRb \rightarrow bRa)$$
    - **传递性**：$$\forall a, b, c \in A (aRb \land bRc \rightarrow aRc)$$
  - **等价类(Equivalence Class)**
    - 设R是A上的等价关系，对于 $$a \in A$$，称集合 $$[a]_R = \{x \in A \mid xRa\}$$为a关于R的等价类
    - a称为该等价类的**代表元**
  - **等价关系的性质**：
    - **完全性**：$$A = \bigcup_{a \in A} [a]_R$$（所有等价类的并集等于A）
    - **互斥性**：对于 $$a, b \in A$$ ，要么 $$[a]_R = [b]_R$$ ，要么 $$[a]_R \cap [b]_R = \emptyset$$
    - **非空性**：每个等价类都非空
  - **商集(Quotient Set)**
    - A关于等价关系R的商集记作 $$A/R = \{[a]_R \mid  a \in A\}$$
    - 商集是所有不同等价类构成的集合
  - **例子**：
    - 整数集合上的模n同余关系： $$aRb \Leftrightarrow a \equiv b \pmod{n}$$
    - 平面上直线的平行关系
    - 集合的等势关系

- **偏序关系(Partial Order Relation)**
  - **定义**：设R是集合A上的二元关系，如果R同时满足自反性、反对称性和传递性，则称R为A上的偏序关系，记作"≤"
  - **偏序关系的条件**：
    - **自反性**：$$\forall a \in A (a \leq a)$$
    - **反对称性**：$$\forall a, b \in A (a \leq b \land b \leq a \rightarrow a = b)$$
    - **传递性**：$$\forall a, b, c \in A (a \leq b \land b \leq c \rightarrow a \leq c)$$
  - **偏序集(Poset)**：集合A连同其上的偏序关系≤构成偏序集，记作$$(A, \leq)$$
  - **可比性**：
    - 对于偏序集中的元素a, b，如果$$a \leq b$$或$$b \leq a$$，则称a与b**可比**
    - 如果既不是$$a \leq b$$也不是$$b \leq a$$，则称a与b**不可比**
  - **特殊元素**：
    - **最大元**：如果存在$$a \in A$$使得$$\forall x \in A (x \leq a)$$，则a为最大元
    - **最小元**：如果存在$$a \in A$$使得$$\forall x \in A (a \leq x)$$，则a为最小元
    - **极大元**：如果$$a \in A$$且不存在$$x \in A$$使得$$a < x$$，则a为极大元
    - **极小元**：如果$$a \in A$$且不存在$$x \in A$$使得$$x < a$$，则a为极小元
    - **上界**：对于子集$$B \subseteq A$$，如果$$\forall b \in B (b \leq a)$$，则a为B的上界
    - **下界**：对于子集$$B \subseteq A$$，如果$$\forall b \in B (a \leq b)$$，则a为B的下界
    - **上确界**：B的所有上界中的最小元称为B的上确界
    - **下确界**：B的所有下界中的最大元称为B的下确界
  - **例子**：
    - 实数集上的"≤"关系
    - 集合的包含关系"⊆"
    - 正整数的整除关系"|"

- **全序关系(Total Order Relation)**
  - **定义**：如果偏序关系满足**完全性**（任意两个元素都可比），则称为全序关系或线性序关系
  - **完全性**： $$\forall a, b \in A (a \leq b \text{ 或 } b \leq a)$$
  - **全序集**：具有全序关系的集合称为全序集或链
  - **例子**：
    - 实数集上的"≤"关系
    - 字典序关系
    - 自然数集上的"≤"关系

- **拟序关系(Strict Partial Order)**
  - **定义**：设R是集合A上的二元关系，如果R同时满足反自反性、反对称性和传递性，则称R为A上的拟序关系，记作"<"
  - **拟序的条件**：
    - **反自反性**：$$\forall a \in A (\neg(a < a))$$
    - **反对称性**：$$\forall a, b \in A (a < b \rightarrow \neg(b < a))$$
    - **传递性**：$$\forall a, b, c \in A (a < b \land b < c \rightarrow a < c)$$
  - **与偏序的关系**：
    - 从偏序≤可以得到严格偏序<：$$a < b \Leftrightarrow (a \leq b \land a \neq b)$$
    - 从严格偏序<可以得到偏序≤：$$a \leq b \Leftrightarrow (a < b \text{ 或 } a = b)$$
- **良序关系(Well Order Relation)**
  - **定义**：既是全序关系，又满足良序性的关系
  - **良序性**：每个非空子集都有最小元
  - **关系层次**：良序 ⊂ 全序 ⊂ 偏序
  - **例子**：
    - **良序**：自然数集$$(\mathbb{N}, \leq)$$，有限全序集
    - **全序非良序**：实数集$$(\mathbb{R}, \leq)$$，整数集$$(\mathbb{Z}, \leq)$$
  - **重要性质**：
    - 无无限递减序列
    - 支持数学归纳法
    - 每个集合都可以良序化（良序定理）
  - **应用**：程序终止性证明，递归算法分析
- **关系的应用**
  - **Hasse图**：用于表示偏序关系的简化有向图
    - 省略自环（自反性）
    - 省略传递边（传递性）
    - 边的方向用位置高低表示
  - 拓扑排序：将偏序集中的元素排列成线性序列

## 图论

### 图

- 图的基本概念
  - 图的定义
  - **图(Graph)**
    - **定义**：$$G = (V, E)$$，其中V是顶点集，E是边集
    - **顶点集**：$$V = \{v_1, v_2, ..., v_n\}$$，非空有限集合
    - **边集**：$$E = \{e_1, e_2, ..., e_m\}$$，每条边连接两个顶点

  - **边的类型**
    - **无向边(Undirected Edge)**
      - 表示为：$$e = \{u, v\}$$，其中$$u, v \in V$$
      - **无序性**：边$$\{u, v\}$$与$$\{v, u\}$$是同一条边
      - 连接两个顶点，没有方向性
    - **有向边(Directed Edge/Arc)**
      - 表示为：$$e = \langle u, v \rangle$$，从u指向v的边
      - **有序性**：边$$\langle u, v \rangle$$与$$\langle v, u \rangle$$是不同的边
      - u称为边的**起点**，v称为边的**终点**
  - 图的表示
    - **邻接矩阵表示(Adjacency Matrix)**
      - **定义**：用0-1矩阵表示图的顶点之间的邻接关系
      - **无向图**：$$A = (a_{ij})_{n \times n}$$，其中$$a_{ij} = 1$$当且仅当顶点$$v_i$$与$$v_j$$之间有边
      - **有向图**：$$a_{ij} = 1$$当且仅当存在从$$v_i$$到$$v_j$$的有向边
      - **性质**：
        - 无向图的邻接矩阵是对称的：$$a_{ij} = a_{ji}$$
        - 简单图的主对角线全为0（无自环）
        - 矩阵第i行（或第i列）中1的个数等于顶点$$v_i$$的度数
      - **例子**：设$$V = \{v_1, v_2, v_3\}$$，边集$$E = \{(v_1, v_2), (v_2, v_3), (v_1, v_3)\}$$
        - 邻接矩阵为：$$\begin{pmatrix} 0 & 1 & 1 \\ 1 & 0 & 1 \\ 1 & 1 & 0 \end{pmatrix}$$

    - **集合表示(Set Representation)**
      - **顶点集表示**：$$V = \{v_1, v_2, ..., v_n\}$$
      - **边集表示**：
        - 无向图：$$E = \{(v_i, v_j) \mid v_i, v_j \in V \text{且} v_i \text{与} v_j \text{相邻}\}$$
        - 有向图：$$E = \{\langle v_i, v_j \rangle \mid \text{存在从} v_i \text{到} v_j \text{的有向边}\}$$
      - **例子**：
        - $$V = \{1, 2, 3, 4\}$$
        - $$E = \{(1,2), (2,3), (3,4), (1,4)\}$$
  - 邻接点与邻接边
    - 在图G=<V,E>中，若两个节点u和v是边e的端点，则称u和v互为**邻接点**，称u与e互为关联
    - 具有公共端点的两条边称为**邻接边**
    - 两个端点相同的边称为**环**或自回路
    - 图中不予任何节点向邻接的节点称为**孤立节点**
    - 仅由孤立节点组成的图称为**零图**
    - 仅含一个节点的零图称为**平凡图**
    - 含有n个节点、m条边的图，称为**(n,m)图**
    - 含有n个节点的图称为**n阶图**
  - 图的分类
    - **按边的性质分类**
      - **简单图(Simple Graph)**
        - 无重边：任意两个顶点间最多有一条边
        - 无自环：没有连接顶点自身的边
        - 最常见的图类型
      - **多重图(Multigraph)**
        - 允许**重边(Multiple Edges)**：同一对顶点间可有多条边
        - 允许**自环(Self-loop)**：顶点可连接自身
        - 应用：交通网络（多条路线）
      - 伪图(Pseudograph)
        - 既允许重边又允许自环的图
        - 最一般的图结构

    - **按边的方向分类**
      - **无向图(Undirected Graph)**
        - 所有边都是无向边
        - 边表示为：$$\{u, v\}$$
        - 邻接矩阵对称
      - **有向图(Directed Graph)**
        - 所有边都是有向边（弧）
        - 边表示为：$$\langle u, v \rangle$$
        - 邻接矩阵一般不对称
      - **混合图(Mixed Graph)**
        - 既有有向边又有无向边
        - 较少使用
    - 按边或点是否含权分类
      - 赋权图
        - **边赋权图**：$$G = (V, E, W)$$，其中$$W: E \rightarrow \mathbb{R}$$
        - **点赋权图**：$$G = (V, E, W)$$，其中$$W: V \rightarrow \mathbb{R}$$
        - **点边都赋权图**：$$G = (V, E, W_V, W_E)$$
  - 图的操作
    - **删除边(Edge Deletion)**
      - **定义**：从图G中删除指定的边e，得到新图$$G - e$$
      - **表示**：$$G - e = (V, E - \{e\})$$
    - **删除顶点(Vertex Deletion)**
      - **定义**：从图G中删除顶点v及其所有关联的边，得到新图$$G - v$$
      - **表示**：$$G - v = (V - \{v\}, E')$$
        - 其中$$E' = \{e \in E \mid v \text{不是}e\text{的端点}\}$$
    - **边收缩(Edge Contraction)**
      - **定义**：将边e的两个端点合并为一个新顶点，删除原边e
      - **操作步骤**：
                1. 选择边$$e = (u, v)$$
                2. 创建新顶点$$w$$
                3. 将所有与u或v相连的边重新连接到w
                4. 删除顶点u、v和边e
      - **表示**：$$G / e$$表示对边e进行收缩后的图
    - **添加边(Edge Addition)**
      - **定义**：向图G中添加新的边e，得到新图$$G + e$$
      - **表示**：$$G + e = (V, E \cup \{e\})$$
  - 子图与补图
    - **子图(Subgraph)**
      - **定义**：图$$G' = (V', E')$$称为图$$G = (V, E)$$的子图，当且仅当$$V' \subseteq V$$且$$E' \subseteq E$$
      - **记号**：$$G' \subseteq G$$
      - **条件**：子图的每条边的端点都必须在子图的顶点集中
      - **例子**：
        - 原图：$$G = (\{1,2,3\}, \{(1,2), (2,3), (1,3)\})$$
        - 子图：$$G' = (\{1,2\}, \{(1,2)\})$$

    - **导出子图(Induced Subgraph)**
      - **定义**：由顶点子集$$V' \subseteq V$$及其间所有边构成的子图
      - **记号**：$$G[V']$$
      - **边集**：$$E' = \{(u,v) \in E \mid u,v \in V'\}$$
      - **特点**：包含指定顶点间的所有原有连接
      - **例子**：在完整三角形中选择两个顶点，导出子图只有一条边

    - **生成子图(Spanning Subgraph)**
      - **定义**：包含原图所有顶点的子图
      - **形式**：$$G' = (V, E')$$，其中$$E' \subseteq E$$
      - **特点**：顶点集不变，只删除部分边
      - **应用**：生成树就是特殊的生成子图

    - **补图(Complement Graph)**
      - **定义**：图$$G = (V, E)$$的补图$$\overline{G} = (V, \overline{E})$$
      - **边集**：$$\overline{E} = \{(u,v) \mid u,v \in V, u \neq v, (u,v) \notin E\}$$
      - **含义**：在同一顶点集上，包含原图中没有的所有可能边
      - **性质**：
        - $$G \cup \overline{G} = K_n$$（完全图）
        - $$G \cap \overline{G} = \emptyset$$
        - $$\overline{\overline{G}} = G$$
        - **如果原先图明确不包含自环，那么补图也不应包含**
      - **例子**：
        - 若$$G$$是路径图$$P_3$$：$$1-2-3$$
        - 则$$\overline{G}$$包含边$$(1,3)$$但不包含$$(1,2)$$和$$(2,3)$$

    - **完全图(Complete Graph)**
      - **定义**：任意两个不同顶点之间都有边相连的简单图
      - **记号**：n个顶点的完全图记作$$K_n$$
      - **边数**：$$\mid E \mid = \frac{n(n-1)}{2}$$
      - **性质**：
        - 每个顶点的度数为$$n-1$$
        - 是$$n-1$$正则图
        - 具有最大可能的边数
        - 完全图的补图是空图（零图）
  - 节点的度数与握手定理
    - **度数(Degree)**
      - **无向图中顶点的度数**：与顶点相连的边数，记作$$d(v)$$或$$\deg(v)$$
        - 自环对度数贡献2
        - 例如：顶点v连接3条边且有1个自环，则$$d(v) = 3 + 2 = 5$$
      - **有向图中顶点的度数**：
        - **入度(In-degree)**：指向顶点的边数，记作$$d^-(v)$$
        - **出度(Out-degree)**：从顶点发出的边数，记作$$d^+(v)$$
        - **总度数**：$$d(v) = d^-(v) + d^+(v)$$
      - **图的度数相关概念**：
        - **最小度数**：$$\delta(G) = \min_{v \in V} d(v)$$
        - **最大度数**：$$\Delta(G) = \max_{v \in V} d(v)$$
    - **握手定理(Handshaking Lemma)**
      - **定理表述**：在任何无向图中，所有顶点的度数之和等于边数的两倍
      - **公式**：$$\sum_{v \in V} d(v) = 2\mid E \mid$$
      - **证明思路**：每条边都有两个端点，所以在计算所有顶点度数之和时，每条边被计算了两次
      - **推论1**：图中度数为奇数的顶点个数必为偶数
        - 因为所有度数之和 $$2\mid E \mid$$ 是偶数，奇数个奇数相加为奇数，偶数个奇数相加为偶数
      - **推论2**：在任何图中，至少存在两个顶点具有相同的度数
        - 利用鸽笼原理：n个顶点的简单图中，度数范围为0到n-1，但不能同时有度数为0和n-1的顶点

    - **有向图的握手定理**
      - **入度之和等于出度之和**：$$\sum_{v \in V} d^-(v) = \sum_{v \in V} d^+(v) = \mid E \mid$$
      - **总度数之和**：$$\sum_{v \in V} d(v) = 2\mid E \mid$$
  - 图的同构
    - **同构的定义(Graph Isomorphism)**
      - **定义**：两个图$$G_1 = (V_1, E_1)$$和$$G_2 = (V_2, E_2)$$称为同构，当且仅当存在双射函数$$f: V_1 \rightarrow V_2$$，使得：
        - $$(u, v) \in E_1 \Leftrightarrow (f(u), f(v)) \in E_2$$
      - **记号**：$$G_1 \cong G_2$$
      - **含义**：两个图同构意味着它们具有完全相同的结构，只是顶点的标记不同
      - **双射函数f称为同构映射**

    - **同构的几何理解**
      - 同构的图可以通过重新标记顶点得到
      - 同构保持所有的结构性质：邻接关系、度数分布、路径长度等
      - 可以想象为将一个图的顶点重新命名得到另一个图

    - **同构不变量(Isomorphism Invariants)**
      - 同构的图必须具有相同的结构性质，这些性质称为同构不变量：
      - **基本不变量**：
        - **顶点数**：$$\mid V_1 \mid = \mid V_2 \mid$$
        - **边数**：$$\mid E_1 \mid = \mid E_2 \mid$$
        - **度数序列**：两图的度数序列必须相同
      - **高级不变量**：
        - **连通分量数**：连通分量的个数相同
        - **最短路径分布**：任意两点间最短路径长度的分布相同
        - **回路长度分布**：各种长度回路的数量相同
        - **直径**：图的直径（最长最短路径）相同
        - **围长**：最短回路的长度相同
- 通路、回路、连通性
  - **通路与回路**
    - **通路(Path)**
      - **定义**：顶点序列$$v_0, v_1, ..., v_k$$，其中相邻顶点间有边
      - **通路长度**：通路中边的数目
      - **简单通路**：除起终点外无重复顶点的通路
      - **基本通路**：无重复边的通路
      - **例子**：在图中从顶点1到顶点4的路径：$$1 \rightarrow 2 \rightarrow 3 \rightarrow 4$$

    - **回路(Circuit/Cycle)**
      - **定义**：起点和终点相同的通路
      - **简单回路**：除起终点外无重复顶点的回路
      - **基本回路**：无重复边的回路
      - **奇回路/偶回路**：长度为奇数/偶数的回路
      - **例子**：三角形图中的回路：$$1 \rightarrow 2 \rightarrow 3 \rightarrow 1$$
    - **可达性(Reachability)**

      - **定义**：在图中，如果存在从顶点u到顶点v的通路，则称v从u可达，记作 $$u \rightsquigarrow v$$

      - **可达性矩阵(Reachability Matrix)**
        - **定义**：n×n矩阵$$R = (r_{ij})$$，其中$$r_{ij} = 1$$当且仅当从顶点$$v_i$$到顶点$$v_j$$可达
        - **计算方法**：
          - 设邻接矩阵为A，则可达性矩阵$$R = (A \cup I)^*$$（传递闭包）
          - 具体：$$R = A^0 \cup A^1 \cup A^2 \cup ... \cup A^{n-1}$$
        - **性质**：
          - 无向图的可达性矩阵是对称的
          - 主对角线全为1（自反性）
          - 可达性矩阵的幂运算：$$R^k = R$$（k ≥ 1）
  - **无向图的连通性**
    - **连通图**：任意两顶点都连通的无向图
      - **定义**：图G称为连通图，当且仅当对于任意两个不同顶点u、v，都存在从u到v的通路
      - **等价条件**：
        - 图中任意两点都可达
        - 图只有一个连通分量
        - 从任一顶点出发都能到达所有其他顶点
      - **非连通图**：不是连通图的图，即存在至少一对顶点不连通

    - **连通分量**：极大连通子图
      - **定义**：图G的连通分量是G的一个极大连通子图
      - **极大性**：不能再添加G中的其他顶点使其仍然连通
      - **完全性**：连通分量包含了其顶点集合内所有可能的边
      - 图的连通分量数记作$$\omega(G)$$
      - **性质**：
        - 每个顶点都属于且仅属于一个连通分量
        - 连通分量的并集等于原图
        - 不同连通分量之间没有边相连
        - 连通图的连通分量数为1

    - **连通分支(Connected Component)**
      - **基于等价关系的定义**：图中可达关系R的每个等价类导出的子图称为连通分支
      - **等价关系性质**：可达关系R满足自反性、对称性、传递性
      - **唯一性**：等价关系的划分是唯一的，每个顶点只属于一个等价类
      - **极大性**：每个连通分支都是极大连通子图，不能再添加顶点保持连通性
      - **例子**：
        - 图$$G = (\{1,2,3,4,5\}, \{(1,2), (3,4)\})$$
        - 等价类：$$[1] = \{1,2\}$$，$$[3] = \{3,4\}$$，$$[5] = \{5\}$$
        - 连通分支：$$(\{1,2\}, \{(1,2)\})$$，$$(\{3,4\}, \{(3,4)\})$$，$$(\{5\}, \emptyset)$$
      - **性质**：
        - 连通分支的并集等于原图的顶点集
        - 不同连通分支之间的顶点不可达
        - 每个连通分支内的任意两顶点都可达
        - 连通分支的个数和大小取决于图的具体结构

    - **割点与桥**：
      - **割点(Cut Vertex/Articulation Point)**
        - **定义**：如果删除顶点v及其关联边后，图的连通分量数增加，则v为割点
        - **判定条件**：顶点v是割点当且仅当存在两个顶点u, w，它们之间的每条路径都经过v
        - **性质**：
          - 割点是连接不同部分的关键顶点
          - 删除割点会破坏图的连通性
          - 叶子顶点（度数为1）不可能是割点
          - 度数为0的孤立顶点不是割点
        - **算法**：使用深度优先搜索的Tarjan算法可以高效找出所有割点

      - **桥(Bridge/Cut Edge)**
        - **定义**：如果删除边e后，图的连通分量数增加，则e为桥
        - **判定条件**：边e是桥当且仅当e不在任何回路中
        - **性质**：
          - 桥是连接不同部分的关键边
          - 删除桥会破坏图的连通性
          - 树中的每条边都是桥
          - 桥的两个端点不一定是割点
        - **算法**：可以通过DFS或找回路的方法识别桥

    - **连通度(Connectivity)**
      - **顶点连通度(Vertex Connectivity)**：
        - **k-连通**：删除任意k-1个顶点后图仍连通
        - **连通度**：$$\kappa(G) = \max\{k \mid G\text{是}k\text{-连通的}\}$$
        - **计算**：$$\kappa(G)$$等于使图不连通所需删除的最少顶点数
        - **特殊情况**：
          - 完全图$$K_n$$的连通度：$$\kappa(K_n) = n-1$$
          - 树的连通度：$$\kappa(T) = 1$$（除了$$K_1$$和$$K_2$$）
          - 非连通图的连通度：$$\kappa(G) = 0$$
        - **性质**：连通度越高，图的鲁棒性越强

      - **边连通度(Edge Connectivity)**
        - **定义**：使图变为非连通所需删除的最少边数
        - **记号**：$$\lambda(G)$$
        - **k-边连通**：删除任意k-1条边后图仍连通
        - **边连通度计算**：$$\lambda(G) = \max\{k \mid G\text{是}k\text{-边连通的}\}$$
        - **例子**：
          - 树的边连通度为1（任何一条边都是桥）
          - 环图$$C_n$$的边连通度为2
          - 完全图$$K_n$$的边连通度为$$n-1$$
          - 星图的边连通度为1
        - **性质**：
          - $$\lambda(G) \leq \delta(G)$$（边连通度不超过最小度数）
          - $$\kappa(G) \leq \lambda(G) \leq \delta(G)$$（Whitney不等式）
          - 边连通度反映了网络的容错能力
        - **最小边割集**：
          - **定义**：删除后使图不连通的最小边集
          - **性质**：边连通度等于最小边割集的大小
- **有向图的连通性**
  - **强连通(Strong Connectivity)**
    - **定义**：在有向图中，如果任意两个顶点u和v都满足$$u \rightsquigarrow v$$且$$v \rightsquigarrow u$$，则称该图是强连通的
    - **等价条件**：
      - 从任一顶点出发都能到达所有其他顶点
      - 任意两顶点间都存在双向路径
      - 图中存在经过所有顶点的有向回路
    - **性质**：
      - 强连通图必须是连通的（忽略方向）
      - 强连通图不能有"出度为0"或"入度为0"的顶点（除非只有一个顶点）
    - **例子**：有向环$$1 \rightarrow 2 \rightarrow 3 \rightarrow 1$$是强连通的

  - **弱连通(Weak Connectivity)**
    - **定义**：如果将有向图的所有有向边都改为无向边后得到的无向图是连通的，则称原有向图是弱连通的
    - **判定方法**：
      - 忽略边的方向，将有向图看作无向图
      - 检查这个无向图是否连通
    - **性质**：
      - 强连通图必定是弱连通的
      - 弱连通不一定强连通
    - **例子**：有向路径$$1 \rightarrow 2 \rightarrow 3$$是弱连通但不强连通

  - **单向连通(Unilateral Connectivity)**
    - **定义**：如果对于有向图中的任意两个顶点u和v，至少有一个方向的路径存在（即$$u \rightsquigarrow v$$或$$v \rightsquigarrow u$$），则称该图是单向连通的
    - **性质**：
      - 强连通图必定是单向连通的
      - 单向连通图必定是弱连通的
      - 单向连通但非强连通的图中，任意两点间只有一个方向可达
    - **例子**：有向路径$$1 \rightarrow 2 \rightarrow 3 \rightarrow 4$$是单向连通的

  - **强连通分量(Strongly Connected Component, SCC)**
    - **定义**：有向图的强连通分量是图的一个极大强连通子图
    - **极大性**：
      - 分量内任意两顶点双向可达
      - 不能再添加其他顶点使其仍然强连通
    - **性质**：
      - 每个顶点都属于且仅属于一个强连通分量
      - 不同强连通分量之间最多只有单向连接
      - 强连通分量的个数反映图的"层次结构"
    - **缩点图**：
      - 将每个强连通分量看作一个顶点
      - 缩点图总是一个DAG（有向无环图）
    - **例子**：
      - 图：$$1 \rightarrow 2 \rightarrow 3 \rightarrow 1, 1 \rightarrow 4 \rightarrow 5$$
      - 强连通分量：$$\{1,2,3\}$$，$$\{4\}$$，$$\{5\}$$

  - **弱连通分量(Weakly Connected Component)**
    - **定义**：在有向图的基础无向图中的连通分量称为原有向图的弱连通分量
    - **计算方法**：
      - 将有向图转换为无向图（忽略边的方向）
      - 在无向图中找连通分量
    - **性质**：
      - 每个强连通分量都包含在某个弱连通分量中
      - 一个弱连通分量可能包含多个强连通分量
    - **应用**：分析有向图的整体连通结构

  - **单向连通分量(Unilateral Connected Component)**
    - **定义**：有向图中的极大单向连通子图
    - **性质**：
      - 分量内任意两顶点至少一个方向可达
      - 每个强连通分量都是单向连通分量
      - 单向连通分量之间的关系比强连通分量复杂
    - **计算**：相对复杂，需要特殊算法

  - **连通性层次关系**
    - **包含关系**：强连通 ⊂ 单向连通 ⊂ 弱连通
    - **具体含义**：
      - **强连通**：任意两点双向可达
      - **单向连通但非强连通**：任意两点至少一个方向可达，但存在某对顶点只能单向到达
      - **弱连通但非单向连通**：忽略方向后连通，但存在某对顶点双向都不可达
      - **非连通**：即使忽略方向也不连通
    - **判定优先级**：
            1. 首先判断是否强连通
            2. 如果不强连通，判断是否单向连通
            3. 如果不单向连通，判断是否弱连通
            4. 如果都不是，则非连通

  - **有向图连通性的性质**
    - **强连通图的性质**：
      - 任意顶点的出度和入度都大于0
      - 存在经过所有顶点的有向回路
      - 删除任意一个顶点后可能不再强连通
    - **DAG的性质**：
      - 没有有向回路
      - 可以进行拓扑排序
      - 至少有一个入度为0的顶点和一个出度为0的顶点
    - **缩点图的性质**：
      - 总是DAG
      - 反映原图的"层次结构"
      - 可以用于算法优化和问题分解

### 树

- **树**
  - **树的定义与性质**
    - **树的定义**
      - **基本定义**：连通且无回路的无向图称为树
      - **等价定义**：
        - n个顶点的连通图有n-1条边
        - 任意两顶点间有唯一简单路径
        - 连通图删除任一边后不连通
        - 无回路图添加任一边后恰有一个回路
        - 极小连通图（删除任一边后不连通）
        - 极大无回路图（添加任一边后产生回路）
    - **树的基本性质**
      - **边数公式**：$$ \mid E \mid = \mid V \mid - 1$$（边数等于顶点数减1）
      - **唯一路径性**：任意两顶点间有唯一简单路径
      - **叶子节点**：至少有两个度数为1的顶点（当n ≥ 2时）
      - **连通性**：删除任一边后图变成森林（两个连通分量）
      - **无回路性**：不包含任何长度≥3的回路

  - **生成树(Spanning Tree)**
    - **定义**：图G的生成树是包含G所有顶点的树
    - **形式化**：设$$G = (V, E)$$，其生成树$$T = (V, E')$$，其中$$E' \subseteq E$$且T是树
    - **存在条件**：
      - 连通图必有生成树
      - 非连通图没有生成树，但每个连通分量都有生成树
    - **生成树的性质**
      - **唯一性**：一般情况下，图的生成树不唯一
      - **边数**：生成树有n-1条边（n为顶点数）
      - **最大性**：不能再添加边而保持无回路
      - **最小性**：不能再删除边而保持连通
  - **最小生成树(Minimum Spanning Tree, MST)**
    - **定义**：加权连通图中权重和最小的生成树
    - **问题描述**：给定加权连通图$$G = (V, E, w)$$，找到生成树T使得$$w(T) = \sum_{e \in T} w(e)$$最小
    - **唯一性**：
      - 当所有边权重都不同时，MST唯一
      - 当存在相同权重的边时，可能有多个MST，但权重和相同
    - **基本性质**
      - **切割性质(Cut Property)**：设S是V的真子集，e是连接S和V-S的最小权重边，则e属于某个MST
      - **回路性质(Cycle Property)**：设C是图中任意回路，e是C中最大权重边，则e不属于任何MST
      - **唯一性条件**：如果图中每条边的权重都不同，则MST唯一
    - **Kruskal算法**
      - **算法思想**：按边权重递增顺序考虑边，选择不形成回路的边
      - **算法步骤**：
                1. 将所有边按权重递增排序
                2. 初始化空的边集合T
                3. 依次考虑每条边e = (u, v)：
                   - 如果u和v在不同连通分量中，则将e加入T
                   - 否则跳过此边
                4. 重复直到T有n-1条边
    - **Prim算法**
      - **算法思想**：从任一顶点开始，逐步扩展生成树
      - **算法步骤**：
                1. 选择任意起始顶点s，将s加入树顶点集合S
                2. 重复以下操作：
                   - 找到连接S和V-S的最小权重边e = (u, v)
                   - 将v加入S，将e加入生成树
                3. 直到S包含所有顶点
  - **无向树的特殊概念**
    - **森林(Forest)**
      - **定义**：无回路的无向图（树的集合）
      - **性质**：
        - 森林的每个连通分量都是树
        - n个顶点的森林最多有n条边
        - k个连通分量的森林恰好有n-k条边
      - **应用**：表示多个不相交的层次结构
- **根树**
  - **根树的定义与分类**
    - **根树(Rooted Tree)**
      - **定义**：指定了一个特殊顶点作为根的树
      - **表示**：$$(T, r)$$，其中T是树，r是根顶点
      - **方向性**：根树具有自然的层次结构和方向性
    - **根树的术语**
      - **根(Root)**：指定的特殊顶点，通常画在最上方
      - **父节点(Parent)**：顶点v的父节点是从根到v路径上v的前一个顶点
      - **子节点(Child)**：顶点v的子节点是以v为父节点的顶点
      - **兄弟节点(Sibling)**：具有相同父节点的顶点
      - **祖先(Ancestor)**：从根到顶点v路径上的所有顶点
      - **后代(Descendant)**：以v为根的子树中的所有顶点
      - **叶节点(Leaf)**：没有子节点的顶点
    - **根树的层次结构**
      - **层次(Level)**：从根到顶点的路径长度
      - **深度(Depth)**：顶点所在的层次（根的深度为0）
      - **高度(Height)**：
        - 顶点的高度：从该顶点到叶节点的最长路径长度
        - 树的高度：根节点的高度
      - **子树(Subtree)**：以某个顶点为根的树
    - **根树的分类**
      - **满树(Full Tree)**：每个内部节点都有相同数目的子节点
      - **完全树(Complete Tree)**：除最后一层外，其他层都是满的，且最后一层从左到右填充
      - **二叉树(Binary Tree)**：每个节点最多有两个子节点
        - **满二叉树**：每个内部节点都有两个子节点
        - **完全二叉树**：除最后一层外都是满的，最后一层从左到右填充
        - **平衡二叉树**：任意节点的左右子树高度差不超过1
      - **m叉树(m-ary Tree)**：每个节点最多有m个子节点
    - **根树的性质**
      - **节点数与边数**：n个节点的根树有n-1条边
      - **叶节点数**：满m叉树中，若有i个内部节点，则有(m-1)i+1个叶节点
      - **高度与节点数**：
        - 高度为h的满m叉树最多有$$\frac{m^{h+1}-1}{m-1}$$个节点
        - n个节点的完全m叉树的高度为$$\lfloor \log_m(n(m-1)+1) \rfloor$$

  - **根树的遍历**
    - **深度优先遍历(DFS)**
      - **前序遍历(Preorder)**
        - **顺序**：根 → 左子树 → 右子树
        - **递归定义**：
                    1. 访问根节点
                    2. 前序遍历左子树
                    3. 前序遍历右子树
        - **应用**：表达式树的前缀表示、目录结构遍历
      - **中序遍历(Inorder)**
        - **顺序**：左子树 → 根 → 右子树
        - **递归定义**：
                    1. 中序遍历左子树
                    2. 访问根节点
                    3. 中序遍历右子树
        - **应用**：二叉搜索树的有序输出、表达式树的中缀表示
        - **特性**：对于二叉搜索树，中序遍历得到有序序列
      - **后序遍历(Postorder)**
        - **顺序**：左子树 → 右子树 → 根
        - **递归定义**：
                    1. 后序遍历左子树
                    2. 后序遍历右子树
                    3. 访问根节点
        - **应用**：表达式树的后缀表示、计算目录大小、删除树
    - 广度优先遍历(BFS)
    - **遍历的应用**
      - **表达式树**：
        - 前序遍历 → 前缀表达式（波兰式）
        - 中序遍历 → 中缀表达式
        - 后序遍历 → 后缀表达式（逆波兰式）
  - **最优树与赫夫曼算法**
    - **最优二叉树问题**
      - **问题描述**：给定n个带权叶节点，构造一棵二叉树使得带权路径长度最小
      - **带权路径长度(WPL)**：$$WPL = \sum_{i=1}^{n} w_i \cdot l_i$$，其中$$w_i$$是权重，$$l_i$$是路径长度
      - **应用背景**：数据压缩、编码理论、决策树
    - **赫夫曼算法(Huffman Algorithm)**
      - **算法思想**：贪心算法，每次合并两个最小权重的子树
      - **算法步骤**：
                1. 将所有叶节点按权重放入优先队列（最小堆）
                2. 重复以下操作直到队列中只剩一个节点：
                   - 取出两个最小权重的节点
                   - 创建新的内部节点，权重为两者之和
                   - 将新节点放回队列
                3. 最后剩下的节点就是根节点
    - **赫夫曼编码**
      - **编码规则**：
        - 左子树编码为0，右子树编码为1（或相反）
        - 叶节点的编码就是从根到该叶节点的路径编码
      - **性质**：
        - **前缀性**：任何编码都不是另一个编码的前缀
        - **最优性**：在所有前缀编码中，赫夫曼编码的平均长度最短
        - **唯一解码性**：可以无歧义地解码
      - **平均编码长度**：$$L = \sum_{i=1}^{n} p_i \cdot l_i$$，其中$$p_i$$是字符概率，$$l_i$$是编码长度
    - **赫夫曼树的性质**
      - **最优性**：在所有可能的二叉树中，赫夫曼树的WPL最小
      - **满二叉树**：赫夫曼树是满二叉树（除叶节点外都有两个子节点）
      - **节点数**：n个叶节点的赫夫曼树有2n-1个节点
      - **构造唯一性**：在权重不同的情况下，赫夫曼树基本唯一（可能因合并顺序略有不同）

### 特殊图

- **欧拉图**
  - **定义**
    - **欧拉通路(Eulerian Path)**
      - **定义**：通过图中每条边恰好一次的通路
      - **起点和终点**：可以不同
      - **边的遍历**：每条边必须且只能经过一次
      - **顶点访问**：顶点可以重复访问
    - **欧拉回路(Eulerian Circuit)**
      - **定义**：通过图中每条边恰好一次且起点终点相同的回路
      - **闭合性**：起点和终点必须相同
      - **完整遍历**：遍历图中所有边
    - **欧拉图(Eulerian Graph)**
      - **定义**：存在欧拉回路的图称为欧拉图
      - 半欧拉图：存在欧拉通路但不存在欧拉回路的图
  - **判定**
    - **无向图的欧拉图判定定理**
      - **欧拉图的充要条件**：
        - 图是连通的
        - 所有顶点的度数都是偶数
      - 半欧拉图的充要条件(存在欧拉通路)：
        - 图是连通的
        - 恰好有两个度数为奇数的顶点
    - **有向图的欧拉图判定定理**
      - **有向欧拉图的充要条件**：
        - 图是强连通的
        - 每个顶点的入度等于出度
      - **有向半欧拉图的充要条件**：
        - 图是弱连通的
        - 要么所有顶点入度等于出度
        - 要么恰好有一个顶点出度比入度大1，一个顶点入度比出度大1，其余顶点入度等于出度
    - **构造算法**
      - **Fleury算法**
        - **算法思想**：逐步构造欧拉路径，避免过早断开图的连通性
        - **基本原则**：除非没有其他选择，否则不走桥边（割边）
        - **算法步骤**：
                    1. **起点选择**：
                       - 对于欧拉回路：从任意顶点开始
                       - 对于欧拉通路：从奇度顶点开始
                    2. **边的选择**：
                       - 在当前顶点的所有未访问边中
                       - 优先选择非桥边
                       - 只有当所有边都是桥边时，才选择桥边
                    3. **迭代过程**：
                       - 走过选定的边，将其标记为已访问
                       - 移动到边的另一端点
                       - 重复直到所有边都被访问
      - Hierholzer算法
        - 算法思想：构造回路并逐步合并
        - 算法步骤：
                    1. 从任意顶点开始构造回路（DFS方式）
                    2. 如果还有未访问的边，从已访问顶点中选择一个有未访问边的顶点
                    3. 从该顶点构造新回路
                    4. 将新回路插入原回路的适当位置
                    5. 重复直到所有边都被访问
        - 优势：
          - 时间复杂度更优
          - 实现相对简单
          - 不需要复杂的桥判定
- **哈密顿图**
  - **定义**
    - **哈密顿通路(Hamiltonian Path)**
      - **定义**：通过图中每个顶点恰好一次的通路
      - **顶点遍历**：每个顶点必须且只能访问一次
      - **边的使用**：不要求使用所有边
      - **起终点**：可以不同
    - **哈密顿回路(Hamiltonian Circuit)**
      - **定义**：通过图中每个顶点恰好一次且起点终点相同的回路
      - **闭合性**：必须回到起始顶点
      - **完整遍历**：访问所有顶点
    - **哈密顿图(Hamiltonian Graph)**
      - **定义**：存在哈密顿回路的图称为哈密顿图
      - **半哈密顿图**：存在哈密顿通路但不存在哈密顿回路的图
    - **与欧拉图的区别**
      - **欧拉图**：关注边的遍历，每条边恰好一次
      - **哈密顿图**：关注顶点的访问，每个顶点恰好一次
      - **复杂度差异**：欧拉图判定P问题，哈密顿图判定NP完全问题

  - **判定**
    - **必要条件**
      - **连通性**：哈密顿图必须是连通的
      - **度数条件**：删除任意k个顶点后，连通分量数不超过k
    - **充分条件**
      - **Dirac定理**：
        - 条件：n≥3，每个顶点度数≥n/2
        - 结论：图是哈密顿图
      - **Ore定理**：
        - 条件：n≥3，任意两个不相邻顶点度数之和≥n
        - 结论：图是哈密顿图(判定通路是为n-1即可)
    - **必要条件判定法**
      - **顶点删除法**：
        - 对于顶点集合S，删除S后的连通分量数记作c(G-S)
        - 必要条件：对于任意顶点集合S，c(G-S) ≤ |S|
        - 应用：通过找反例证明图不是哈密顿图
    - **特殊图类的哈密顿性**
      - **完全图K_n**：n≥3时都是哈密顿图
      - **完全二分图K_{m,n}**：m=n≥2时是哈密顿图
      - **轮图W_n**：n≥3时都是哈密顿图
      - **网格图**：某些特定尺寸的网格图是哈密顿图
  - **特殊问题**
    - [抄近路算法]()(P335)
    - [中国邮路问题](https://zhuanlan.zhihu.com/p/401982790)
- **偶图(二分图)**
  - **定义**
    - **二分图(Bipartite Graph)**
      - **定义**：顶点集可以分为两个不相交的子集，使得每条边的两个端点分别属于不同的子集
      - **数学表示**：$$G = (V_1 \cup V_2, E)$$，其中$$V_1 \cap V_2 = \emptyset$$，且$$\forall (u,v) \in E$$，有$$(u \in V_1 \land v \in V_2) \lor (u \in V_2 \land v \in V_1)$$
      - **别名**：也称为偶图、双分图
    - **完全二分图(Complete Bipartite Graph)**
      - **定义**：二分图中两个顶点子集间的每对顶点都有边相连
      - **记号**：$$K_{m,n}$$表示两部分分别有m和n个顶点的完全二分图
      - **边数**：$$ \mid E \mid = m \times n$$
      - **例子**：$$K_{3,2}$$表示一部分3个顶点，另一部分2个顶点，共6条边
    - **匹配相关概念**
      - **匹配(Matching)**：边集的子集，其中任意两条边都不共享顶点
      - **最大匹配**：边数最多的匹配
      - **完全匹配**：每个顶点都被匹配的匹配
      - **饱和**：在匹配中，被匹配的顶点称为饱和顶点
  - **判定**
    - **二分图判定定理**
      - **充要条件**：图是二分图当且仅当图中不包含奇长度的回路
      - **等价表述**：图是二分图当且仅当图是二着色的
    - **二分图的性质**
      - **度数关系**：在二分图中，两部分顶点的度数之和相等
        - $$\sum_{v \in V_1} d(v) = \sum_{v \in V_2} d(v) = \mid E \mid$$
      - **着色数**：二分图的色数最多为2
      - **独立集**：每个部分都是独立集（内部无边）
      - **最小顶点覆盖**：由König定理，最小顶点覆盖数等于最大匹配数
    - **霍尔定理(Hall's Theorem)**
      - **定理表述**：设 $$ G = (V_1 \cup V_2, E)$$是二分图，则G中存在饱和$$V_1$$的匹配当且仅当：
        - **霍尔条件**：对于 $$V_1$$的任意子集$$S$$，有  $$\mid N(S) \mid \geq \mid S \mid$$
        - 其中$$N(S) = \{v \in V_2 \mid \exists u \in S, (u,v) \in E\}$$是S的邻域
      - **几何理解**：
        - $$N(S)$$是S中所有顶点的邻居在$$V_2$$中的并集
        - 霍尔条件要求任何子集的邻居数量不少于子集本身的大小
      - **例子**：
        - 设$$V_1 = \{a, b, c\}$$，$$V_2 = \{1, 2, 3, 4\}$$
        - 邻接关系：a-{1,2}，b-{2,3}，c-{3,4}
        - 检查霍尔条件：
          - $$\mid N(\{a\})\mid  = \mid \{1,2\}\mid  = 2 \geq 1$$
          - $$\mid N(\{b\})\mid  = \mid \{2,3\}\mid  = 2 \geq 1$$
          - $$\mid N(\{c\})\mid  = \mid \{3,4\}\mid  = 2 \geq 1$$
          - $$\mid N(\{a,b\})\mid  = \mid \{1,2,3\}\mid  = 3 \geq 2$$
          - $$\mid N(\{a,c\})\mid  = \mid \{1,2,3,4\}\mid  = 4 \geq 2$$
          - $$\mid N(\{b,c\})\mid  = \mid \{2,3,4\}\mid  = 3 \geq 2$$
          - $$\mid N(\{a,b,c\})\mid  = \mid \{1,2,3,4\}\mid  = 4 \geq 3$$
        - 霍尔条件成立，存在完美匹配
    - **t条件(t-Condition)**
      - **定义**：对于二分图 $$G = (V_1 \cup V_2, E)$$ ，如果对于 $$V_1$$ 的任意子集S，都有 $$ \mid N(S) \mid  \geq \mid S \mid  - t$$ ，则称G满足t条件
      - **与霍尔定理的关系**：
        - 霍尔条件等价于0条件：$$\mid N(S)\mid  \geq \mid S\mid  - 0 = \mid S\mid $$
        - t条件是霍尔条件的推广，允许一定程度的"缺失"
      - **t条件的意义**：
        - **最大匹配大小**：如果G满足t条件，则G的最大匹配大小至少为 $$\mid V_1\mid  - t$$
        - **容错性**：t条件衡量了匹配问题的容错能力
        - **近似匹配**：当完美匹配不存在时，t条件给出了最好的近似结果
      - **定理**：二分图G满足t条件当且仅当G的最大匹配大小至少为 $$\max(0, \mid V_1\mid  - t)$$
      - **计算方法**：
        - **直接检验**：枚举$$V_1$$的所有子集，检查邻域条件
        - **最大流方法**：构造网络流模型，计算最大流
        - **匈牙利算法**：直接计算最大匹配，验证大小
      - **例子**：
        - 设$$V_1 = \{a, b, c, d\}$$，$$V_2 = \{1, 2, 3\}$$
        - 邻接关系：a-{1}，b-{1,2}，c-{2,3}，d-{3}
        - 检查不同的t条件：
          - **t=0（霍尔条件）**：$$N(\{a,d\}) = \{1,3\}$$，$$\mid \{1,3\}\mid  = 2 < 2 = \mid \{a,d\}\mid $$，不满足
          - **t=1**：对所有子集S，$$\mid N(S)\mid  \geq \mid S\mid  - 1$$，需要验证
          - 最大匹配大小为3，所以满足1条件
- **平面图**
  - **定义**
    - **平面图(Planar Graph)**
      - **定义**：能够画在平面上使得边只在顶点处相交的图
      - **平面嵌入**：图在平面上的一个具体画法称为平面嵌入
      - **非平面图**：无法在平面上画出而边不相交的图
    - **面(Face)**
      - **定义**：平面图的平面嵌入将平面分割成若干个区域，每个区域称为面
      - **内面**：有界的面称为内面
      - **外面**：无界的面称为外面（总是存在且唯一）
      - **面的边界**：围成面的边的集合
      - **面的度数**：围成面的边数（桥边被计算两次）
    - **平面图的表示**
      - **几何表示**：在平面上的实际画法
      - **组合表示**：不依赖于具体坐标的结构描述
      - **对偶图**：每个面对应一个顶点，相邻面对应的顶点间有边
  - **判定**
    - **欧拉公式(Euler's Formula)**
      - **公式**：对于连通平面图，$$V - E + F = 2$$
      - **其中**：V是顶点数，E是边数，F是面数
      - **推广**：对于有k个连通分量的平面图，$$V - E + F = k + 1$$
    - **必要条件**
      - **边数限制**：
        - 对于简单连通平面图：$$E \leq 3V - 6$$（V ≥ 3）
        - 对于简单连通无三角形平面图：$$E \leq 2V - 4$$（V ≥ 3）
      - **推导过程**：
        - 每个面至少有3条边界边
        - 每条边最多属于2个面的边界
        - 因此：$$3F \leq 2E$$
        - 结合欧拉公式：$$F = 2 - V + E$$
        - 得到：$$3(2 - V + E) \leq 2E$$
        - 化简：$$E \leq 3V - 6$$
    - **Kuratowski定理**
      - **定理内容**：图是平面图当且仅当它不包含$$K_5$$或$$K_{3,3}$$的细分
      - **细分(Subdivision)**：在边上插入度数为2的顶点得到的图
      - **$$K_5$$**：5个顶点的完全图
      - **$$K_{3,3}$$**：完全二分图
      - **历史意义**：完全刻画了平面图的结构

## 结语

- 本身离散我认为是非常有吸引力的一门学科，可惜它要考试qwq
- 希望这篇文章能帮到你哇，编写也花了我不少时间呢嘻嘻。
