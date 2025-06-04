---
layout:     post
title:      "计算机组成原理-数字逻辑概论.25"
subtitle:   " \"Digital logic learning\""
date:       2025-06-02 23:00:00
author:     "LanZinYtt"
header-img: ""
catalog: true
tags:
    - Computer_Science_Specialized_Courses
    - Principles_of_Computer_Composition
---

<p id = "build"></p>

>计组虐我千百遍~

>在这里，我将梳理教材 *(数字逻辑概论[9787301343692])* 各个章节内容，尽可能得浅显易懂

# 计算机组成原理-数字逻辑概论

## Number System and Codes
1. Number Systems

    - 数制中我们常用的有十进制(**Dec**imal)、二进制(**B**inary)、十六进制(**Hex**adecimal)、八进制(**Oct**al)

2. Number Conversion

    - 在k进制下，数的实际大小$S_k=\sum_{i=-n}^{m-1} a_i \times k^i  (a_i \in \{0, 1, 2, \ldots, k-1\})$
    - 例如：$(2A.3)_{16} = 2 \times 16^1 + 10 \times 16^0 + 3 \times 16^{-1} = 32 + 10 + 0.1875 = (42.1875)_{10}$
    - **LSB (Least Significant Bit)** 最低有效位、**MSB (Most Significant Bit)** 最高有效位，在大端模式中MSB先传输，小端模式中LSB先传输

3. Signed Binary Numbers
    - Signed-Magnitude(原码)
        - 添加0或1在MSB前，表示正负
        - 其余位正常表示数值大小
        - 例如：$+5 = [0101]_{SM}$，$-5 = [1101]_{SM}$，$-0=[10..0]_{SM}$
        - 范围：$-(2^{n-1}-1)$ 到 $+(2^{n-1}-1)$
    - Ones' Complement(反码)
        - 当数值为负，所有位反转并在前添1，当数值为正，直接添0
        - 例如：$+5 = [0101]_{OC}$，$-5 = [1010]_{OC}$，$-0=[11..1]_{OC}$
        - 范围：$-(2^{n-1}-1)$ 到 $+(2^{n-1}-1)$
        - 优点：加减法运算统一，可直接由原码转换
        - 注意：存在两个零表示（+0和-0）
    - **Twos' Complement**(补码)
        - 当数值为负，先取反码再加1；当数值为正，直接添0
        - 例如：$+5 = [0101]_{TC}$，$-5 = [1011]_{TC}$，$+0=[00..0]_{TC}$
        - 范围：$-2^{n-1}$ 到 $+(2^{n-1}-1)$
        - 优点：只有一个零表示，加减法运算统一
        - 计算规律：负数的补码 = 原码取反 + 1，或者从右往左第一个1保持不变，其余位取反
4. Addition and Subtraction of Signed Binary Numbers
    - 对SM来说，计算可以先肉眼观察哪个绝对值更大，然后再让另一个与其做运算。
    - 对OC来说，加减法运算是统一的，都可以无论加减都转换成加，再做正常二进制加法，并把最高位循环进位加给最低位即可。
    - 对TC来说，加减法运算是统一的，直接做正常二进制加法，最简单。
