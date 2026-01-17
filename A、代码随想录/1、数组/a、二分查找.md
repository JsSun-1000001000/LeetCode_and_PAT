
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

最好分块处理，不要混在一起
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
参考答案是：用两个二分查找分别查找左边界和右边界
```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int left = getLeftEdge(nums, target);
        int right = getRightEdge(nums, target);
        if(left == -2 || right == -2){
            return {-1, -1};
        }
        else if(right - left > 1){
            return {left + 1, right - 1};
        }
        else{
            return {-1,-1};
        }
    }
private:
    int getRightEdge(vector<int>& nums, int target){
        int left = 0;
        int right = nums.size()-1;
        int rightEdge = -2;
        while(left <= right){
            int middle = left + (right - left)/2;
            if(target < nums[middle]){
                right = middle - 1;
            }
            else {
                left = middle + 1;
                rightEdge = left;
            }
        }
        return rightEdge;
    }
    int getLeftEdge(vector<int>& nums, int target){
        int left = 0;
        int right = nums.size()-1;
        int leftEdge = -2;
        while(left <= right){
            int middle = left + (right - left)/2;
            if(target <= nums[middle]){
                right = middle - 1;
                leftEdge = right;
            }
            else {
                left = middle + 1;
            }
        }
        return leftEdge;
    }
};
```

## [69. x 的平方根 - 力扣（LeetCode）](https://leetcode.cn/problems/sqrtx/description/)

## 代码
二分查找法：
注意：
- 乘积long long
- 左边界小于等于的时候就可以跳出了
```cpp
class Solution {
public:
    int mySqrt(int x) {
        int left = 0;
        int right = x;
        int res = -1;
        while(left <= right){
            int middle = left + (right - left)/2;
            if((long long)middle * middle > x){
                right = middle - 1;
            }
            else if((long long)middle * middle <= x){
                res = middle;
                left = middle + 1;
            }
        }
        return res;
    }
};
```
数学方法：
`exp`函数，没用过；
注意： 由于计算机无法存储浮点数的精确值（浮点数的存储方法可以参考 IEEE 754，这里不再赘述），而指数函数和对数函数的参数和返回值均为浮点数，因此运算过程中会存在误差。
因此在得到结果的整数部分 ans 后，我们应当找出 ans 与 ans+1 中哪一个是真正的答案。
```cpp
class solution{
public:
	int mySqrt(int x){
		if(x == 0){
			return 0;
		}
		int res = exp(0.5 * log(x));
		return ((long long)(res + 1)*(res + 1) <= x ? res+1 : res);
	}
};
```
牛顿迭代法【挖坑】

## [367. 有效的完全平方数 - 力扣（LeetCode）](https://leetcode.cn/problems/valid-perfect-square/description/)

## 代码

