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
