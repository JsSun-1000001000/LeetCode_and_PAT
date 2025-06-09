翻译题干：
给n个数，计算它们平均值，但是要踢出一些不合法的数字。
输入：
n个
给n个数（字符）
输出：
不合法的要输出error
最后输出平均值。
## 分析
sscanf和sprintf的使用
一个是将字符串a转换为double类型的数值temp
一个是将temp格式化为两位小数的字符串b
==sscanf() – 从⼀个字符串中读进与指定格式相符的数据
sprintf() – 字符串格式化命令，主要功能是把格式化的数据写⼊某个字符串中==
## 代码
```cpp
#include <bits/stdc++.h>
using namespace std;
int main(){
    int n,cnt=0;  // n为输入的数值个数，cnt为合法数值的计数器
    char a[50],b[50];  // a存储原始输入字符串，b存储格式化后的字符串
    double temp=0.0,sum=0.0;  // temp临时存储转换后的数值，sum累加合法数值的和
    
    cin>>n;  // 读取输入的数值个数
    for(int i=0;i<n;i++){
        cin>>a;  // 读取原始输入字符串
        
        // 使用sscanf将字符串转换为double类型
        sscanf(a,"%lf",&temp);
        
        // 使用sprintf将double类型格式化为两位小数的字符串
        sprintf(b,"%.2f",temp);
        
        int flag=0;  // 标记原始字符串与格式化后的字符串是否一致
        
        // 比较原始字符串与格式化后的字符串
        for(int j=0;j<strlen(a);j++){
            if(a[j]!=b[j]){
                flag=1;  // 若存在不同字符，标记为非法
            }
        }
        
        // 判断是否为非法输入（字符串不一致或数值超出范围）
        if(flag||temp<-1000 ||temp>1000){
            printf("ERROR: %s is not a legal number\n", a);
            continue;  // 跳过当前输入，处理下一个
        }else {
            sum += temp;  // 累加合法数值
            cnt++;  // 合法数值计数加1
        }
    }
    
    // 输出结果，注意单复数和未定义情况
    if(cnt==1){
        printf("The average of 1 number is %.2f", sum);
    }
    else if(cnt>1){
        printf("The average of %d numbers is %.2f", cnt, sum / cnt);
    }
    else{
        printf("The average of 0 numbers is Undefined");
    }
    return 0;
}
```