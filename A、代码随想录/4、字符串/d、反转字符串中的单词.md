## [151. 反转字符串中的单词 - 力扣（LeetCode）](https://leetcode.cn/problems/reverse-words-in-a-string/description/)

## 分析

不太明白 还得看看。。。
## 代码

```cpp
class Solution {
public:
    void removeExtraSpaces(string& s){
        int slow = 0;
        for(int i = 0; i < s.size(); ++i){
            if(s[i] != ' '){
                if(slow != 0){
                    s[slow++] = ' ';
                }
                while(i < s.size() && s[i] != ' '){
                    s[slow++] = s[i++];
                }
            }
        }
        s.resize(slow);
    }

    void reverse(string& s, int start, int end){
        for(int i = start, j = end; i < j; i++, j--){
            swap(s[i],s[j]);
        }
    }

    string reverseWords(string s) {
        //移除多余空格
        //反转字符串
        //单词反转
        removeExtraSpaces(s);
        reverse(s, 0, s.size()-1);
        int start = 0;
        for(int i = 0; i <= s.size(); ++i){
            //到达空格或者末尾表示单词结束，开始反转
            if(i == s.size() || s[i] == ' '){
                reverse(s, start, i - 1);
                start = i + 1;
            }
        }
        return s;
    }
};
```