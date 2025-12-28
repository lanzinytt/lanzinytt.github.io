---
layout: post
title: "数据结构与算法PPT记忆点整理.25"
subtitle: ' "Data Structures and Algorithms"'
date: 2025-12-27 17:00:00
author: "LanZinYtt"
header-img: ""
catalog: true
tags:
  - Computer_Science_Specialized_Courses
  - Principles_of_Computer_Composition
---

# 数据结构与算法

## 1.1 基本概念

- 算法是解决问题的方法。
- 计算机问题求解步骤：![alt text](/img/in-post/Data_Structures_and_Algorithms/Steps_for_Solving_Computer_Problems.png)
- 算法 + 数据结构 = 程序
- **算法的特征**
  - 输入（input）：算法有零个或多个输入量；
  - 输出（output）：算法至少产生一个输出量；
  - 确定性（definiteness）：算法的每一条指 令都有确切的定义，没有二义性；
  - 有穷性（finiteness）：算法必须总能在执行有限步之后终止。
- **程序与算法的比较**
  - 计算机程序是算法用某种程序语言的一个具体表示（实现）
  - 计算机程序是用来给计算机读的
  - 而算法是给人来读的，直接将算法输入计算机是不能运行的
  - 程序可以不满足算法的有穷性。
- 数据结构基本概念

  - **数据(Data)** ：是客观事物的符号表示。在计算机科学中指的是所有能输入到计算机中并被计算机程序处理的符号的总称。

  - **数据元素(Data Element)** ：是数据的基本单位，在程序中通常作为一个整体来进行考虑和处理。

  - 一个数据元素可由若干个**数据项(Data Item)**组成。数据项是数据的不可分割的最小单位。数据项是对客观事物某一方面特性的数据描述。

  - **数据对象(Data Object)**：是性质相同的数据元素的集合，是数据的一个子集。如字符集合 C={’A’,’B’, ‘C’,…} 。(**数据对象可以是有限的，也可以是无限的。**)

- 数据元素之间的逻辑结构
  - **集合**：结构中的数据元素除了“同属于一个集合”外，没有其它关系。
  - 线性结构：结构中的数据元素之间存在一对一的关系。
  - 树型结构：结构中的数据元素之间存在一对多的关系。
  - 图状结构：结构中的数据元素之间存在多对多的关系。
- 数据元素之间的物理结构
  - **顺序存储结构**：用数据元素在存储器中的相对位置来表示数据元素之间的逻辑结构(关系)。
  - **链式存储结构**：在每一个数据元素中增加一个存放另一个元素地址的指针(pointer)，用该指针来表示数据元素之间的逻辑结构(关系)。
- 数据结构的三个组成部分
  - 逻辑结构： 数据元素之间逻辑关系的描述
  - 存储结构： 数据元素在计算机中的存储及其 逻辑关系的表现称为数据的存储结构或物理结构。
  - 数据操作： 对数据要进行的运算。
- 抽象数据类型 (ADTs: Abstract Data Types)
  - 更高层次的数据抽象
  - 由用户定义，用以表示应用问题的数据模型
  - 由基本的数据类型组成, 并包括一组相关的操作
  - 可以通过固有的数据类型（如整型、实型、字符型等）来表示和实现。
  - ADT 的最重要的特点是抽象和信息隐蔽。**ADT 仅是一组逻辑特性描述， 与其在计算机内的表示和实现无关。**
  - ![alt text](/img/in-post/Data_Structures_and_Algorithms/ADTs.png)
  - ![alt text](/img/in-post/Data_Structures_and_Algorithms/Examples_of_ADTs.png)
## 1.2 算法复杂度分析
- 渐近分析的符号：
    - ![alt text](/img/in-post/Data_Structures_and_Algorithms/Symbols_of_asymptotic_analysis.png)
- **`渐近增长率比较的三种方法`**
    - 定义法：![alt text](/img/in-post/Data_Structures_and_Algorithms/Definition_method.png)
    - 极限法：![alt text](/img/in-post/Data_Structures_and_Algorithms/Limit_method.png)
    - 取对数法：![alt text](/img/in-post/Data_Structures_and_Algorithms/Logarithmic_method.png)
