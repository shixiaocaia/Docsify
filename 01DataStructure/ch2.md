## 链表理论基础

**单链表**

![链表1](http://pic.shixiaocaia.fun/202208080645797.png)

链表是一种通过指针串联在一起的线性结构，每一个节点由两部分组成，一个是数据域一个是指针域（存放指向下一个节点的指针），最后一个节点的指针域指向null。

链表得入口节点称为head（头节点）。



**双链表**

![链表2](http://pic.shixiaocaia.fun/202208080647499.png)

单链表中的指针域只能指向节点的下一个节点。

双链表：每一个节点有两个指针域，一个指向下一个节点，一个指向上一个节点。

双链表 既可以向前查询也可以向后查询。



**循环链表**

![链表4](http://pic.shixiaocaia.fun/202208080648608.png)

循环链表，顾名思义，就是链表首尾相连。

**链表的存储**

数组在内存中是连续分布，在内存中不是连续分布的。

链表是通过指针域的指针链接在内存中各个节点。

分配机制取决于操作系统的内存管理。



## 基本用法

**链表的定义**

```cpp
struct ListNode{
    int val; //element
    ListNode *next; //next ptr
    ListNode(int x) : val(x), next(NULL) {} // 节点的构造函数
}

ListNod* head = new ListNode(5);
```

**删除节点**

- 只要将C节点的next指针 指向E节点就可以了。
- 释放中间D节点的内存。

**添加节点**

- C节点的next指针指向新的节点F

- F节点的next指针指向节点D

**新建节点**
- 初始化一个新的空节点，值为0，指向该节点的指针为Node
  ```cpp
  ListNode* Node = new ListNode(0);

## 数组链表对比

![链表-链表与数据性能对比](http://pic.shixiaocaia.fun/202208080658535.png)

- 数组在定义时，长度固定，不可变。
- 链表长度不固定，可以动态增删。

## 移除链表元素

**例题：LC203**

---

**直接删除**

```cpp
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        while(head != NULL && head->val == val){ //如果头节点符合条件，删除直不符合
            ListNode* tmp = head;
            head = head->next;
            delete tmp;
        }

        //删除非头节点
        ListNode* cur=head;
        while(cur != NULL && cur->next != NULL){
            if(cur->next->val == val){
                ListNode* tmp = cur->next;
                cur->next = cur->next->next;
                delete tmp;
            }
            else{
                cur = cur->next;
            }
        }
        return head;
    }
};
```

**创建虚节点统一删除**

```cpp
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode* dummy = new ListNode(0);
        dummy->next = head;
        ListNode* cur = dummy;

        while(cur != NULL && cur ->next != NULL){
            if(cur ->next->val == val){
                ListNode *tmp = cur->next;
                cur->next = cur->next->next;
                delete tmp;
            }
            else{
                cur = cur->next; 
            }
        }
        head = dummy->next;
        delete dummy;
        return head;

    }
};
```

## 设计链表

**例题：LC707**

---

mark。待重写。

## 例题

**[LC203.移除链表元素](https://leetcode.cn/problems/remove-linked-list-elements/)**

> 使用C++，注意释放删除的内存空间。

**[LC707.设计链表](https://leetcode.cn/problems/design-linked-list/)**

> 思路简单，但是全是细节的题。
>
> 模拟了链表的各种操作。

**[LC206.反转链表](https://leetcode.cn/problems/reverse-linked-list/)**

> 方法1：递归
>
> 递归的方法与双指针的方法相同，简洁一些。
>
> 方法2：双指针

**[LC24. 两两交换链表中的节点](https://leetcode.cn/problems/swap-nodes-in-pairs/)**

> 通过循环判断后两个节点是否为空
>
> ![24.两两交换链表中的节点1](D:\Code\Typorapic\202208110712982.png)
>
> 1. 保存后两个节点
> 2. cur 指向 2 这个节点
> 3. 再指向1这个节点
> 4. 最后指向下一组的3

**[LC19.删除链表的倒数第N个节点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)**

> 处理数组、链表中的某部分——双指针
>
> 将fast指针指向删除节点的前一个节点，然后fast指针遍历到NULL时，刚好slow指针遍历到要删除的节点。
>
> 同样用哑节点，规避了分类头节点问题。

**[面试题 02.07. 链表相交](https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/)**

> 先计算两个链表的长度，计算他们长度差，将指针移动到统一起点。
>
> 开始遍历较长的链表（默认A，比较后交换），当二者指针相同相等时，找到了相交节点返回，否则返回NULL。
>
> 注意判断交点是**指针相等**，不是数值相等。

**[LC142.环形链表II](https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/)**

> 待做，主要是涉及到的数学问题。
>
> 1. 判断是否有环形
> 2. 判断环形的入口

## 归纳总结

- 链表的例题第一遍都是参考的思路，涉及指针的操作，是过去不熟悉的，需要多次复习。
- 增加**哑节点**可以使得处理头节点像其他非头节点情况下。
- 节点的大小，和数组一样从0开始
