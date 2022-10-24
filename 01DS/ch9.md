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

## 背包问题

### 01背包问题

**二维数组dp**

1. dp数组及其含义

`dp[i][j]`表示从0-i个物品中任意取重量为j得物品后，最大价值。

2. 确定递推表达式

也就是状态和选择，对于01背包来说，状态就是「背包的容量」和「可选择的物品」。

选择就是「装进背包」或者「不装进背包」。

```cpp
for 状态1 in 状态1的所有取值：
    for 状态2 in 状态2的所有取值：
        for ...
            dp[状态1][状态2][...] = 择优(选择1，选择2...)
```

注：下标是从1开始遍历，上一个物品的价值

**不放物品：**不放物品就是当前容量放不下，那么`dp[i][j] = dp[i-1][j]`，相当于和前面的最大值相同。

**放物品**：放物品是由当前不放，和放的最大值决定的。如果当前放了，那么就剩下的空间的最大存放价值为`dp[i-1][j - weight[i]]`，加上当前物品的价值，取最大值。即`dp[i][j] = max(dp[i-1][j], dp[i-1][j - weight[i]] + value[i])`。

3. 初始化dp数组

首先从`dp[i][j]`的定义出发，如果背包容量j为0的话，即`dp[i][0]`，无论是选取哪些物品，背包价值总和一定为0。

由递推表达式可以看出，是由前一个递推出来的，所以最开始的`dp[i-1][j]`，所以最开始的0要`dp[0][...]`需要初始化。

```cpp
dp[...][0] = 0;
dp[0][...] = 0;

//大小够存放第一个物品时价值，也是此时的最大值，注意dp数组的含义
for (int j = weight[0]; j <= bagweight; j++) {
    dp[0][j] = value[0];
}
```

4. 确定遍历顺序

先遍历物品，再遍历背包大小。

```cpp
// weight数组的大小 就是物品个数
for(int i = 1; i < weight.size(); i++) { // 遍历物品
    for(int j = 0; j <= bagweight; j++) { // 遍历背包容量
        if (j < weight[i]) dp[i][j] = dp[i - 1][j]; 
        else dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - weight[i]] + value[i]);

    }
}
```

5. 举例推导

---

**一维dp 01 背包**

1. 确定dp数组（dp table）以及下标的含义

在一维dp数组中，dp[j]表示：容量为j的背包，所背的物品价值可以最大为dp[j]。

2. 确定递推公式

```cpp
dp[j] = max(dp[j], dp[j - weight[i]] + value[i]);
```

3. dp数组如何初始化

dp[j]表示：容量为j的背包，所背的物品价值可以最大为dp[j]，那么dp[0]就应该是0，因为背包容量为0所背的物品的最大价值就是0。

**这样才能让dp数组在递归公式的过程中取的最大的价值，而不是被初始值覆盖了**。

那么我假设物品价值都是大于0的，所以dp数组初始化的时候，都初始为0就可以了。

4. 确定遍历顺序

```cpp
for(int i = 0; i < weight.size(); i++) { // 遍历物品
    for(int j = bagWeight; j >= weight[i]; j--) { // 遍历背包容量
        dp[j] = max(dp[j], dp[j - weight[i]] + value[i]);
	//倒序遍历，才能保证前一个值都后面一个值最优化无影响
    }
}
```

```cpp
void test_1_wei_bag_problem() {
    vector<int> weight = {1, 3, 4};
    vector<int> value = {15, 20, 30};
    int bagWeight = 4;

    // 初始化
    vector<int> dp(bagWeight + 1, 0);
    for(int i = 0; i < weight.size(); i++) { // 遍历物品
		cout << "weight:" << weight[i] << endl;
		for(int j = bagWeight; j >= weight[i]; j--) { // 遍历背包容量
            dp[j] = max(dp[j], dp[j - weight[i]] + value[i]);
			printf("dp[%d]: = %d\n", j, dp[j]);
		}
		cout << endl;
	}
    cout << dp[bagWeight] << endl;
}

int main() {
    test_1_wei_bag_problem();
	system("pause");
}
```

### 完全背包

> 有N件物品和一个最多能背重量为W的背包。第i件物品的重量是weight[i]，得到的价值是value[i] 。**每件物品都有无限个（也就是可以放入背包多次）**，求解将哪些物品装入背包里物品价值总和最大。
>
> **完全背包和01背包问题唯一不同的地方就是，每种物品有无限件**。

01背包内嵌的循环是从大到小遍历，为了保证每个物品仅被添加一次。

而完全背包的物品是可以添加多次的，所以要从小到大去遍历。

```cpp
// 先遍历物品，再遍历背包
for(int i = 0; i < weight.size(); i++) { // 遍历物品
    for(int j = weight[i]; j <= bagWeight ; j++) { // 遍历背包容量
        dp[j] = max(dp[j], dp[j - weight[i]] + value[i]);

    }
}
```

纯背包问题，是看能够凑成这个某个，否则要考虑组合还是排列问题，要注意遍历的顺序。

### 多重背包

> 有N种物品和一个容量为V 的背包。第i种物品最多有Mi件可用，每件耗费的空间是Ci ，价值是Wi 。求解将哪些物品装入背包可使这些物品的耗费的空间 总和不超过背包容量，且价值总和最大。

把多件物品划分成多个重复的单件物品，就变成了01背包问题。

