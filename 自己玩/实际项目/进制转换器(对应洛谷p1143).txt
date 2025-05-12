//原理:把输入的对应进制先转换为10进制，再转换为任意给定进制
#include <bits/stdc++.h>
using namespace std;
int first;//作为10进制中转站
char ans[100];//存储答案的每一位
char word[100];//以字符读入,防止超过10的进制出现字母情况
int main()
{
    int n,m,len;
    scanf("%d",&n);//输入要被转换的数的进制
    scanf("%s",word);//输入该数
    len = strlen(word);//确定位数
    first = 0;
    if(n >= 10)//如果进制大于10
    {
        for (int i = 0; i <= len-1; i++)//一位一位处理
        {
            if(word[i] >= 'A')//如果对应为字母，先转换为具体数字
            {
                first = first * n + (word[i] - 'A' + 10);
            }
            else//如果小于10，直接当作数字
            {
                first = first * n + (word[i] - '0');
            }
        }
    }
    else//如果小于十进制，正常处理
    {
        for (int i = 0; i <= len - 1; i++)
        {
            first = first * n + (word[i] - '0');
        }
    }
    scanf("%d",&m);//输入要转换成的进制
    int k;
    if(m >= 10)//如果大于10，要考虑字母
    {
        k = 0;//记录位数
        while(first)//如果还大于零，即没转换完
        {
            if(first%m>=10)//字母处理
            {
                ans[++k] = first%m + 'A' - 10;
            }
            else//正常处理
            {
                ans[++k] = first%m + '0';
            }
            first /= m;
        }
    }
    else//正常处理
    {
        k = 0;
        while(first)
        {
            ans[++k] = first%m + '0';
            first /= m;
        }
    }
    for (int i = k;i>=1;i--)//按位置倒着输出
    {
        printf("%c",ans[i]);
    }
    return 0;
}
