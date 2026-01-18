## [27. 移除元素 - 力扣（LeetCode）](https://leetcode.cn/problems/remove-element/description/)
## 代码
暴力解法：
```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int size = nums.size();
        for(int i = 0; i < size; i++){
            if(nums[i] == val){
                for(int j = i + 1; j < size; j++){
                    nums[j-1] = nums[j];
                }
                i--;
                size--;
            }
        }
        return size;
    }
};
```
双指针法：
```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int left = 0;
        for(int right = left; right < nums.size(); right++){
            if(nums[right]!=val){
                nums[left] = nums[right];
                left++;
            }
        }
        return left;
    }
};
```
## [26. 删除有序数组中的重复项 - 力扣（LeetCode）](https://leetcode.cn/problems/remove-duplicates-from-sorted-array/description/)

## 代码
```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int slow = 0;
        for(int fast = slow; fast < nums.size(); fast++){
            if(nums[fast]!=nums[slow]){
                slow++;
                nums[slow] = nums[fast];
            }
        }
        return slow + 1;
    }
};
```
## [283. 移动零 - 力扣（LeetCode）](https://leetcode.cn/problems/move-zeroes/description/)

## 代码
```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int slow = 0;
        int fast = 0;
        while(fast < nums.size()){
            if(nums[fast]!=0){
                swap(nums[fast],nums[slow]);
                slow++;
            }
            fast++;
        }
    }
};
```
## [844. 比较含退格的字符串 - 力扣（LeetCode）](https://leetcode.cn/problems/backspace-string-compare/description/)
## 代码
用栈的思路：
```cpp
class Solution {
public:
    bool backspaceCompare(string s, string t) {
        string ss;
        string tt;
        for(int i = 0; i < s.size(); i++){
            if(s[i]!='#'){
                ss+=s[i];
            }
            else if(!ss.empty()){
                ss.pop_back();
            }
        }
        for(int i = 0; i < t.size(); i++){
            if(t[i]!='#'){
                tt+=t[i];
            }
            else if(!tt.empty()){
                tt.pop_back();
            }
        }
        if( ss == tt)return true;
        return false;
    }
};
```
双指针：
```cpp
class Solution {
public:
    bool backspaceCompare(string s, string t) {
        //双指针
        int sPoint = s.size() - 1;
        int tPoint = t.size() - 1;

        int sCount = 0;
        int tCount = 0;

        while(1){
            while(sPoint >= 0){
                if(s[sPoint] == '#'){
                    sCount++;
                }
                else{
                    if(sCount > 0){
                        sCount --;
                    }
                    else{
                        break;
                    }
                }
                sPoint --;
            }
            while(tPoint >= 0){
                if(t[tPoint] == '#'){
                    tCount++;
                }
                else{
                    if(tCount > 0){
                        tCount --;
                    }
                    else{
                        break;
                    }
                }
                tPoint --;
            }
            if(sPoint < 0 || tPoint < 0){
                break;
            }
            if(s[sPoint]!=t[tPoint]) return false;
            sPoint --;
            tPoint --;
        }
        if(sPoint == -1 && tPoint == -1)return true;
        return false;
    }
};
```
## [977. 有序数组的平方 - 力扣（LeetCode）](https://leetcode.cn/problems/squares-of-a-sorted-array/description/)
暴力：
```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& A) {
        for (int i = 0; i < A.size(); i++) {
            A[i] *= A[i];
        }
        sort(A.begin(), A.end()); // 快速排序
        return A;
    }
};
```

双指针法：
数组其实是有序的， 只不过负数平方之后可能成为最大数了。那么数组平方的最大值就在数组的两端，不是最左边就是最右边，不可能是中间。此时可以考虑双指针法了
```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        int left = 0;
        int right = nums.size() - 1;

        vector<int> res(nums.size());

        int pos = nums.size()-1;

        while(left <= right){
            if(nums[left]*nums[left] >= nums[right]*nums[right]){
                res[pos] = nums[left]*nums[left];
                left++;
                pos--;
            }
            else{
                res[pos] = nums[right]*nums[right];
                right--;
                pos--;
            }
        }
        return res;
    }
};
```


