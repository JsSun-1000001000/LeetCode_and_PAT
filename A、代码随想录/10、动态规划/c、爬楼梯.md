## [70. 爬楼梯 - 力扣（LeetCode）](https://leetcode.cn/problems/climbing-stairs/)

## 分析

- 确定dp数组：爬i层有dpi种方法
- dpi = dpi-1 + dpi-2种方法
- 初始化，第一层有1种第二层有2种
- 顺序：从前向后遍历
- 12358。。。的数组

和斐波那契不同的是，没有讨论0应该是什么
## 代码

```cpp
class Solution {
public:
    int climbStairs(int n) {
        if(n <= 1){
            return n;
        }
        vector<int> dp(n+1);
        dp[1] = 1;
        dp[2] = 2;
        for(int i = 3; i <= n; i++){
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
};
```


