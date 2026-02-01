## [383. 赎金信 - 力扣（LeetCode）](https://leetcode.cn/problems/ransom-note/description/)



## 代码
```cpp
class Solution {

public:

    bool canConstruct(string ransomNote, string magazine) {

        //magazine里的字符不可以重复使用

        int record[26] = {0};

        if(ransomNote.size() > magazine.size()){

            return false;

        }

  

        for( int  i = 0; i < magazine.length(); i++){

            record[magazine[i] - 'a']++;

        }

        for(int j = 0; j < ransomNote.length(); j++){

            record[ransomNote[j] - 'a']--;

            if(record[ransomNote[j] - 'a'] < 0){

                return false;

            }

        }

        //只有小写字母

        return true;

    }

};
```