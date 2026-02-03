## [344. 反转字符串 - 力扣（LeetCode）](https://leetcode.cn/problems/reverse-string/)

## 分析

双指针法

## 代码
```cpp
class Solution {

public:

    void reverseString(vector<char>& s) {

        for(int i = 0, j = s.size()-1; i < s.size()/2; i++, j--){

            swap(s[i],s[j]);

        }

    }

};
```