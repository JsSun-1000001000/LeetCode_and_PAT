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
## 