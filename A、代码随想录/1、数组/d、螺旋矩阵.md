螺旋矩阵要坚持一致的左闭右开，或者左开右闭区间，这样才能按照统一的规则画下来

## [59. 螺旋矩阵 II - 力扣（LeetCode）](https://leetcode.cn/problems/spiral-matrix-ii/description/)
```cpp
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        int left = 0, right = n-1, top = 0, bottom = n-1;
        vector<vector<int>> matrix(n, vector<int>(n));
        int k = 1;
        while(k<=n*n){
            for(int i = left;i<=right;++i,++k)matrix[top][i] = k;
            ++top;
            for(int i = top;i<=bottom;++i,++k)matrix[i][right] = k;
            --right;
            for(int i = right;i>=left;--i,++k)matrix[bottom][i] = k;
            --bottom;
            for(int i=bottom;i>=top;--i,++k)matrix[i][left] = k;
            ++left;
        }
        return matrix;
    }
};
```




