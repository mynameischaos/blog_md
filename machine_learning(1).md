---
title: 机器学习——读书笔记1
date: 2016-10-13 12:09:00 
tags: machine learning
categories: machine learning
---

书名：《机器学习》

作者： 周志华

### 第1章 绪论

1. 什么是机器学习 ？

	机器学习是这样一门学科，它致力于研究如何通过计算的手段，利用经验来改善系统自身的性能。在计算机系统中，“经验”通常是以“数据”形式存在，因此，机器学习就是从数据中产生“模型”(model)的算法， 即“学习算法”。数据作为输入，机器学习算法处理后得到输出是模型。当新的数据输入时，模型会做出相应的判断，得到相应的输出。
	
	[Mitchell, 1997］给出了定义：A computer program is said to learn from **experience E** with respect to some class of **tasks T** and **performance measure P**, if its performance at tasks in T, as measured by P, improves with experience E.(假设用P来评估计算机程序在某任务类T上的性能，若一个程序通过利用经验E在T中任务上获得了性能改善，则我们就说关于T和P，该程序对E进行了学习。)

2. 基本术语
	
	数据集、样本（示例）、属性（特征）、属性值、属性空间、样本空间、特征向量、标记空间（输出空间）、分类、回归、聚类、簇、监督学习、无监督学习、泛化、独立同分布。

3. 假设空间

	**归纳：**从特殊到一般的“泛化”过程，即从具体的事实归结出一般性规律。

	**演绎：**从一般到特殊的“特化”过程，即从基础原理推演出具体情况。

	”从样例中学习”显然是一个归纳的过程，因此也称“归纳学习”（inductive learning）.
	
	**假设空间：**所有假设（可能取值）组成的空间，称为假设空间。

	**版本空间：**存在一个与训练集一致的“假设集合”，称为版本空间。	
4. 归纳偏好

	**归纳偏好：**机器学习算法在学习过程中对某种类型假设的偏好。
	
	**奥卡姆剃刀(Occam's razor)：**是一种常用的、自然科学研究中最基本的原则，即“若有多个假设与观察一致，则选择最简单的那个”
	
	**没有免费的午餐(No Free Lunch Theorem)定理：**无论一个算法在解决一个问题的时候多聪明、一个算法多笨，但是他们的期望性都是相同的。期望性指的是算法运用于所有问题所得到的误差总和。 寓意就是：空谈“什么学习算法更好”毫无意义，因为若考虑所有潜在的问题，则所有学习算法都一样好。要谈学习算法的相对优劣，必须要针对具体的学习问题。
	
5. 发展历程



