> [!Mark]
>
> 记录刷题中遇到的问题。

## 语法问题

- 初始化vector\<string\>变量时，为什么要声明命名空间

```cpp
std::vector<std::string> chessboard(n, std::string(n, '.'));
```

> 到后面还是不要直接使用using namepsace std;避免冲突等问题。

- 定义变量时，每个变量都应该赋予初值，哪怕是指向为空。

## 算法逻辑问题

顺序问题：

1. 排序的降序还是升序问题
2. 遍历顺序从前向后，还是从后向前
3. 问题的等价形式