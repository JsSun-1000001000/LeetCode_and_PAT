翻译题干：
性感素数是一对素数primes(p,p+6)
现在给出一个整数integer 告诉我是不是性感素数
输入：给一个N ==要求小于等于10的8次方==
输出：是的话输出Yes并在另一行给出一对中的另一个素数；不是的话输出No并在另一行给出大于N的最小素数
## 思路
2 3 5 7 11 13 17 19 23 29 31 37
位数是1 和位数是7的素数 一定是一对；3-9 
先看给出的数字是不是素数？是的话根据尾数+-6看另一个是不是素数；不是素数的话找最近的素数？
写一个函数：同时返回p、p-6、p+6是不是素数，是的话Yes；不是的话从p+1开始找第一个满足的返回。
## 代码
```cpp
#include <bits/stdc++.h>

using namespace std;

int N;
int No_result;

int Judge_prime(int N){
    if(N<2){
        return 0;
    }
    for(int i=2;i<=sqrt(N);i++){
        if(N%i==0){
            return 0;
        }
    }
    return 1;
}

int main(){
    cin>>N;
    if(Judge_prime(N)&&Judge_prime(N-6)){
        cout<<"Yes"<<endl<<N-6;
    }
    else if(Judge_prime(N)&&Judge_prime(N+6)){
        cout<<"Yes"<<endl<<N+6;
    }
    else{
        for(No_result=N+1;;No_result++){
            if(Judge_prime(No_result)&&Judge_prime(No_result-6)){
                break;
            }
            if(Judge_prime(No_result)&&Judge_prime(No_result+6)){
                break;
            }
        }
        cout<<"No"<<endl<<No_result;
    }
    return 0;
}
```
## 总结
数学问题、重点在于理清题目要什么，以及素数的判断方法