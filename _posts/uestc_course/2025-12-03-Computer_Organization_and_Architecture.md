---
layout:     post
title:      "计算机组成原理PPT整理.25"
subtitle:   " \"Computer Organization and Architecture\""
date:       2025-12-3 20:00:00
author:     "LanZinYtt"
header-img: ""
catalog: true
tags:
    - Core_General_Education_Courses
---

# 计算机组成原理

## 第一章

## 第二章
### 关于非二进制补码编码及其运算
```java
Q: 
    4位十进制数的模运算系统，模等于[填空1]
    该运算系统中，9828+8072= [填空2]
    该模运算系统中，-1928表示为什么？
    则该模运算系统表示的范围是？
    负数的最高为是？正数的最高位是？
     
```
```java
A:
    10000(1e4)
    7900
    8072；-5000到4999；
    -10000/2到10000/2-1
    负数最高位为5，6，7，8，9，整数最高位为0，1，2，3，4
    
```
### 移码
- 移码实际上就是补码+偏移量 记住这一点

### 大端/小端编码
- 对于0x12345678这串4B的数据可以有大端小端两种模式
- 大端： 高地址| 78 | 56 | 34 | 12 |低地址 （高位字节排放在内存的低地址端）
- 小端： 高地址| 12 | 34 | 56 | 78 |低地址 
- 与大小端相关的还有一个概念，LSB和MSB，最小数位和最大数位，分别对应0x1中的0001的首位0和0x8中1000的末尾0

### **浮点数**
- 特别需要记忆的是32位IEEE标准下的浮点数**由1位符号位S，8位阶码E和23位尾数M构成**，所以也可以认为是24位的原码，并且阶码偏移量为127
- 表达浮点数范围（考虑隐藏位）：
    - 正数最大：| 0 | 11111110 | 11111111111111111111111 |  
    - = $(2-2^{-23})*2^{127}$（注意若阶码全1则表达无穷）
    - 正数规格化最小：| 0 | 00000001 | 00000000000000000000000 | 
    - = $1.0*2^{-126}$ 
    - 正数非规格化最小：	
| 0 | 00000000 | 00000000000000000000001 |
    - = $2^{-23}*2^{-126}$  (非规格化下阶码无论是多少指数均为-126)
- 对于常规浮点数（不考虑隐藏位，规格化定义为最高位为1）
    - 正数最大：| 0 | 11111111 | 11111111111111111111111 | 
    - = $(1-2^{-24})*2^{127}$ 
    - 正数规格化最小：| 0 | 00000000 | 10000000000000000000000 | 
    - = $2^{-1}*2^{-128}$ 

## 第三章

### 标志位
- **标志位的计算**(其中C指进位，F指结果)
    - 溢出标志OF：$OF=C_n \oplus C_{n-1}$
    - 符号标志SF：
    - $SF= F_{n-1}$
    - 零标志ZF=1当且仅当F=0；
    - 进位/借位标志CF：$CF=C_{out} \oplus  C_{in}$
- 根据标志位判断溢出
    - 无符号加溢出条件：CF=1
    - 带符号加溢出条件：OF=1
    
### 各编码加减运算
- 原码:
![alt text](/img/in-post/Computer_Organization_and_Architecture/Signed_binary_addition_and_subtraction.png)
- 补码:
![alt text](/img/in-post/Computer_Organization_and_Architecture/Shift_addition_and_subtraction.png)

### **乘法**
- 无符号整数乘法运算:
![alt text](/img/in-post/Computer_Organization_and_Architecture/Unsigned_integer_multiplication.png)
- **`原码乘法算法`**(包括二位布斯):
![alt text](/img/in-post/Computer_Organization_and_Architecture/Signed_Binary_Multiplication_Algorithm.png)
- **`补码乘法运算`**
![alt text](/img/in-post/Computer_Organization_and_Architecture/Two's_Complement_Multiplication_1.png)
![alt text](/img/in-post/Computer_Organization_and_Architecture/Two's_Complement_Multiplication_2.png)
- 除法（大概率不考）

### **浮点数运算**
- 运算规则
![alt text](/img/in-post/Computer_Organization_and_Architecture/Floating-point_calculation_method.png)