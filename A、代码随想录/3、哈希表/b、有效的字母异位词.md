## [242. 有效的字母异位词 - 力扣（LeetCode）](https://leetcode.cn/problems/valid-anagram/)

```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        int record[26] = {};
        for(int i = 0; i < s.size(); i++){
            record[s[i]-'a'] ++;
        }  
        for(int i = 0; i < t.size(); i++){
            record[t[i]-'a'] --;
        }
        for(int i = 0; i < 16; i++){
            if(record[i] != 0){
                return false;
            }
        }
        return true;
    }
};
```
