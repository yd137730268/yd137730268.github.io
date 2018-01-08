---  
layout: post  
title: algorithm  
date: 2018-01-08  
categories: blog  
tags: [Java]  
description: algorithm  
  
---  

--From ： 算法 第四版
 
1. 基础 
	1.1 基础编程模型
		1) 数组
		2) 二分查找 : log(n), 暴力遍历 : n
	1.2 数据抽象
	1.3 背包队列和栈
		1) 链表
		2) 双栈算术表达式求值 : 对没有省略括号的表达式，依次入栈，遇到右括号求出栈顶值，再入栈，最后得出所有值
	1.4 算法分析
		1) 时间
		2) 内存 : 对象，链表，数组，字符串等
2. 排序
	2.1 初级排序
		1) 选择排序 : 按顺序依次选出，n^2/2
		2) 插入排序 : 一次遍历并进行插入排序，n^2/2
		3) 希尔排序 : 间隔为d插入排序，缩小间隔继续排序,n*log2n
	2.2 归并排序 : 分治法拆分成两个部分递归排序，在合并在一起 (java.util.Arrays.legacyMergeSort(T[] a, Comparator<? super T> c))
	2.3 快速排序 : 选第一个元素为标记，一轮后，大的在右边，小的在左边，分为两部分继续排序
		1) 普通快速排序
		2) 改进的快速排序 : 在一轮后进行递归时，会忽略和标记元素相同的元素，在相同元素较多的时候比普通快排快速 (java.util.DualPivotQuicksort.sort(int[] a, int left, int right, int[] work, int workBase, int workLen))
	2.4 优先队列 : (java.util.PriorityQueue<E>)
		1) 堆排序 : 堆排序最大元素(N/2-1)，交换到末尾，继续重复操作
3. 查找
	3.1 符号表 ：键-值
	3.2 二叉查找树 : 二叉查找树
	3.3 平衡查找树 : 红黑树
	3.4 散列表 : hashMap
4. 图
	
5. 字符串

6. Other : 
