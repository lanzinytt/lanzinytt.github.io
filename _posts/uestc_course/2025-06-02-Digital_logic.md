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

## Digital Circuit

## Combination

## Flip-Flop

## Synchronous Sequeential Logic Circuit

## Verilog Implementation of Logic Circuit

## Memory and Programmable Logic Device