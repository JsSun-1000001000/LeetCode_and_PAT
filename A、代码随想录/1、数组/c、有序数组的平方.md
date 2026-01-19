
见上一篇文章；

滑动窗口，**就是不断的调节子序列的起始位置和终止位置，从而得出我们想要的结果**。

在暴力解法中，是一个for循环滑动窗口的起始位置，一个for循环为滑动窗口的终止位置，用两个for循环 完成了一个不断搜索区间的过程。

那么滑动窗口如何用一个for循环来完成这个操作呢。

首先要思考 如果用一个for循环，那么应该表示 滑动窗口的起始位置，还是终止位置。

如果只用一个for循环来表示 滑动窗口的起始位置，那么如何遍历剩下的终止位置？

此时难免再次陷入 暴力解法的怪圈。

所以 **只用一个for循环，那么这个循环的索引，一定是表示 滑动窗口的终止位置。**

窗口就是 满足其和 ≥ s 的长度最小的 连续 子数组。

窗口的起始位置如何移动：如果当前窗口的值大于等于s了，窗口就要向前移动了（也就是该缩小了）。

窗口的结束位置如何移动：窗口的结束位置就是遍历数组的指针，也就是for循环里的索引。

解题的关键在于 窗口的起始位置如何移动

**滑动窗口的精妙之处在于根据当前子序列和大小的情况，不断调节子序列的起始位置。从而将O(n^2)暴力解法降为O(n)。**
## [209. 长度最小的子数组 - 力扣（LeetCode）](https://leetcode.cn/problems/minimum-size-subarray-sum/description/)

```cpp
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int left = 0;
        int subLength = 0;
        int sum = 0;
        int result = INT_MAX;

        for( int right = 0; right < nums.size(); right++){
            sum += nums[right];
            while(sum >= target){
                subLength = right-left+1;
                result = result < subLength ? result : subLength;
                sum -= nums[left++];
            }
        }
        return result == INT_MAX ? 0 : result;
    }
};
```

## [904. 水果成篮 - 力扣（LeetCode）](https://leetcode.cn/problems/fruit-into-baskets/description/)
```cpp
class Solution {
public:
    int totalFruit(vector<int>& fruits) {
        int left = 0;
        int res = 0;
        unordered_map<int,int> count;
        for( int right = 0; right < fruits.size(); right ++){
            ++count[fruits[right]];
            while(count.size()>2){
                auto it = count.find(fruits[left]);
                --it->second;
                if(it->second == 0){
                    count.erase(it);
                }
                ++left;
            }
            res = max(res, right - left + 1);
        }
        return res;
    }
};
```

```cpp
class Solution {
public:
    int totalFruit(vector<int>& fruits) {
        int left = 0;
        vector<int> intCounts(fruits.size());//记录某种水果采摘的个数
        int kinds = 0;//记录采摘水果的种类
        int ans = 0;
        for(int i=0;i<fruits.size();i++){
            if(intCounts[fruits[i]] == 0){
                kinds++;
            }
            intCounts[fruits[i]]++;
            while(kinds >2){//发现采摘种类大于2时，left开始右移
                intCounts[fruits[left]]--;//每次右移都丢掉对应篮子里的水果
                if(intCounts[fruits[left]] == 0){ // 直到把某个篮子里的水果丢空则种类-1.
                    kinds--;
                }
                left++;
            }
            ans = max(ans,i-left+1);
        }
        return ans;
    }
};
```