5. Numerical Codes
    - Binary Coded Decimal(**BCD**)
        - 8421Code
        - Excess-3Code(余三码)**具有自补性**
        - 5421Code
        - **自补性**(Self-Complementing Property):编码满足： 编码(9-n) = 编码(n)的按位取反

    |  Dec   | 8421   |Excess-3| 5421   |
    |:------:|:------:|:------:|:------:|
    | 0      | 0000   | 0011   | 0000   |
    | 1      | 0001   | 0100   | 0001   |
    | 2      | 0010   | 0101   | 0010   |
    | 3      | 0011   | 0110   | 0011   |
    | 4      | 0100   | 0111   | 0100   |
    | 5      | 0101   | 1000   | 1000   |
    | 6      | 0110   | 1001   | 1001   |
    | 7      | 0111   | 1010   | 1010   |
    | 8      | 1000   | 1011   | 1011   |
    | 9      | 1001   | 1100   | 1100   |
    
    - Gray Code(格雷码)
        - 具有相邻数值只有一位编码不同的优越特性，有效避免多位跳变，提高系统可靠性。
        - **二进制转格雷码**：
            - $G_{n-1} = B_{n-1}$（最高位相同）
            - $G_i = B_{i+1} ⊕ B_i$（其他位为高位二进制与当前位异或）
    - Parity Code(奇偶校验码)
        - Odd Parity(奇校验)
            - 检验位设置使得整个码字中的1的个数为奇数
        - Even Parity(偶校验)
            - 校验位设置使得整个码字中的1的个数为偶数
        - 只能检测奇数个bit错误
## Logical Algebra
1. Three Basic Function of Logical Algebra
    - AND
    - OR
    - NOT
    - 过于简单不详述
