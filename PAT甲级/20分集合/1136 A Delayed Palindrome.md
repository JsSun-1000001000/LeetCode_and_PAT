翻译题干：
给一个n然后讲n和n的回文串相加看是不是回文串，是就输出，10步之内都不是就返回不是。
输入：
n
输出：
n+n回=a
a+a回=b
...直到相加结果出现回文串（10步以内）
## 分析：
1 将字符串倒置与原字符串⽐较看是否相等可知s是否为回⽂串
2 字符串s和它的倒置t相加，只需从头到尾相加然后再倒置（记得要处理最后⼀个进位carry，如果有进位要在末尾+’1’）
3 倒置可采⽤algorithm头⽂件⾥⾯的函数reverse(s.begin(), s.end())直接对s进⾏倒置
## 代码：