翻译题干：
给出⼀个皇后图，以这样的⽅式给出：⼀个数组包含n个数字，每个数字表⽰该列的皇后所在的⾏数～判断给出的皇后图是否满⾜不会互相攻击（任意两个皇后都要不在同⼀⾏或者同⼀列，且不在斜对⾓线上～）
输入：
k行
每行n列q，随后q1到qn
输出：
yes no
## 分析
注意判定条件，没别的了
## 代码
```cpp
#include <bits/stdc++.h>
using namespace std;

int main(){
    int k,n;
    cin>>k;
    for(int i=0;i<k;i++){
        cin>>n;
        vector<int> v(n);
        bool result=true;
        for(int j=0;j<n;j++){
            cin>>v[j];
            for(int t=0;t<j;t++){
                if(v[j]==v[t]||abs(v[j]-v[t])==abs(j-t)){
                    result=false;
                    break;
                }
            }
        }
        cout<<(result==true?"YES\n":"NO\n");
    }
    return 0;
}
```