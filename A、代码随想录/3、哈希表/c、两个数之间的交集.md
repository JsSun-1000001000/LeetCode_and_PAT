std::set和std::multiset底层实现都是红黑树，std::unordered_set的底层实现是哈希表， 使用unordered_set 读写效率是最高的，并不需要对数据进行排序，而且还不要让数据重复，所以选择unordered_set。

## [349. 两个数组的交集 - 力扣（LeetCode）](https://leetcode.cn/problems/intersection-of-two-arrays/description/)

```cpp
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        //一个unordered set存储结果
        unordered_set<int> result;
        //另一个存储nums1
        unordered_set<int> nums1_set(nums1.begin(),nums1.end());
        //用nums2中的元素和nums1作比较
        for( int i : nums2){
            //如果在set里面出现过
            if(nums1_set.find(i) != nums1_set.end()){
                //插入result set
                result.insert(i);
            }
        }
        //返回
        return vector<int>(result.begin(),result.end());
    }
};
```

- 时间复杂度: O(n + m) m 是最后要把 set转成vector
- 空间复杂度: O(n)

