再次重申：

当我们需要查询一个元素是否出现过，或者一个元素是否在集合里的时候，就要第一时间想到哈希法。

## [1. 两数之和 - 力扣（LeetCode）](https://leetcode.cn/problems/two-sum/)

看看需不需要有序，不需要就用unordered喽

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> maptool;
        for(int i = 0; i < nums.size(); i++){
            auto iter = maptool.find(target - nums[i]);
            //注意 不等于的时候是找到了
            if(iter != maptool.end()){
                //first key & second value
                return {iter->second, i};
            }
            maptool.insert(pair<int, int>(nums[i], i));
        }
        return {};
    }
};
```