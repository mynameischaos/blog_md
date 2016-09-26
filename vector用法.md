---
title: C++ STL之vector用法总结
date: 2016-09-25 22:44:00
tags: STL
categories: STL
---

### 介绍

1. vector是表示可变大小数组的序列容器。
2. 就像数组一样，vector也采用的连续存储空间来存储元素。也就是意味着可以采用下标对vector的元素进行访问，和数组一样高效。但是又不像数组，它的大小是可以动态改变的，而且它的大小会被容器自动处理。
3. 本质讲，vector使用动态分配数组来存储它的元素。当新元素插入时候，这个数组需要被重新分配大小为了增加存储空间。其做法是，分配一个新的数组，然后将全部元素移到这个数组。就时间而言，这是一个相对代价高的任务，因为每当一个新的元素加入到容器的时候，vector并不会每次都重新分配大小。
4. vector分配空间策略：vector会分配一些额外的空间以适应可能的增长，因为存储空间比实际需要的存储空间更大。不同的库采用不同的策略权衡空间的使用和重新分配。但是无论如何，重新分配都应该是对数增长的间隔大小，以至于在末尾插入一个元素的时候是在常数时间的复杂度完成的。
5. 因此，vector占用了更多的存储空间，为了获得管理存储空间的能力，并且以一种有效的方式动态增长。
6. 与其它动态序列容器相比（deques, lists and forward_lists）， vector在访问元素的时候更加高效，在末尾添加和删除元素相对高效。对于其它不在末尾的删除和插入操作，效率更低。比起lists和forward_lists统一的迭代器和引用更好。

### 用法

**1. 头文件**  

```C++
#include<vector>
```

**2. vector声明及初始化**

```C++
vector<int> vec;		//声明一个int型向量
vector<int> vec(5);		//声明一个初始大小为5的int向量
vector<int> vec(10, 1);	//声明一个初始大小为10且值都是1的向量
vector<int> vec(tmp);	//声明并用tmp向量初始化vec向量
vector<int> tmp(vec.begin(), vec.begin() + 3);	//用向量vec的第0个到第2个值初始化tmp
int arr[5] = {1, 2, 3, 4, 5};	
vector<int> vec(arr, arr + 5);		//将arr数组的元素用于初始化vec向量
//说明：当然不包括arr[4]元素，末尾指针都是指结束元素的下一个元素，
//这个主要是为了和vec.end()指针统一。
vector<int> vec(&arr[1], &arr[4]); //将arr[1]~arr[4]范围内的元素作为vec的初始值
```

**3. vector基本操作** 

(1). 容量  

* 向量大小： vec.size();
* 向量最大容量： vec.max_size();
* 更改向量大小： vec.resize();
* 向量真实大小： vec.capacity();
* 向量判空： vec.empty();
* 减少向量大小到满足元素所占存储空间的大小： vec.shrink_to_fit();  //[shrink_to_fit](http://www.cplusplus.com/reference/vector/vector/shrink_to_fit/)

(2). 修改

* 多个元素赋值： vec.assign(); //类似于初始化时用数组进行赋值
* 末尾添加元素： vec.push_back();
* 末尾删除元素： vec.pop_back();
* 任意位置插入元素： vec.insert();
* 任意位置删除元素： vec.erase();
* 交换两个向量的元素： vec.swap();
* 清空向量元素： vec.clear();

(3)迭代器

* 开始指针：vec.begin();
* 末尾指针：vec.end(); //指向最后一个元素的下一个位置
* 指向常量的开始指针： vec.cbegin(); //意思就是不能通过这个指针来修改所指的内容，但还是可以通过其他方式修改的，而且指针也是可以移动的。
* 指向常量的末尾指针： vec.cend();

(4)元素的访问

* 下标访问： vec[1];  //并不会检查是否越界
* at方法访问： vec.at(1); //以上两者的区别就是at会检查是否越界，是则抛出out of range异常
* 访问第一个元素： vec.front();
* 访问最后一个元素： vec.back();
* 返回一个指针： int* p  = vec.data(); //可行的原因在于vector在内存中就是一个连续存储的数组，所以可以返回一个指针指向这个数组。这是是C++11的特性。


(4)算法

* 遍历元素

```C++
vector<int>::iterator it;
for (it = vec.begin(); it != vec.end(); it++)
    cout << *it << endl;
//或者
for (size_t i = 0; i < vec.size(); i++) {
	cout << vec.at(i) << endl;
}
```

* 元素翻转  

```C++
#include <algorithm>
reverse(vec.begin(), vec.end());
```

* 元素排序

```bash
#include <algorithm>
sort(vec.begin(), vec.end()); //采用的是从小到大的排序
//如果想从大到小排序，可以采用上面反转函数，也可以采用下面方法:
bool Comp(const int& a, const int& b) {
	return a > b;
}
sort(vec.begin(), vec.end(), Comp);
``` 

参考文献：  
[vector官网](http://www.cplusplus.com/reference/vector/vector/)
[博客园vector博客](http://www.cnblogs.com/wang7/archive/2012/04/27/2474138.html)





