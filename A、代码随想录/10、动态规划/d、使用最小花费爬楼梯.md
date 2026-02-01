## [746. 使用最小花费爬楼梯 - 力扣（LeetCode）](https://leetcode.cn/problems/min-cost-climbing-stairs/description/)

你妈隔壁说的是中国话吗


## 分析

- dp数组到达第 i 阶台阶花费的最少体力
- `dp[i] = min(dp[i-1]+cost[i-1],dp[i-2]+cost[i-2])`
- 初始化0 和 1
- 从前到后遍历cost数组就可以了
## 代码

```cpp
class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {
        vector<int> dp(cost.size() + 1);
        dp[0] = 0;
        dp[1] = 0;
        for(int i = 2; i <= cost.size(); i++){
            dp[i] = min(dp[i-1]+cost[i-1], dp[i-2]+cost[i-2]);
        }
        return dp[cost.size()];
    }
};
```


