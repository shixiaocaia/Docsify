## 数组理论基础

- C++二位数组中地址是连续存放
  - JAVA中并不是


## 二分查找

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
                right = mid ;
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

