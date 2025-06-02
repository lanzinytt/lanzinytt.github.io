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
        - 例如：$+5 = [0101]_{SM}$，$-5 = [1101]_{SM}$
        - 范围：$-(2^{n-1}-1)$ 到 $+(2^{n-1}-1)$
    - Ones' Complement(反码)
        
    - **Twos' Complement**(补码)
## Logical Algebra

## Digital Circuit

## Combination

## Flip-Flop

## Synchronous Sequeential Logic Circuit

## Verilog Implementation of Logic Circuit

## Memory and Programmable Logic Device