- **小结**：![alt text](/img/in-post/Data_Structures_and_Algorithms/Algorithm_complexity_analysis.png)
## 2.1 线性表
- 顺序存取法：![alt text](/img/in-post/Data_Structures_and_Algorithms/Sequential_access_method.png)
- **小结**：![alt text](/img/in-post/Data_Structures_and_Algorithms/Linear_list.png)
## 2.2 栈和队列
- **小结**：![alt text](/img/in-post/Data_Structures_and_Algorithms/Stack_and_queue.png)
## 2.3 多维数组
- **数组存储的行优先与列优先**：
  - 行优先：从右往左的顺序排布，如a[0][0]下一个位置是a[0][1];
  - 列优先：从左往右的顺序排布，如a[0][0]下一个位置是a[1][0];
![alt text](/img/in-post/Data_Structures_and_Algorithms/Row-major_and_column-major.png)
## 3.1 分治算法
- 分治法的复杂性分析(挺有启发性的):![alt text](/img/in-post/Data_Structures_and_Algorithms/Complexity_analysis_of_divide_and_conquer.png)
- **递归式的求解**
![alt text](/img/in-post/Data_Structures_and_Algorithms/Recursive_solution.png)
  - **主方法（主定理）**
  ![alt text](/img/in-post/Data_Structures_and_Algorithms/Main_method.png)
  ![alt text](/img/in-post/Data_Structures_and_Algorithms/Master_Theorem.png)
## 3.2 查找
- **顺序查找的性能分析**
  ![alt text](/img/in-post/Data_Structures_and_Algorithms/Performance_analysis_of_sequential_search.png)
- 索引查找一般指的是分块查找，在索引表中查找时需要高速查找，一般使用二分查找，因此索引表一般是顺序表
- 哈希表
  - **哈希函数**：
    ![alt text](/img/in-post/Data_Structures_and_Algorithms/Hash_function.png)
  - **`处理冲突的方法`**
    ![alt text](/img/in-post/Data_Structures_and_Algorithms/Ways_to_handle_conflicts.png)
  - 哈希表的查找效率分析
    ![alt text](/img/in-post/Data_Structures_and_Algorithms/Analysis_of_the_search_efficiency_of_hash_tables.png)
- **小结**：![alt text](/img/in-post/Data_Structures_and_Algorithms/Search.png)
# 3.3 排序
- 内部排序/外部排序
  - 若待排序记录都在内存中，称为内部排序；
  
  - 若待排序记录一部分在内存，一部分在外存，则称为外部排序。
  - 外部排序时，要将数据分批调入内存来排序，中间结果还要及时放入外存，显然外部排序要复杂得多。 
- 排序类型的介绍
  - 插入排序
    - 二分插入排序
    - 希尔排序
  - 冒泡排序
    - 鸡尾酒排序
  - 快速排序
  - 归并排序
  - 选择排序
    - 树形选择排序/锦标赛排序
  - 堆排序
  - 基数排序
  ![alt text](/img/in-post/Data_Structures_and_Algorithms/Comparison_of_sorting_algorithms.png)
- **小结**：![alt text](/img/in-post/Data_Structures_and_Algorithms/Sort.png)
## 4 树与二叉树
- 普通树是
- 特殊形态的二叉树：![alt text](/img/in-post/Data_Structures_and_Algorithms/Binary_trees_of_special_forms.png)
- 在完全二叉树中，最后一个非叶结点的编号为 ⌊n/2⌋（指向下取整）
  - 可以考虑其左子结点编号为 2i（如果存在）、其右子结点编号为 2i+1（如果存在）分析得。
- 由二叉树的前序序列+中序序列，或由其后序序列+中序序列均能唯一地确定一棵二叉树，但由前序序列+后序序列却不一定能唯一地确定一棵二叉树。 
- 树的存储结构
  - 孩子表示法：![alt text](/img/in-post/Data_Structures_and_Algorithms/Child_expression.png)
  - 双亲孩子表示法：![alt text](/img/in-post/Data_Structures_and_Algorithms/Parent-child_notation.png)
  - 孩子兄弟表示法：![alt text](/img/in-post/Data_Structures_and_Algorithms/Child_sibling_notation.png)
