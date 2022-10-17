## What

动态规划，英文：Dynamic Programming，简称DP，如果某一问题有很多重叠子问题，使用动态规划是最有效的。

所以动态规划中每一个状态一定是由上一个状态推导出来的，**这一点就区分于贪心**，贪心没有状态推导，而是从局部直接选最优的，同时这也是全局最优的。

## 步骤

1. 确定dp数组（dp table）以及下标的含义
2. 确定递推公式
3. dp数组如何初始化
4. 确定遍历顺序
5. 举例推导dp数组

**找问题的最好方式就是把dp数组打印出来，看看究竟是不是按照自己思路推导的！**

## 例子-斐波那契数列

1. 确定dp数组（dp table）以及下标的含义

> dp[i] 表示第i个数的斐波那契数列数值

2. 确定递推公式

> 题目已给：dp[i] = dp[i-1] + dp[i-2]

3. dp数组如何初始化

> dp[0] = 0, dp[1] = 1;

4. 确定遍历顺序

> 从前向后遍历，因为后一项依赖前两项。

5. 举例推导dp数组

> 按照这个递推公式dp[i] = dp[i - 1] + dp[i - 2]，我们来推导一下，当N为10的时候，dp数组应该是如下的数列：
>
> 0 1 1 2 3 5 8 13 21 34 55
>
> 根据这个，可以打印输出判断是否正确。

```cpp
class Solution {
public:
    int fib(int n) {
        int dp[35];
        dp[0] = 0;
        dp[1] = 1;
        for(int i = 2; i <= n; i++){
            dp[i] = dp[i-1] + dp[i-2];
        }
        return dp[n];
    }
};
```

**优化空间写法**

```cpp
class Solution {
public:
    int climbStairs(int n) {
        if (n <= 1) return n;
        int dp[3];
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i <= n; i++) {
            int sum = dp[1] + dp[2];
            dp[1] = dp[2];
            dp[2] = sum;
        }
        return dp[2];
    }
};
```



## 刷题

**[746. 使用最小花费爬楼梯](https://leetcode.cn/problems/min-cost-climbing-stairs/)**

> 根据五个步骤。
>
> 递推公式我一开始就想错了。是由走一步上来的的费用或者走两步上来的费用，加上当前层的费用。
>
> 最后答案也是，走一步跨上来的，走两步上来的最小值。

**[62. 不同路径](https://leetcode.cn/problems/unique-paths/)**
> 本科做过的题，注意初始化。
>
> 如果按照五步法的话，要注意最左一层，最上一层的初始。

**[63. 不同路径 II](https://leetcode.cn/problems/unique-paths-ii/)**

> 和上一题一样，再对有障碍物的地方做一个特判，如果当前位置有障碍物就清0。
>
> 此外要注意本题还将start处设置了障碍物，那肯定无法到达。

```cpp
vector<vector<int>> dp(m, vector<int>(n, 0)); // 初始化一个二维数组
```

**[343. 整数拆分](https://leetcode.cn/problems/integer-break/)**
> 1. dp[i]表示 分拆数字i，可以得到的最大乘积为 dp[i]。
>
> 2. dp[i] 一种为 j * (i - j)，一种为j * dp[i - j] 是对 i - j 的再拆分至少两个数的最大值 `dp[i] = max(dp[i], max((i - j) * j, dp[i - j] * j));`
>
> 3. dp[0] dp[1] 就不应该初始化，也就是没有意义的数值。只初始化dp[2] = 1.
>
> 4. dp[i] 是依靠 dp[i - j]的状态，所以遍历i一定是从前向后遍历，先有dp[i - j]再有dp[i]。
>
>    枚举 j 的时候，是从1开始的。i 是从3开始，这样dp[i - j]就是dp[2]正好可以通过我们初始化的数值求出来。

> 用容器实现初始化，`int dp[n  + 1] = {0}`报错。
