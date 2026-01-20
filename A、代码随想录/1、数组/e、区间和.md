区间和要用到==前缀和==

注意：前缀和不能暴力，极端查询的话时间复杂度特别大

前缀和的思想是==**重复利用计算过的子数组之和，降低区间查询需要累加计算的次数。**==

要求区间和，直接右边界的前缀和-左边界的前缀和=区间和 

大量输入输出，最好用`scanf printf`耗时小

## [58. 区间和（第九期模拟笔试）](https://kamacoder.com/problempage.php?pid=1070)

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main(){
    int n;
    int a,b;
    scanf("%d",&n);

    vector<int> vec(n);
    vector<int> p(n);
    int presum = 0;
    for(int i = 0; i < n; i++){
        scanf("%d",&vec[i]);
        presum += vec[i];
        p[i] = presum;
    }

    while(~scanf("%d%d",&a,&b)){
        int sum;
        if(a == 0){
            sum = p[b];
        }
        else{
            sum = p[b]-p[a-1];
        }
        printf("%d\n",sum);
    }
    return 0;
}
```