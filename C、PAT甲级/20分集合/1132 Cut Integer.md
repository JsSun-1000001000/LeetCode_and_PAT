翻译题干：
cI就是把一个k位的整数Z切割成两个整数A和B（K/2）
167334/167\*334=3，满足这个条件输出yes
输入：
n几个事例，整数Z
输出：
可以yes不可以no
## 分析
stoi函数和substr函数
## 代码
```cpp
#include <bits/stdc++.h>
using namespace std;

int main(){
    int n,m;
    cin>>n;
    for(int i=0;i<n;i++){
        cin>>m;
        string s=to_string(m);
        int len=s.length();
        int a=stoi(s.substr(0,len/2));
        int b=stoi(s.substr(len/2));
        if(a*b!=0&&m%(a*b)==0){
            cout<<"Yes"<<endl;
        }
        else{
            cout<<"No"<<endl;
        }
    }
    return 0;
}
```