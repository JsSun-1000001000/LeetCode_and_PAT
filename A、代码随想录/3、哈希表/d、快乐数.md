
**==当我们遇到了要快速判断一个元素是否出现集合里的时候，就要考虑哈希法了
==**
## [202. 快乐数 - 力扣（LeetCode）](https://leetcode.cn/problems/happy-number/description/)

```cpp
class Solution {
public:
    int getsum(int n){
        int sum = 0;
        while(n){
            sum += (n % 10) * (n % 10);
            n = n / 10;
        }
        return sum;
    }
  
    bool isHappy(int n) {
        //用unordered set来判断是否是重复出现，
        //因为重新命中了就意味着这个数不是快乐数字
        unordered_set<int> result;
        while(1){
            //各位求和um(n);
            int sum = getsum(n);
            //special situation
            if(sum == 1){
                return true;
            }
            //放在set里比较 find返回的是迭代器，找不到会返回end
            if(result.find(sum) != result.end()){
                //如果重复出现了 就返回false
                return false;
            }
            else{
                result.insert(sum);
            }
            //求和后的结果作为新的数重新进入循环
            n = sum;
        }
    }
};
```