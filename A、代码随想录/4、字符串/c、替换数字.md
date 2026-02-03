## [54. 替换数字（第八期模拟笔试）](https://kamacoder.com/problempage.php?pid=1064)

## 代码
```cpp
#include <iostream>
using namespace std;

int main(){
    string s;
    while(cin >> s){
        int oldIndex= s.size() - 1;
        int count = 0;//统计 数字个数
        for(int i = 0; i < s.size(); i++){
            if(s[i] >= '0' && s[i] <= '9'){
                count++;
            }
        }
        //扩容 number 6 - 数字本身
        s.resize(s.size() + count * 5);
        int newIndex = s.size() - 1;
        //从后往前覆盖
        while(oldIndex >= 0){
            if(s[oldIndex] >= '0' && s[oldIndex] <= '9'){
                s[newIndex--] = 'r';
                s[newIndex--] = 'e';
                s[newIndex--] = 'b';
                s[newIndex--] = 'm';
                s[newIndex--] = 'u';
                s[newIndex--] = 'n';
            }
            else{
                s[newIndex--] = s[oldIndex];
            }
            oldIndex--;
        }
        cout << s << endl;
    }
    return 0;
}
```