```cpp
void test_multi_pack() {
    vector<int> weight = {1, 3, 4};
    vector<int> value = {15, 20, 30};
    vector<int> nums = {2, 3, 2};
    int bagWeight = 10;
    for (int i = 0; i < nums.size(); i++) {
        while (nums[i] > 1) { // nums[i]保留到1，把其他物品都展开
            weight.push_back(weight[i]);
            value.push_back(value[i]);
            nums[i]--;
        }
    }

    vector<int> dp(bagWeight + 1, 0);
    for(int i = 0; i < weight.size(); i++) { // 遍历物品
        for(int j = bagWeight; j >= weight[i]; j--) { // 遍历背包容量
            dp[j] = max(dp[j], dp[j - weight[i]] + value[i]);
        }
        for (int j = 0; j <= bagWeight; j++) {
            cout << dp[j] << " ";
        }
        cout << endl;
    }
    cout << dp[bagWeight] << endl;

}
int main() {
    test_multi_pack();
}
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

**[96. 不同的二叉搜索树](https://leetcode.cn/problems/unique-binary-search-trees/)**

> 做DP应该想到举例子递归后续的关系，才能写出递推关系式。
>
> 空树也是二叉搜索树，然后1也很明确，2也很明确，到3的时候就明白了，我以不通的值做节点的情况，左0右2，左1右1，左2右0。到这里子树在划分，就找到了递推关系式。

**[416. 分割等和子集](https://leetcode.cn/problems/partition-equal-subset-sum/)**

> 重刷。思考01背包思路

**[1049. 最后一块石头的重量 II](https://leetcode.cn/problems/last-stone-weight-ii/)**

> 还是01背包，关键怎么联想过去。
>
> 最后一块石头的重量：从一堆石头中,每次拿两块重量分别为x,y的石头,若x=y,则两块石头均粉碎;若x<y,两块石头变为一块重量为y-x的石头求最后剩下石头的最小重量(若没有剩下返回0)
>
> 问题转化为：把一堆石头分成两堆,求两堆石头重量差最小值
>
> 进一步分析：要让差值小,两堆石头的重量都要接近sum/2;我们假设两堆分别为A,B,A<sum/2,B>sum/2,若A更接近sum/2,B也相应更接近sum/2
>
> 进一步转化：将一堆stone放进最大容量为sum/2的背包,求放进去的石头的最大重量MaxWeight,最终答案即为sum-2*MaxWeight;

**[474. 一和零](https://leetcode.cn/problems/ones-and-zeroes/)**

> 这题本质上还是01背包的问题，可以用`dp[i][j]`表示 i 个 0 和 j 个1 的最大字串个数。
>
> 背包的遍历都是从后向前更新的。

**[518. 零钱兑换 II](https://leetcode.cn/problems/coin-change-ii/)**

> dp递推式写错了。
>
> 能看出来这是一个完全背包的问题。
>
> dp[j]含义是能组合成j金额的方案数，那么dp[j]应该由dp[ j - coins[i]]推出来的。
>
> 初始化dp[0] = 1,这样才会对后续产生影响。

**[377. 组合总和 Ⅳ](https://leetcode.cn/problems/combination-sum-iv/)**

> 还是一个完全背包问题。
>
> 注意：外包内物品是排列，外物品内包是组合。排列是注重顺序的，组合是不注重的。
>
> C++测试用例有两个数相加超过int的数据，所以需要在if里加上dp[i] < INT_MAX - dp[i - num]。
>
> 但java就不用考虑这个限制，java里的int也是四个字节吧，也有可能leetcode后台对不同语言的测试数据不一样。

**[322. 零钱兑换](https://leetcode.cn/problems/coin-change/)**

> 完全背包问题。
>
> 凑足总额为j - coins[i]的最少个数为dp[j - coins[i]]，那么只需要加上一个钱币coins[i]即dp[j - coins[i]] + 1就是dp[j]（考虑coins[i]）
>
> 所以dp[j] 要取所有 dp[j - coins[i]] + 1 中最小的。
>
> 递推公式：dp[j] = min(dp[j - coins[i]] + 1, dp[j]);
>
> dp[0] 组成0就是需要0个，其他值为了避免被初始值min覆盖，其他应该为INT_MAX。

**[279. 完全平方数](https://leetcode.cn/problems/perfect-squares/)**

> 和322一样的思路。

**[139. 单词拆分](https://leetcode.cn/problems/word-break/)**

> 没有想到用哈希表，查找子串出现的问题。
>
> 题目中说了单词可以重复使用，也不用全部使用，因此这是一个完全背包问题。
>
> 背包的容量就是字符串的长度，物品就是wordDict。
>
> 1. 确定dp数组以及下标的含义
>
> **dp[i] : 字符串长度为i的话，dp[i]为true，表示可以拆分为一个或多个在字典中出现的单词**。
>
> 2. 确定递推公式
>
> 如果确定dp[j] 是true，且 [j, i] 这个区间的子串出现在字典里，那么dp[i]一定是true。（j < i ）。
>
> 所以递推公式是 if([j, i] 这个区间的子串出现在字典里 && dp[j]是true) 那么 dp[i] = true。
>
> 3. dp数组如何初始化
>
> 从递归公式中可以看出，dp[i] 的状态依靠 dp[j]是否为true，那么dp[0]就是递归的根基，dp[0]一定要为true，否则递归下去后面都都是false了。
>
> 4. 确定遍历顺序
>
> 题目中说是拆分为一个或多个在字典中出现的单词，所以这是完全背包。这里应该考虑前后组合的顺序，因此应该先遍历背包再遍历物品。

**[198. 打家劫舍](https://leetcode.cn/problems/house-robber/)**

> 递归表达式想到了，上一个偷了，上一个没偷 + 当前的值。
>
> 所以要初始化 0 1这两个值，对于dp[0]肯定是偷了第一家的东西，对于dp[1]是0，1中选偷一个，对于第三个开始，来判断前两家的偷了或者没偷的情况。

