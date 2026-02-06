## [1047. 删除字符串中的所有相邻重复项 - 力扣（LeetCode）](https://leetcode.cn/problems/remove-all-adjacent-duplicates-in-string/description/)

说白了，栈
## 代码
```cpp
class Solution {
public:
    string removeDuplicates(string s) {
        stack<int> st;
        for(char member : s){
            if(st.empty() || member != st.top()){
                st.push(member);
            }
            else{
                st.pop();
            }
        }
        string res = "";
        while(!st.empty()){
            res += st.top();
            st.pop();
        }
        reverse(res.begin(), res.end());
        return res;
    }
};
```