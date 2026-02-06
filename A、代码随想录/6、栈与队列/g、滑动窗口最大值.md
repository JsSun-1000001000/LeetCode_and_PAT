## [239. 滑动窗口最大值 - 力扣（LeetCode）](https://leetcode.cn/problems/sliding-window-maximum/description/)

hard~

## 代码

```cpp
class Solution {
private:
    class myqueue{
    public:
        deque<int> que;
        void pop(int val){
            if(!que.empty() && val == que.front()){
                que.pop_front();
            }
        }

        void push(int val){
            while(!que.empty() && val > que.back()){
                que.pop_back();
            }
            que.push_back(val);
        }

        int front(){
            return que.front();
        }
    };

public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        //给滑动窗口用
        myqueue que;
        //存最大值
        vector<int> res;
        //k个数压入队列
        for(int i = 0; i < k; i++){
            que.push(nums[i]);
        }
  
        res.push_back(que.front());

        for(int i = k; i < nums.size(); i++){
            que.pop(nums[i - k]);
            que.push(nums[i]);//滑动窗口挪动一格
            res.push_back(que.front());//记录对应的最大值
        }
        return res;
    }
};
```