---
layout:     post   				    # 使用的布局（不需要改）
title:      数据结构（一）				# 标题 
subtitle:   单向链表 #副标题
date:       2019-02-14 				# 时间
author:     BY 	wangjian					# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - 数据结构
---

## 今天是情人节
> 单向链表

本篇博文主要是带大家了解一下数据结构里面的数组＋单向链表

  - 链表是什么，优缺点
  - 操作链表
  - 经典面试题：单向链表反转

### 链表概念
链表是一种用于存储数据集合的数据结构：
- 相邻元素之间通过指针连接
- 最后一个元素的后继指针值为NULL
- 在程序执行过程中，链表的长度可以增加或减小
- 链表的空间能够按需分配（直到系统内存耗尽）
- 没有内存空间的浪费（但是链表中的指针需要一些额外的内存开销）

优点表现在以下几个方面：
- 可以在常数时间内扩展，相比与数组在内存中是以固定大小创建的一块连续的存储空间，链表的扩展性得以体现
- 动态分配空间

缺点表现在以下几个方面:
- 访问单个元素的时间的开销问题，最差的情况下访问一个元素的开销为O(n)
- 

### 操作链表
 首先我们先画一个链表的图，直观的看一下
![avatar][base64-1]
> 接下来我们写一个链表的声明
```
public class ListNode{
    private int data;
    private ListNode next;
    public ListNode(int data){
        this.data = data
    }
    public void setData(int data){
        this.data = data;
    }
    public int getData(){
        return data;
    }
    public void setNext(ListNode next){
        this.next = next;
    }
    public ListNode getNext(){
        return this.next;
    }
}
```
> 链表的遍历
```
public int Listlength(ListNode node){
    int length =0;
    ListNode currentNode = node;
    while(currentNode!=null){
        length++;
        currentNode = current.getNext()
    }
    return length;
}
```

**时间复杂度为O(n),用于扫描长度为n的链表。空间复杂度为O(1),仅用于创建临时变量**
>链表的插入

  三种情况
  - 在单向链表的开头插入
  - 在单向链表的结尾插入
  - 在单向链表的中间插入
```
public ListNode insertNode(ListNode headNode, ListNode insertToNode, int position){
    if(headNode == null){
        return insertToNode;
    }
    int size = Listlength(headNode);
    if(position>size+1||position<1){
        System.out.println(" position is valid inputs");
        return headNode;
    }
    if(position == 1){
        insertToNode.next(headNode);
        return insertToNode;
    }else{
        //在链表中间或末尾插入
        ListNode previousNode = headNode;
        int count = 0;
        while(count<position-1){
            count++;
            previousNode = previousNode.getNext()
        
        insertToNode.setNext(previousNode.getNext())
        previousNode.setNext(insertToNode)
    }
    return headNode;
}
```

### 链表反转
  
自己想到的反转链表的方法，仅供参考：
- 通过java的stack类特性
- 通过redis 的lists结构的特性
- 算法实现

暂时先上算法实现部分
```
public class demo {

    private static Node head;
    private static class Node{
        int data;
        Node next;
        Node(int data){
            this.data = data;
        }
    }
    public static void reverLinkedList(){
        Node p1 = head;
        Node p2 = head.next;
        Node p3 = null;
        while(p2!=null){
            p3 = p2.next;
            p2.next = p1;
            p1 = p2;
            p2 = p3;
        }
        head.next = null;
        head = p1;
    }

    public static void main(String [] args){
        //初始化链表
        head = new Node(3);
        head.next = new Node(5);
        Node temp = head.next;
        temp.next = new Node(1);
        temp = temp.next;
        temp.next = new Node(4);
        temp = temp.next;
        temp.next = new Node(9);
        //输出链表
        temp = head;
        while(temp!=null){
            System.out.println(temp.data);
            temp = temp.next;
        }
        //逆序链表
        reverLinkedList();
        //输出逆序后链表
        temp = head;
        while(temp!=null){
            System.out.print(temp.data);
            temp = temp.next;
        }
    }
}
```
> 引自 程序员小灰 




[base64-1]:data:image/png;base64,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
