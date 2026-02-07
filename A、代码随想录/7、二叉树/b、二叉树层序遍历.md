## [102. 二叉树的层序遍历 - 力扣（LeetCode）](https://leetcode.cn/problems/binary-tree-level-order-traversal/description/)
## 代码
递归法：
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */

class Solution {
public:
    void order(TreeNode* cur, vector<vector<int>>& result, int dep){
        if(cur == nullptr){
            return;
        }
        if(result.size() == dep){
            result.push_back(vector<int>());
        }

        result[dep].push_back(cur->val);
        order(cur->left, result, dep + 1);
        order(cur->right, result, dep + 1);
    }

    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> result;
        int dep = 0;
        order(root, result, dep);
        return result;
    }
};
```

迭代法：
【挖坑】

## [107. 二叉树的层序遍历 II - 力扣（LeetCode）](https://leetcode.cn/problems/binary-tree-level-order-traversal-ii/description/)

## 代码

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */

class Solution {
public:
    void order(TreeNode* cur, vector<vector<int>>& result, int dep){
        if(cur == nullptr){
            return ;
        }
        if(result.size() == dep){
            result.push_back(vector<int>());
        }
        result[dep].push_back(cur->val);
        order(cur->left, result, dep + 1);
        order(cur->right, result, dep + 1);
    }
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        vector<vector<int>> result;
        int dep = 0;
        order(root, result, dep);
        reverse(result.begin(), result.end());
        return result;
    }
};
```