2. Laws and Rules of Logical Algebra
    <details><summary>布尔代数基本定律</summary>

    - 交换律 (Commutative Laws)
            - $A + B = B + A$
            - $A · B = B · A$
    - 结合律 (Associative Laws)
        - $A + (B + C) = (A + B) + C$
        - $A · (B · C) = (A · B) · C$
    - 分配律 (Distributive Laws)
        - $A · (B + C) = A · B + A · C$
        - $A + (B · C) = (A + B) · (A + C)$
    - 互补律 (Complement Laws)
        - $A + \overline{A} = 1$
        - $A · \overline{A} = 0$
    - 同一律 (Identity Laws)
        - $A + 0 = A$
        - $A · 1 = A$
    - 零元律 (Null Laws)
        - $A + 1 = 1$
        - $A · 0 = 0$
    - 重复律 (Idempotent Laws)
        - $A + A = A$
        - $A · A = A$
    - 吸收律 (Absorption Laws)
        - $A + A · B = A$
        - $A · (A + B) = A$
    - 反演律 (Involution Law)
        - $\overline{\overline{A}} = A$    
    - **德摩根定律** (De Morgan's Laws)
        - $\overline{A+B} = \overline{A} · \overline{B}$
        - $\overline{A · B} = \overline{A} + \overline{B}$
    - **一致律** (Consensus Laws)
        - $A · B + \overline{A} · C + B · C = A · B + \overline{A} · C$
        - $(A + B) · (\overline{A} + C) · (B + C) = (A + B) · (\overline{A} + C)$
    - **冗余律** (Redundancy Laws)
        - $A + \overline{A} · B = A + B$
        - $A · (\overline{A} + B) = A · B$
    
    </details>
    
    - **Duality Rule** (对偶规则)
        - 定义：将布尔表达式中的 + 与 ·，0 与 1 互换，变量不变，得到对偶式
        - **重要性质**：如果一个布尔等式成立，其对偶式也必然成立
        - 示例：$F_1=A+B·C$，$F_2=(A+B)·(A+C)$ ，有$F_1^D=A·(B+C)=A·B+A·C=F_2^D$，故$F_1=F_2$ 
    - **Expansion Rule** (Shannon's Expansion Theorem)
        - **基本形式**：对于任意布尔函数 $F(x_1, x_2, \ldots, x_n)$，可以按照变量 $x_i$ 进行展开：
        
        $$F(x_1, x_2, \ldots, x_n) = x_i \cdot F(x_1, \ldots, x_{i-1}, 1, x_{i+1}, \ldots, x_n) + \overline{x_i} \cdot F(x_1, \ldots, x_{i-1}, 0, x_{i+1}, \ldots, x_n)$$

        - **递归展开**：可以对多个变量连续展开
        
        $$F(A,B,C) = A \cdot F(1,B,C) + \overline{A} \cdot F(0,B,C)$$
        $$= A \cdot [B \cdot F(1,1,C) + \overline{B} \cdot F(1,0,C)] + \overline{A} \cdot [B \cdot F(0,1,C) + \overline{B} \cdot F(0,0,C)]$$
    - 异或同或
        - 异或与同或满足分配律和交换律
        - 异或与同或的零一律很特殊
            - $A ⊕ 0 = A$
            - $A ⊕ 1 = \overline{A}$
            - $A ⊙ 0 = \overline{A}$
            - $A ⊙ 1 = A$
3. Function Transformation
    - Standard Froms 
    - **Canonical AND-OR**
        - **Minterm(极小项)**
            - 定义：n个变量的最小项是包含所有n个变量的乘积项，每个变量以原变量或反变量形式出现且仅出现一次
            - 特性：在2ⁿ种变量组合中，每个最小项仅在一种组合下为1，其余均为0

                | A | B | C |   Minterm  |
                |:-:|:-:|:-:|:----------:|
                | 0 | 0 | 0 | m₀ = Ā·B̄·C̄ |
                | 0 | 0 | 1 | m₁ = Ā·B̄·C |
                | 0 | 1 | 0 | m₂ = Ā·B·C̄ |
                | 0 | 1 | 1 | m₃ = Ā·B·C |
                | 1 | 0 | 0 | m₄ = A·B̄·C̄ |
                | 1 | 0 | 1 | m₅ = A·B̄·C |
                | 1 | 1 | 0 | m₆ = A·B·C̄ |
                | 1 | 1 | 1 | m₇ = A·B·C |
        - **Canonical OR-AND**
            - **Maxterm(极大项)**
                - 定义：n个变量的最大项是包含所有n个变量的加法项，每个变量以原变量或反变量形式出现且仅出现一次
                - 特性：在2ⁿ种变量组合中，每个最大项仅在一种组合下为0，其余均为1

                | A | B | C |  Maxterm   |
                |:-:|:-:|:-:|:----------:|
                | 0 | 0 | 0 | M₀ = A+B+C |
                | 0 | 0 | 1 | M₁ = A+B+C̄ |
                | 0 | 1 | 0 | M₂ = A+B̄+C |
                | 0 | 1 | 1 | M₃ = A+B̄+C̄ |
                | 1 | 0 | 0 | M₄ = Ā+B+C |
                | 1 | 0 | 1 | M₅ = Ā+B+C̄ |
                | 1 | 1 | 0 | M₆ = Ā+B̄+C |
                | 1 | 1 | 1 | M₇ = Ā+B̄+C̄ |
            - **互补关系**：Mᵢ = m̄ᵢ（第i个最大项等于第i个最小项的反）
            - **德摩根转换**：
                - 如果 F = Σm(1,3,5,7)，则 F = ΠM(0,2,4,6)
                - 即不在最小项列表中的项构成最大项列表
                - 因此这类题其实做真值表非常显然
    - **逻辑相邻**(Logical Adjacency):在布尔运算中，只有当两个形式中只有一个变量不同时才被称作相邻
    - <details><summary>例题</summary>

        Wirte the sum of Minterms of a function
        - $F(A,B,C)=\overline{(A\overline{B}+B\overline{C})\overline{AB}}$
        
        <details><summary> 解答过程</summary>
        
        - **Step 1: 化简原函数**
        - $$F(A,B,C) = \overline{(A\overline{B}+B\overline{C})\overline{AB}} \\ = \overline{(A\overline{B}+B\overline{C})} + \overline{\overline{AB}} \\ = \overline{(A\overline{B}+B\overline{C})} + AB \\ = \overline{A\overline{B}} \cdot \overline{B\overline{C}} + AB \\ = (\overline{A}+B) \cdot (\overline{B}+C) + AB
            $$
        - **Step 2: 展开分配律**
        $$= \overline{A}\overline{B} + \overline{A}C + B\overline{B} + BC + AB  \\ = \overline{A}\overline{B} + \overline{A}C + BC + AB$$
        - **Step 3: 补全变量（恢复缺失变量）**
        $\\ \overline{A}\overline{B} = \overline{A}\overline{B}(C + \overline{C}) = \overline{A}\overline{B}C + \overline{A}\overline{B}\overline{C} \\ \overline{A}C = \overline{A}C(B + \overline{B}) = \overline{A}BC + \overline{A}\overline{B}C \\ BC = BC(A + \overline{A}) = ABC + \overline{A}BC \\ AB = AB(C + \overline{C}) = ABC + AB\overline{C}$
        - **Step 4: 合并同类项**
        $$F = \overline{A}\overline{B}\overline{C} + \overline{A}\overline{B}C + \overline{A}BC + AB\overline{C} + ABC$$
        - **Step 5: 识别最小项**
        $ \\ \overline{A}\overline{B}\overline{C}$ → $000$ → $m_0 \\ \overline{A}\overline{B}C$ → $001$ → $m_1 \\ \overline{A}BC$ → $011$ → $m_3 \\ AB\overline{C}$ → $110$ → $m_6 \\ ABC$ → $111$ → $m_7$
        - **最终答案**：
        $$F = m_0 + m_1 + m_3 + m_6 + m_7 = \sum m(0,1,3,6,7)$$
        
        </details>    
    </details>

4. Function Simplification
    - **Simplest function**
        - 定义：项数最少，每一项中的变量也最少的表达形式
        - <details><summary>例题</summary>

            Write the simplification of AND-OR functions
            - $F(A,B,C,D,E) = AC + \overline{B}C + B\overline{D} + C\overline{D} + A(B + \overline{C}) + \overline{A}BC\overline{D} + A\overline{B}DE$
            
            <details><summary>答案</summary>
            
            $F=A+\overline{B}C+B\overline{D}$
            
            </details>
            
            **tips** ：对于化为最简OR-AND形式的题，可以采用对偶求得AND-OR形式再对偶求得。

        </details>
    - **K-Map**(卡诺图\烧烤图)
        - 卡诺图是一种图形化的布尔函数化简方法，通过格雷码排列的方式将逻辑相邻的最小项放在物理相邻的位置。
        - **4变量K-Map** (当变量大于5时难以构造，故一般只用到4变量)
            
            |     | CD=00 | CD=01 | CD=11 | CD=10 |
            |:---:|:-----:|:-----:|:-----:|:-----:|
            |AB=00|  m₀   |  m₁   |  m₃   |  m₂   |
            |AB=01|  m₄   |  m₅   |  m₇   |  m₆   |
            |AB=11| m₁₂   | m₁₃   | m₁₅   | m₁₄   |
            |AB=10|  m₈   |  m₉   | m₁₁   | m₁₀   |
        - **化简规则**
            - **基本原则**：$AB + A\overline{B} = A$（消去不同的变量）
            - **圈的要求**：
                - 圈的大小必须是2的幂次：1, 2, 4, 8, 16...
                - 圈必须是矩形（包括正方形）
                - 圈应尽可能大，以获得最大化简
                - 所有为1的格子都必须被圈覆盖
                - 圈可以重叠
                - 利用卡诺图的环形特性，边界可以相连
        - **Don't Care条件**
            - 用X或d表示，表示该状态下函数值无关紧要
            - 在化简时可以将X当作0或1使用，以获得最佳化简效果
            - 最终结果中X可以是0也可以是1
        - <details><summary>例题</summary>

            Use K-Map to simplify the following functions
            - $F(A,B,C,D) = \sum m(0,1,4,5,6,7,8,9,11,15)$
            
            <details><summary>解答过程</summary>
            
            - **Step 1: 画出4变量卡诺图并填入1**(对于M则是0)
            
            |     | CD=00 | CD=01 | CD=11 | CD=10 |
            |:---:|:-----:|:-----:|:-----:|:-----:|
            |AB=00|   1   |   1   |   0   |   0   |
            |AB=01|   1   |   1   |   1   |   1   |
            |AB=11|   0   |   0   |   1   |   0   |
            |AB=10|   1   |   1   |   1   |   0   |
            
            - **Step 2: 寻找可圈的矩形**
                - 圈1：m₀,m₁,m₄,m₅ (2×2矩形) → $\overline{A}\overline{C}$ 
                - 圈2：m₄,m₅,m₆,m₇ (1×4矩形) → $A\overline{B}$
                - 圈3：m₈,m₉,m₁₁ 需要与边界m₁₅连接 → $B\overline{C}\overline{D} + BC\overline{D} + B\overline{C}D + BCD$
                
            - **Step 3: 重新分析找最优解**
                - 圈1：m₀,m₁,m₄,m₅ → $\overline{C}\overline{D}$
                - 圈2：m₄,m₅,m₆,m₇ → $A\overline{B}$ 
                - 圈3：m₈,m₉ → $B\overline{A}\overline{C}$
                - 圈4：m₁₁,m₁₅ → $BCD$
                
            - **最终答案**：
            $$F = \overline{C}\overline{D} + A\overline{B} + B\overline{A}\overline{C} + BCD$$
            
            </details>
        </details>

## Digital Circuit
1. CMOS Transistor
    <div style="display: flex; align-items: flex-start; gap: 20px;">
    <div style="flex: 1;">
    
    - **NMOS晶体管 (N-channel Metal-Oxide-Semiconductor)**
        - **结构组成**：包含gate(栅极)、source(源极)、drain(漏极)三个端子
        - **工作原理**：通过栅极电压($V_{gs}$)控制source-drain之间的电阻($R_{ds}$)，起到逻辑控制开关的作用
        - **开关特性**：
            - 当$V_{gs} = 0$时：NMOS晶体管处于**OFF**状态，$R_{ds}$很大($> 10^6Ω$)
            - 当$V_{gs} > 0$(高电平)时：NMOS晶体管处于**ON**状态，$R_{ds}$显著降低
        - **控制规律**：$V_{gs}$增大 → $R_{ds}$减小 (Not point in - 非反向导通)
    
    </div>
    <div style="flex: 0 0 300px;">
    
    ![NMOS](/img/in-post/Digital_logic/NMOS_Transistor.png)
    
    </div>
    </div>
    
    <div style="display: flex; align-items: flex-start; gap: 20px; margin-top: 20px;">
    <div style="flex: 1;">
    
    - **PMOS晶体管 (P-channel Metal-Oxide-Semiconductor)**
        - **结构组成**：同样包含gate(栅极)、source(源极)、drain(漏极)三个端子
        - **工作原理**：与NMOS相反，通过栅极电压($V_{gs}$)反向控制source-drain之间的电阻
        - **开关特性**：
            - 当$V_{gs} = 0$时：PMOS晶体管处于**OFF**状态，$R_{ds}$很大
            - 当$V_{gs} < 0$(低电平)时：PMOS晶体管处于**ON**状态，$R_{ds}$显著降低
        - **控制规律**：$V_{gs}$减小 → $R_{ds}$减小 (Point in - 反向导通)
    
    </div>
    <div style="flex: 0 0 300px;">
    
    ![PMOS](/img/in-post/Digital_logic/PMOS_Transistor.png)
    
    </div>
    </div>
    **CMOS技术优势**
    - **互补特性**：NMOS和PMOS的导通条件互补，可构成完整的逻辑门电路
    - **低功耗**：静态时总有一个晶体管处于截止状态，几乎无静态功耗
    - **高集成度**：晶体管可以做得很小，适合大规模集成电路
    - **逻辑完备性**：可以实现所有基本逻辑运算(AND, OR, NOT)
2. CMOS Gate

3. Electrical Characteristics

## Combination

## Flip-Flop

## Synchronous Sequeential Logic Circuit

## Verilog Implementation of Logic Circuit

## Memory and Programmable Logic Device