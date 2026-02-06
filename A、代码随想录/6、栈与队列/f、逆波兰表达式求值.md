## [150. 逆波兰表达式求值 - 力扣（LeetCode）](https://leetcode.cn/problems/evaluate-reverse-polish-notation/description/)

## 代码

```cpp
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<long long> st;
        for(int i = 0; i < tokens.size(); i++){
            if(tokens[i] == "+" || tokens[i] == "-" || tokens[i] == "*" || tokens[i] == "/"){
                long long num1 = st.top();
                st.pop();
                long long num2 = st.top();
                st.pop();
                if(tokens[i] == "+"){
                    st.push(num2 + num1);
                }
                if(tokens[i] == "-"){
                    st.push(num2 - num1);
                }
                if(tokens[i] == "*"){
                    st.push(num2 * num1);
                }
                if(tokens[i] == "/"){
                    st.push(num2 / num1);
                }
            }
            else{
                //stoll string->long long
                st.push(stoll(tokens[i]));
            }
        }
        long long res = st.top();
        st.pop();
        return res;
    }
};
```