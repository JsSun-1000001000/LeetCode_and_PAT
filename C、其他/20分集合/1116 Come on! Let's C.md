翻译题干：

输入：
第一行给==选手（contestants）==的总数n，随后n行给出选手id4位数；之后给一个k和k个id
输出：
冠军神秘奖 如果id不在ranklist里，输出are you kidding，如果id被checked过输出checked。
排名质数的Mystery Award，否则巧克力；rankid为1Minions奖
## 分析
注意格式、注意素数开方要强转double类型
## 代码
```cpp
#include <bits/stdc++.h>
using namespace std;
int ran[10000];
bool isprime(int a){
    if(a<=1){
        return false;
    }
    int Sqrt=sqrt((double)a);
    for(int i=2;i<=Sqrt;i++){
        if(a%i==0){
            return false;
        }
    }
    return true;
}
int main(){
    int n,k;
    cin>>n;
    for(int i=0;i<n;i++){
        int id;
        cin>>id;
        ran[id]=i+1;
    }
    cin>>k;
    set<int> ss;
    for(int i=0;i<k;i++){
        int id;
        cin>>id;
        printf("%04d: ",id);
        if(ran[id]==0){
            printf("Are you kidding?\n");
            continue;
        }
        if(ss.find(id)==ss.end()){
            ss.insert(id);
        }
        else{
            printf("Checked\n");
            continue;
        }
        if(ran[id]==1){
            printf("Mystery Award\n");
        }
        else if(isprime(ran[id])){
            printf("Minion\n");
        }
        else{
            printf("Chocolate\n");
        }
    }
    return 0;
}
```