- 二叉树与树和森林之间的转换
  - 树转换为二叉树
    ![alt text](/img/in-post/Data_Structures_and_Algorithms/Convert_a_tree_into_a_binary_tree.png)
  - 二叉树转换为树
    ![alt text](/img/in-post/Data_Structures_and_Algorithms/Binary_tree_converted_to_tree.png)
  - 森林转换为二叉树
    ![alt text](/img/in-post/Data_Structures_and_Algorithms/Convert_the_forest_into_a_binary_tree.png)
  - 二叉树转换为森林
    ![alt text](/img/in-post/Data_Structures_and_Algorithms/Binary_tree_conversion_to_forest.png)
- 二叉树的应用
  ![alt text](/img/in-post/Data_Structures_and_Algorithms/Applications_of_binary_trees.png)
  - **`平衡二叉树的平衡调整`**
    - ![alt text](/img/in-post/Data_Structures_and_Algorithms/Step1.png)
    - ![alt text](/img/in-post/Data_Structures_and_Algorithms/Step2.png)
    - ![alt text](/img/in-post/Data_Structures_and_Algorithms/Step3.png)
    - ![alt text](/img/in-post/Data_Structures_and_Algorithms/Step4.png)
    - ![alt text](/img/in-post/Data_Structures_and_Algorithms/Step0.png)
  - **`霍夫曼树`**
    - 构造过程：![alt text](/img/in-post/Data_Structures_and_Algorithms/Huffman_tree_construction_process.png)
    - 霍夫曼编码：![alt text](/img/in-post/Data_Structures_and_Algorithms/Huffman_coding.png)
- **小结**：![alt text](/img/in-post/Data_Structures_and_Algorithms/Tree_and_Binary_Tree.png)
## 5 图与贪心算法
- 图的表示法
  - 邻接表
  - 邻接矩阵
  - 十字链表表示法：
    - ![alt text](/img/in-post/Data_Structures_and_Algorithms/Cross-linked_list_representation.png)
    - ![alt text](/img/in-post/Data_Structures_and_Algorithms/Cross-linked_list_exercises.png)
  - 邻接多重表表示法：
    - ![alt text](/img/in-post/Data_Structures_and_Algorithms/Adjacency_multi-list_representation.png)
- **`拓扑排序算法`**
  - ![alt text](/img/in-post/Data_Structures_and_Algorithms/Topological_sorting_algorithm.png)
- **`关键路径`**
  - 相关定义：![alt text](/img/in-post/Data_Structures_and_Algorithms/Definitions_related_to_the_critical_path.png)
  - 算法思想：
    - ![alt text](/img/in-post/Data_Structures_and_Algorithms/Critical_path_algorithm_concept.png)
    - ![alt text](/img/in-post/Data_Structures_and_Algorithms/Critical_path_method.png)
- **小结**：
![alt text](/img/in-post/Data_Structures_and_Algorithms/Graphs_and_Greedy_Algorithms_1.png)
![alt text](/img/in-post/Data_Structures_and_Algorithms/Graphs_and_Greedy_Algorithms_2.png)
## 6 动态规划
- **`动态规划求解`**
  - 带权重的活动安排问题：![alt text](/img/in-post/Data_Structures_and_Algorithms/Weighted_activity_schedule.png)
  - 最长公共子序列：![alt text](/img/in-post/Data_Structures_and_Algorithms/Longest_common_subsequence.png)
  - 矩阵连乘问题：![alt text](/img/in-post/Data_Structures_and_Algorithms/Matrix_chain_multiplication.png)
  - 序列对齐问题：![alt text](/img/in-post/Data_Structures_and_Algorithms/Sequence_alignment.png)
- 小结：![alt text](/img/in-post/Data_Structures_and_Algorithms/Dynamic_programming.png)