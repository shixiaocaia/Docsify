## 栈与队列理论基础

**我们使用的stack是属于哪个版本的STL？**

C++标准库是有多个版本的，才能知道对应的栈和队列的实现原理。下面是三个最为普遍的STL版本：

1. HP STL 其他版本的C++ STL，一般是以HP STL为蓝本实现出来的，HP STL是C++ STL的第一个实现版本，而且开放源代码。
2. P.J.Plauger STL 由P.J.Plauger参照HP STL实现出来的，被Visual C++编译器所采用，不是开源的。
3. SGI STL 由Silicon Graphics Computer Systems公司参照HP STL实现，被Linux的C++编译器GCC所采用，SGI STL是开源软件，源码可读性甚高。

**基本功能**

栈提供push 和 pop 等等接口，所有元素必须符合先进后出规则，所以栈不提供走访功能，也不提供迭代器(iterator)。 不像是set 或者map 提供迭代器iterator来遍历所有元素。

**C++中stack 不是容器**

栈是以底层容器完成其所有的工作，对外提供统一的接口，底层容器是可插拔的（也就是说我们可以控制使用哪种容器来实现栈的功能）。

所以STL中栈往往不被归类为容器，而被归类为container adapter（容器适配器）。

我们常用的SGI STL，如果没有指定底层实现的话，默认是以**deque**为缺省情况下栈的低层结构。

deque是一个双向队列，只要封住一段，只开通另一端就可以实现栈的逻辑了。

SGI STL中 队列底层实现缺省情况下一样使用deque实现的。

## 例题

**[232. 用栈实现队列](https://leetcode.cn/problems/implement-queue-using-stacks/)**

> 使用双栈，一个为输入栈，一个为输出栈。
>
> 输入栈用来存放入队操作，输出栈在pop时，一一弹出栈顶元素。当输出栈为空时，需要将输入栈中的元素全部push到输出栈中。这样才能保证队列的先进先出，移动到两次出栈就变转换了顺序！并且如果不是一起出栈，后续有其他元素push进来会扰乱顺序。
>
> 返回队列元素，用一次pop，再压入一次即可
>
> 判断队列为空，只要两个栈都为空时即为空。

**[225. 用队列实现栈](https://leetcode.cn/problems/implement-stack-using-queues/)**

>对比用栈实现队列，用队列模拟栈，第二个队列只是用来备份的，将前n-1个数备份，然后弹出栈顶元素，最后再还原回去。
>
>那么栈顶元素，只要back一下即可。
>
>判断为空的，只要判断第一个队列是否为空即可。

**[20. 有效的括号](https://leetcode.cn/problems/valid-parentheses/)**

> 用来栈的先进后出，将左括号压入栈中，遇到右括号时如果前一个匹配则出栈，否则入栈。并且在此处"([)]"是无效字符串。

**[1047. 删除字符串中的所有相邻重复项](https://leetcode.cn/problems/remove-all-adjacent-duplicates-in-string/)**

> 类似括号匹配，匹配前一个字符是否相同，相同就出栈，否则入栈。最后将栈的字符出栈保存到的ans中，但是由于栈是后进先出，所以要反转字符串。

**[150. 逆波兰表达式求值](https://leetcode.cn/problems/evaluate-reverse-polish-notation/)**

> 昨天写的时候把字符也入栈，导致要判断复数情况，实际上读取tokens,在过程中遇到运算符时，弹出计算即可.
> 还有需要主要弹出顺序，先出栈的是被减数num1,再出栈是减数num2,最后应该num2-num1。

> PS: 这题不配是中等题吧。

**[239. 滑动窗口最大值](https://leetcode.cn/problems/sliding-window-maximum/)**

> 单调队列，始终维护队列中是一个单调递减，在k区间范围内的最大值。使用deque来模拟。
>
> 每次出队，是第i-k数，如果这个数在队中就出栈，并且最前面的数一定是最大，序号最靠前的数，不会出多的数值。
>
> 每次入队，从后面，当大于队尾数时，就出队队尾这个值，这个值肯定不是区间内的次大值。
>
> 记录答案，一定是队首的数。

**[347. 前 K 个高频元素](https://leetcode.cn/problems/top-k-frequent-elements/)**

> 小顶堆待做。