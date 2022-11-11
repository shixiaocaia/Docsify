## 数组理论基础

- C++二位数组中地址是连续存放
  - JAVA中并不是


## 二分查找

### 思路

**使用前提**

- 有序数组
- 无重复的元素

**思路**

[left,right]闭区间版本

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size()-1;
// 右区间为闭区间，下标从size-1开始
        
        while(left <= right){
            int mid = left + (right - left) / 2;// 防止溢出 等同于(left + right)/2
            if(nums[mid] > target)
                right = mid - 1;
            else if(nums[mid] < target)
                left = mid + 1;
            else return mid;
        }
        return -1;
    }
};
```

- 这里防止溢出是指，当left和right同为int较大型数据时候，(left+right)容易溢出，而left + (right - left) / 2，相等价也避免了溢出的问题。

[left,right)左闭右开版本

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size();

        while(left < right){
            int mid = left + ((right - left) >> 1);
            if(nums[mid] > target)
                right = mid ; //右是开区间
            else if(nums[mid] < target)
                left = mid + 1;
            else return mid;
        }
        return -1;
    }
};
```

- 位运算符优先级大于+-，注意括号
- 位运算符作除法速度大于除法

### 例题

 **模板题**

> [LC704.二分查找](https://leetcode.cn/problems/binary-search/)
> **[LC69.x的平方](https://leetcode.cn/problems/sqrtx/)**
>
> > 注意两数平方时越界，要加(long long)
>
>  **[LC367.有效的完全平方数](https://leetcode.cn/problems/valid-perfect-square/)**

 **[LC35.搜索插入位置](https://leetcode.cn/problems/search-insert-position/)**

> 二分：一共分为三（四）种情况：（按照[left,right]考虑）
>
> 1. 数组中找到，返回序号
> 2. 数组中插入，最终left==right时，若nums[right]<target, 那么left=left+1（也等价于right+1,因为二者重合了，数值相同），若nums[left] > target, 那么right=right -1但是实际插入位置应该就在此处，因此为right+1，两种比值可以更新为一种right+1。
> 3. 越界插入，如果小于所有数，在头部插入，最后更新为[0,-1], 实际插入为left或者right+1。如果大于所有数，在尾部插入，最后更新为[nums.size()+1,num.size()],实际插入为left或者right+1。
>
> 总结：最后如果没有找到这个数，最终都可以归纳为right+1情况。

> **暴力**循环，如果发现比target大的数，返回当前位置插入。如果遍历完没有，即在nums.size()处插入。

**[LC34.在排序数组中查找元素的第一个和最后一个位置](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/)**

> 一开始想试一下暴力遍历，之前没有学过LC形式，不知道这个输出形式，看了一眼题解如何输出形式，发现是分两部分返回。
>
> 寻找左右边界，对于我们新手分开做，先找左边界，再找右边界。区别“数据不重复”的题，这里可能会遇到重复数据。
>
> 1. 找左边界，从右边向左边推，当我们找到一个target值时，应该继续向左边移动，看看有没有重复值出现，同时这里做一个剪枝判断，如果前一个值小于target或者当前数为第一个数时，跳出循环。
> 2. 找右边界，从左边向右边推，当我们找到一个target时，应该继续向右边，找到边界点，同时做一个剪枝判断，如果后一个值大于target值或者当前为最后一个数时，跳出循环。
>
> 本题卡了我很久一个点：**数组越界访问问题**，剪枝判断应该先判断越界问题再判断大小，否则会出现数组的越界访问。

## 双向指针

**例题：**[LC27.移除元素](https://leetcode.cn/problems/remove-element/)

**快慢指针**

```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int slow = 0, fast = 0;
        //指向不是删除元素时更新
        //快指针是在原数组中寻找val，慢指针是最后的答案数组位置，用来更新
        for(; fast < nums.size(); fast++){
            if(nums[fast] != val){ 
                nums[slow++] = nums[fast];
            }
        }
        return slow;
    }
};
```

**优化**

```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
       int leftIndex = 0;
       int rightIndex = nums.size() - 1;
       while(leftIndex <= rightIndex){
           //找到左边等于val
           while(leftIndex <= rightIndex && nums[leftIndex] != val){
               leftIndex++;
           }
           //找到右边不等于val，如果等于，也会跳过这一个
           while(leftIndex <= rightIndex && nums[rightIndex] ==val){
               rightIndex--;
           }
           if(leftIndex < rightIndex)
           {
               nums[leftIndex++] = nums[rightIndex--];
           }
       }
       //最后leftIndex 肯定指向下一个，返回
       return leftIndex;
    }
};
```

**模板题**

> [LC24.删除重复元素](https://leetcode.cn/problems/remove-duplicates-from-sorted-array/)
>
> [LC27.移除元素](https://leetcode.cn/problems/remove-element/)

[LC283.移动零](https://leetcode.cn/problems/move-zeroes/)

> 一个指向0，一个指向非0，可以用来交换

[LC844.比较含退格的字符串](https://leetcode.cn/problems/backspace-string-compare/)

> 第一种用栈暴力做
> 第二种是，明白#字符只针对前一个字符进行退格基础上，那我们便可以后续遍历这两个数组，确定一个不会移动的字符时，进行比较。
>
> 当序列都在边界范围时进行比较，else的时候分为三种情况，最后合并为一种，这里比较复杂一点。

[LC977.有序数组的平方](https://leetcode.cn/problems/squares-of-a-sorted-array/)

> 用了暴力
>
> 排序待更新。
>
> 使用双向指针，由于原数组按照非递减排序，那么平方后的数，应该在两头，通过双向指针指向头和尾，进行比较大小移动。

## 滑动窗口

**例题：**[LC209.最小子串长度](https://leetcode.cn/problems/minimum-size-subarray-sum/)

```cpp
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int left = 0, right;
        int sum = 0;
        int minlen = INT_MAX;

        for (right = 0; right < nums.size(); right++) {
            sum += nums[right]; //字串和
            while (left <= right && sum >= target) { //更新答案和起始位置
                minlen = min(minlen, right - left + 1);
                sum -= nums[left++];
            }
        }

        return minlen == INT_MAX ? 0 : minlen; //判断有没有找到合适的子串
    }
};

```

```cpp
最小滑窗模板：给定数组 nums，定义滑窗的左右边界 i, j，求满足某个条件的滑窗的最小长度。
while j < len(nums):
    判断[i, j]是否满足条件
    while 满足条件：
        不断更新结果(注意在while内更新！)
        i += 1 （最大程度的压缩i，使得滑窗尽可能的小）
    j += 1
最大滑窗模板：给定数组 nums，定义滑窗的左右边界 i, j，求满足某个条件的滑窗的最大长度。

while j < len(nums):
    判断[i, j]是否满足条件
    while 不满足条件：
        i += 1 （最保守的压缩i，一旦满足条件了就退出压缩i的过程，使得滑窗尽可能的大）
    不断更新结果（注意在while外更新！）
    j += 1
```

**模板题**

> [LC209.最小子串长度](https://leetcode.cn/problems/minimum-size-subarray-sum/)
>
> > 本题可以用前缀和+二分做，通过s[j]-s[i] >= target,可以变化为 s[j] >= s[i]+target。在s数组中寻找第一个大于 s[i]+target位置，进行更新大小，使用了C++ lower_bound()函数
>
> [LC904.水果篮子](https://leetcode.cn/problems/fruit-into-baskets/)
>
> > 大佬的滑动窗口思路，我不断地把水果放到篮子中，当水果种类大于2种时，进行更新篮子中水果种类，最后更新result。
> >
> > 这里的更新篮子思路是：从左边界left开始更新，将这个序号下的水果数-1，当移动到删除完这个水果数为0时，此时水果种类-1，加上前面右边界更新的一个新的，刚好为2种，继续更新答案。
>
> [LC76.最小覆盖字串](https://leetcode.cn/problems/minimum-window-substring/)
>
> > 自己做的时候，忽略了字符串重复出现问题。以及在移动左边界上欠缺考虑，看题解使用的方法是在左边的字符数量已经在后面出现次数大于了所需数量，再去更新右边界。
>
> 难点：字串问题划分为最大和最小，边界更新时机很重要。

## 模拟

> [LC59.螺旋矩阵2](https://leetcode.cn/problems/spiral-matrix-ii/)
>
> [LC54.螺旋矩阵1](https://leetcode.cn/problems/spiral-matrix/)
>
> 上述两题的边界条件判断
