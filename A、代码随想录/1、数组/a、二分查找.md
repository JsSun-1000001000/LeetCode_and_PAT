
# [704. 二分查找 - 力扣（LeetCode）](https://leetcode.cn/problems/binary-search/)

1. 要清楚区间的定义
2. 是用左闭右开，还是左右闭区间，不要混在一起
3. 坚持循环不变量的原则
## 第一种

左闭右闭区间

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size()-1;
        //如果左边界小于右边界
        while( left <= right ){
            int middle = left+(right-left)/2;
            if( nums[middle] > target){
                //target 在区间内
                right = middle - 1;
            }
            else if( nums[middle] < target ){
                //target 在区间外
                left = middle + 1;
            }
            else{
                return middle;
            }
        }
        return -1;
    }
};
```

## 第二种

左闭右开

```cpp
class Solution{
public:
	int search(vector<int>& nums, int target){
		int left = 0;
		int right = nums.size();
		while(left < right){
			int middle = left + ((right - left)>>1);
			if( nums[middle] > target){
				right = middle;
			}
			else if( nums[middle] < target ){
				left = middle +1;
			}
			else{
				return middle;
			}
		}
		return -1;
	}
};
```
---

# [35. 搜索插入位置 - 力扣（LeetCode）](https://leetcode.cn/problems/search-insert-position/description/)
## 代码
暴力：
```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        for(int i = 0; i < nums.size(); i++){
            if(nums[i]>=target){
                return i;
            }
        }
        return nums.size();
    }
};
```
二分查找法：
左右闭区间：
```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size() - 1;
        while( left <= right ){
            int middle = left + (right-left)/2;
            if( nums[middle] > target ){
                right = middle - 1;
            }
            else if( nums[middle] < target ){
                left = middle + 1;
            }
            else{
                return middle;
            }
        }
        return  right+1;
    }
};
```
左闭右开：
```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size();// 定义target在左闭右开的区间里，[left, right)  target
        while(left < right){
            int middle = left + (right - left)/2;
            if(target < nums[middle]){
                //左闭右开区间 不包含右边界
                right = middle;
            }
            else if(target > nums[middle]){
                left = middle + 1;
            }
            else{
                return middle;
            }
        }
        return right;
    }
};
```

# [34. 在排序数组中查找元素的第一个和最后一个位置 - 力扣（LeetCode）](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/description/)

## 代码
暴力：
```cpp
//zaishuo
```
二分查找：
```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int start = -1;
        int end = -1;
        int left = 0;
        int right = nums.size() - 1;//左右闭区间
        while( left <= right ){
            //三种情况
            //第一种 超出边界 -1-1
            //第二种 没有返回 -1-1
            //第三种 左右边界
            int middle = left + (right - left)/2;
            if(target < nums[middle]){
                right = middle - 1;
            }
            else if(target > nums[middle]){
                left = middle + 1;
            }
            else{
                //找到了target
                start = end = middle;
                while(start >= 0 && nums[start]==target){
                    start = start - 1;
                }
                while(end < nums.size() && nums[end]==target){
                    end = end + 1;
                }
                if(nums.size() == 1){
                    return {0,0};
                }
                else{
                    return {start + 1,end - 1};
                }
            }
        }
        return {start,end};
    }
};
```
参考答案是：用两个二分查找分别查找zuo'bian

