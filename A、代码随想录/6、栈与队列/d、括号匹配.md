用栈解决的经典问题

编译原理的话，编译器在 词法分析的过程中处理括号、花括号等这个符号的逻辑，也是使用了栈这种数据结构。

再举个例子，linux系统中，cd这个进入目录的命令我们应该再熟悉不过了。这个命令最后进入a目录，系统是如何知道进入了a目录呢 ，这就是栈的应用

## 代码

```cpp
class Solution {
public:
    bool isValid(string s) {
        //括号左多余
        //括号不匹配
        //括号右多余
        stack<char> match;
        //括号一定是一对一对的，奇数一定是不匹配的
        if(s.size() % 2 != 0){
            return false;
        }
        for(int i = 0; i < s.size(); i++){
            if(s[i] == '('){
                match.push(')');
            }
            else if(s[i] == '['){
                match.push(']');
            }
            else if(s[i] == '{'){
                match.push('}');
            }
            else if(match.empty() || match.top() != s[i]){
                return false;
            }
            else{
                match.pop();
            }
        }
        return match.empty();
    }
};
```