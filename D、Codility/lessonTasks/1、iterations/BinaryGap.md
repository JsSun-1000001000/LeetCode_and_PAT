A _binary gap_ within a positive integer N is any maximal sequence of consecutive zeros that is surrounded by ones at both ends in the binary representation of N.

For example, number 9 has binary representation 1001 and contains a binary gap of length 2. The number 529 has binary representation 1000010001 and contains two binary gaps: one of length 4 and one of length 3. The number 20 has binary representation 10100 and contains one binary gap of length 1. The number 15 has binary representation 1111 and has no binary gaps. The number 32 has binary representation 100000 and has no binary gaps.

Write a function:

> int solution(int N);

that, given a positive integer N, returns the length of its longest binary gap. The function should return 0 if N doesn't contain a binary gap.

For example, given N = 1041 the function should return 5, because N has binary representation 10000010001 and so its longest binary gap is of length 5. Given N = 32 the function should return 0, because N has binary representation '100000' and thus no binary gaps.

Write an ****efficient**** algorithm for the following assumptions:

> - N is an integer within the range [1..2,147,483,647].

---
## Analysis

要两个1之间的连续0，必须是两个1之间的，1000不算。
给一个十进制数，返回对应二进制数的最长连续0

## Code
```cpp
// you can use includes, for example:
// #include <algorithm>
// you can write to stdout for debugging purposes, e.g.
// cout << "this is a debug message" << endl;

#include <stack>
int solution(int N) {
    // Implement your solution here
    //先把二进制数剥离出来
    //最高位一定是1 除非他是0 从最高位看 是0直接返回
    //两个参数记录，一个记录到下一个1之间有多少0，一个记录当前最大数量0
    //如果最后一位是0，最后一次统计不算数
    //可以看出 用栈会比较有意思
    stack<int> binarynum;
    int count = 0;
    int max0 = 0;
    if(N == 0 || N == 1){
        return max0;
    }
    while(N){
        int bt = N % 2;
        binarynum.push(bt);
        N = N / 2;
    }
    while(!binarynum.empty()){
        if(binarynum.top() == 1){
            max0 = max(max0, count);
            binarynum.pop();
            count = 0;
        }
        else{
            count++;
            binarynum.pop();
        }
    }
    return max0;
}
```