---
layout:     post
title:      "计算机组成原理-Verilog.25"
subtitle:   " \"Verilog learning\""
date:       2025-06-02 9:00:00
author:     "LanZinYtt"
header-img: ""
catalog: true
tags:
    - Computer_Science_Specialized_Courses
    - Principles_of_Computer_Composition
---

<p id = "build"></p>

>计组虐我千百遍~

>在这里我将又示例大概的讲解一些verilog关键语法，希望能起到梳理作用

# 计算机组成原理-Verilog

- 实际上未来就业时可能并用不上这类**硬件描述语言**，但是确实能帮我们更好的理解计算机较底层的一些编排原理。
- 先来一段代码示例：

```verilog

//module和endmodule闭合，这里模块可以是电路单元也可以是测试单元
module example(
    input wire a,b,c,   //这里有时会忽略wire，缺省时默认是wire
    output wire y   //input或output不可省略，必须声明
);
assign y = (~a & ~b & ~c);    //数据流型
endmodule

```

### 硬件结构描述方式

这里不得不提到三种表述硬件结构的描述方式

1. 结构型：最接近实际硬件结构的描述方式，不易描述功能稍微复杂的电路。常用于实例化语句。

```verilog

module simple(
    a,b,c,d
);
input a,b,c;
output d;   //input或output可以延后定义
wire w1,w2,w3;

and(w1,a,b); //and 与门
not(w3,c);  //not 非门
and(w2,a,w3);
nor(d,w1,w2);// nor 或非门 还有nand 与非门 xor 异或门

/* 值得注意的是：
    not [元件名](output,input);
    这里元件名可省缺，类似于C++中结构体
*/
endmoudle

```

1. 数据流：能比较直观地表达底层的逻辑行为，使用的语句多为和硬件行为一致的并行语句，也只适用于小规模的电路设计。

```verilog

module simple(
    a,b,c,d
);
input a,b,c;
output d;

assign d=~((a & b) | (a & ~c));
/*  assign是连续赋值关键字，只要右表达式发生变化，左侧立即更新
    并且assign是并行瞬时执行，因此一般用在组合逻辑而不用于时序逻辑
    
    tips：
    1.assign只能赋值驱动wire类型
    2.一个wire只能被一个assign驱动
    3.不能在always块内使用assign
    4.配套有deassign可以取消连续赋值
*/
endmodule

```

1. 行为级：更加抽象，适合规模大些的电路设计。串行语句可以是其载体。

```verilog

module simple(
    a,b,c,d
);
input a,b,c;
output d;

reg d; //always只允许reg型在语块内被赋值

always @(a or b or c)begin  //begin和end相当于{ }，同理的，当always、if等后面只跟一条语句，可以省略begin和end
    d=~((a & b) | (a & ~c));
end
/*
    always是行为级建模的关键语句
    always @()中可以由下列敏感信号触发
    1. a,b,c    电平
    2. posedge/negedge  clk 时钟上升/下降沿
    3. *    自动敏感列表
    另外，由于always块于块之间是并行的，所以我们得避免赋值的竞争
*/
endmodule

```

### 数字逻辑电路的设计步骤

这里以7.1(1)为例：

题目描述：
7.1 Implement the full adder of two 1-bit binary numbers in Verilog.

(1)Use the dataflow level description to implement the logic functions of both the sum and the carry for the higher-big.

1. 根据问题的描述画出真值表

| A | B | $C_{in}$ |  S  | $C_{out}$ |
|:-:|:-:|:--------:|:---:|:---------:|
| 0 | 0 |    0     |  0  |     0     |
| 0 | 0 |    1     |  1  |     0     |
| 0 | 1 |    0     |  1  |     0     |
| 0 | 1 |    1     |  0  |     1     |
| 1 | 0 |    0     |  1  |     0     |
| 1 | 0 |    1     |  0  |     1     |
| 1 | 1 |    0     |  0  |     1     |
| 1 | 1 |    1     |  1  |     1     |

1. 化简，得到信号逻辑表达式

- $S = A \oplus B \oplus C_{in}$
- $C_{out} = A·B + A·C_{in} + B·C_{in}$

1. 根据逻辑表达式画出电路图(指定用verilog时用代码描述就行)

```verilog

// 1位全加器 - 数据流级描述
module full_adder_dataflow(
    input wire A, B, Cin,           // 两个加数和进位输入
    output wire S, Cout           // 和输出和进位输出
);

// 根据逻辑表达式实现
assign S = A ^ B ^ Cin;                        // S = A ⊕ B ⊕ Cin
assign Cout = (A & B) | (A & Cin) | (B & Cin);   // Cout = A·B + A·Cin + B·Cin

endmodule

```

1. 搭建电路，验证功能
