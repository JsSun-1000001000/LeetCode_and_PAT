
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

```