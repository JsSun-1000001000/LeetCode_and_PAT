## [347. 前 K 个高频元素 - 力扣（LeetCode）](https://leetcode.cn/problems/top-k-frequent-elements/description/)

### 我看不懂。。。还要重新看一遍，先标记一下


**所以我们要用小顶堆，因为要统计最大前k个元素，只有小顶堆每次将最小的元素弹出，最后小顶堆里积累的才是前k个最大元素。**

要求前k个高频元素，就要根绝元素出现的频率构建map，然后构建小根堆，将所有的频率压入堆中，如果堆的大小大于k了，就将元素从堆顶弹出

最后倒叙构建数组

## 代码
```cpp
class Solution {
public:
    //小根堆
    class smallheap{
    public:
        bool operator()(const pair<int,int>& lhs, const pair<int, int>& rhs){
            return lhs.second > rhs.second;
        }
    };

    vector<int> topKFrequent(vector<int>& nums, int k) {
        //统计元素出现频率
        unordered_map<int, int> map;
        for(int i = 0; i < nums.size(); i++){
            map[nums[i]]++;
        }
        //对频率排序
        //定义一个小根堆 大小为k
        priority_queue<pair<int, int>, vector<pair<int, int>>, smallheap> pri_que;
        //用固定大小为k的小根堆扫描所有频率的数值
        for(unordered_map<int, int>::iterator it = map.begin(); it != map.end(); it++){
            pri_que.push(*it);
            if(pri_que.size() > k){
                pri_que.pop();
            }
        }
        //找出前k个高频元素，因为小根堆先弹出最小的，倒叙输出到数组中
        vector<int> result(k);
        for(int i = k - 1; i >= 0; i--){
            result[i] = pri_que.top().first;
            pri_que.pop();
        }
        return result;
    }
};
```