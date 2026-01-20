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

## [54. 螺旋矩阵 - 力扣（LeetCode）](https://leetcode.cn/problems/spiral-matrix/description/)
```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> ans;
        if(matrix.size() == 0 || matrix[0].size() == 0){
           return {};
        }
        int a = 0, b = matrix.size()-1;//up right
        int c = 0, d = matrix[0].size()-1;//down left

        while(true){
            for(int i = c;i<=d;i++){
                ans.insert(matrix.begin()+i,matrix[a][i]);
            }
            if(++a>d)break;
            for(int i = a;i<=b;i++){
                ans.insert(matrix.begin()+d+i,matrix[i][d]);
            }
            if(--d>d)break;
            for(int i = d;i<=c;i--){
                ans.insert(matrix.begin()+d+b+i,matrix[b][i]);
            }
            if(--b>d)break;
            for(int i = b;i<=a;i--){
                ans.insert(matrix.begin()+d+b+c+i,matrix[i][c]);
            }
            if(++c>d)break;
        }
        return ans;
    }
};
```

```cpp
class Solution {
private:

    static constexpr int directions[4][2] = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};

public:

    vector<int> spiralOrder(vector<vector<int>>& matrix) {

        if(matrix.size() == 0 || matrix[0].size() == 0){

            return {};

        }

        int rows = matrix.size();

        int columns = matrix[0].size();

  

        vector<vector<bool>> visited(rows, vector<bool>(columns));

        int all = rows*columns;

        vector<int> result(all);

        int row = 0;

        int column = 0;

        int directionIndex = 0;

        for(int i = 0; i < all; i++){

            result[i] = matrix[row][column];

            visited[row][column] = true;

            int nextRow = row + directions[directionIndex][0],

            nextColumn = column + directions[directionIndex][1];

            if(nextRow<0||nextRow>=rows||nextColumn<0||nextColumn>=columns||visited[nextRow][nextColumn]){

                directionIndex = (directionIndex + 1)%4;

            }

            row+=directions[directionIndex][0];

            column+=directions[directionIndex][1];

        }

        return result;

    }

};
```



