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

## [49. 字母异位词分组 - 力扣（LeetCode）](https://leetcode.cn/problems/group-anagrams/description/)

```cpp
class Solution {

public:

    vector<vector<string>> groupAnagrams(vector<string>& strs) {

        unordered_map<string, vector<string>> m;

        for(string &s : strs){

            string sorted_s = s;

            ranges::sort(sorted_s);

            m[sorted_s].push_back(s);//sort 后 相同的分到一组

        }

        vector<vector<string>> res;

        res.reserve(m.size());

        for(auto& [_,value] : m){

            res.push_back(value);

        }

        return res;

    }

};
```