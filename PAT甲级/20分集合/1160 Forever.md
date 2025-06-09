翻译题干：
一个正数A有K位，满足如下条件：
1. A的各位的和是m
2. A+1的各位和是n
3. m和n的最大公约数是一个比2大的**素数**（a prime number）
输入：
第一行输入一个正数n（小于等于5）
接下来n行，每行给出一对数K（3~10位）和m（各位和1~90）
输出：
每对Km，第一行输出x（第x组）然后输出n和A，如果没有，就输出No Solution
不唯一就按照n升序排序，再不唯一就按照A升序排序。
## 思路
A和A+1的各位数字的最大公约数是比2大的素数，1001和1002的m和n为2和3最大公约为1，1009和1010的m和n最大公约为2，由此能发现满足条件的后两位只能是99==（假定两个数1087，1088，显然这两位的m=16和n=17只相差1，最大公约数只能为1，同理1089和1090的m=18和n=10只相差8，对于这一类，最大公约数只能为2，4，8，而1099的m和n相差为17，因此能满足要求的尾数至少为99。）==
（前置条件是 A 的各位数字之和为 m，A+1 的各位数字之和为 n）：
- 若 A 的末位数字不为9，那么 A+1 不会产生进位，则有 n=m+1，那么 GCD(m,n)=1，不满足题意，所以满足题意的 A 的末位数字一定为9。
- 若 A 的倒数第二位数字不为9，那么 A+1 只会产生1次进位，则有 n=m+1−9=m−8，其中-9是因为末位数字由9变为0，那么 GCD(m,n)=8，仍然不满足题意，所以满足题意的 A 的倒数第二位数字也一定为9。
## 代码
---
``` cpp
#include <iostream>
#include <vector>
#include <cmath>
#include <algorithm>
using namespace std;
struct node {
    int n, num;
    friend bool operator < (node &a, node &b) {
        if (a.n != b.n) return a.n < b.n;
        return a.num < b.num;
    }
}T;
int N, K, m, temp, sum, sum2, I, II;
vector<node> A;
int is_prime(int x) {
    if (x <= 2) return 0;
    for (int i = 2; i <= sqrt(x); i++) {
        if (x % i == 0) return 0; 
    }
    return 1;
}
int main() {
    cin >> N;
    for (int i = 1 ; i <= N; i++) {
        A.clear();
        cout << "Case " << i << '\n';
        cin >> K >> m;
        if (K * 9 < m) cout << "No Solution\n";
        else {
            temp = pow(10, K - 2);
            for (int i = temp / 10; i < temp; i++) {
                sum = 18, sum2 = 0, I = i, II = i + 1;
                while (I) {
                    sum += I % 10;
                    I /= 10;
                    if (sum > m) break;
                }
                while (II) {
                    sum2 += II % 10;
                    II /= 10;
                }
                if (sum == m && is_prime(__gcd(m, sum2))) {
                    T.n = sum2, T.num = i;
                    A.push_back(T);
                }
            }
            sort(A.begin(), A.end());
            if (A.empty()) cout << "No Solution\n";
            for (auto &it : A) {
                cout << it.n << ' ' << it.num << "99\n";
            }
        }
        
    }
    return 0;
}
```
---