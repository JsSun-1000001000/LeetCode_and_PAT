## [225. 用队列实现栈 - 力扣（LeetCode）](https://leetcode.cn/problems/implement-stack-using-queues/description/)

## 代码
```cpp
class MyStack {
public:

    queue<int> que;
    queue<int> queHelp;

    MyStack() {
    }
    void push(int x) {
        que.push(x);
    }
    int pop() {
        int size = que.size() - 1;//-1 是把最后一个元素留下来
        while(size--){
            queHelp.push(que.front());
            que.pop();
        }
  
        int result = que.front();
        que.pop();
        que = queHelp;
        while(!queHelp.empty()){
            queHelp.pop();
        }
        return result;
    }
    int top() {
        int size = que.size() - 1;//-1 是把最后一个元素留下来
        while(size--){
            queHelp.push(que.front());
            que.pop();
        }
  
        int result = que.front();
        queHelp.push(que.front());
        que.pop();

        que = queHelp;
        while(!queHelp.empty()){
            queHelp.pop();
        }
        return result;
    }

    bool empty() {
        return que.empty();
    }
};

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack* obj = new MyStack();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->top();
 * bool param_4 = obj->empty();
 */
```

