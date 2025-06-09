翻译题干：
给n个数，算出他们可能的排列组合的和
输入：
n和数
输出：
和
## 分析
==将数列中的每个数字读取到temp中，假设我们选取的⽚段中包括temp，且这个⽚段的⾸尾指针分别为p和q，那么对于p，有i种选择，即12…i，对于q，有n-i+1种选择，即i, i+1, … n，所以p和q组合形成的⾸尾⽚段有i * (n-i+1)种，因为每个⾥⾯都会出现temp，所以temp引起的总和为temp * i * (n – i+1)；遍历完所有数字，将每个temp引起的总和都累加到sum中，最后输出sum的值～==（真聪明啊真聪明柳神的脑袋瓜是怎么长得。。。）
==存在double类型累加导致的精度问题。。。存疑==
## 代码
```cpp
#include <bits/stdc++.h>
using namespace std;

int main(){
    int n;
    cin>>n;
    long long sum=0;
    double temp;
    for(int i=1;i<=n;i++){
        cin>>temp;
        sum+=(long long)(temp*1000)*i*(n-i+1);
    }
    printf("%.2f",sum/1000.0);
    return 0;
}
```