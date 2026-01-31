## [509. 斐波那契数 - 力扣（LeetCode）](https://leetcode.cn/problems/fibonacci-number/description/)

```cpp
class Solution {
public:
    int fib(int n) {
        if(n <= 1){
            return n;
        }
        vector<int> dp(n+1);
        dp[0] = 0;
        dp[1] = 1;
        for(int i = 2; i <= n; i++){
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
};
```

需要一维数组来保存递归结果；
确定下标含义；
递推公式；
如何初始化；
确定遍历顺序；
推导dp数组；


