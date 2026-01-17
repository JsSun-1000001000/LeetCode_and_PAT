
[704. 二分查找 - 力扣（LeetCode）](https://leetcode.cn/problems/binary-search/)

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

[704. 二分查找 - 力扣（LeetCode）](https://leetcode.cn/problems/binary-search/)

## 代码
暴力：
```cpp

```
二分查找法：
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

