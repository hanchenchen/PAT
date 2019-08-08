# 1040 **Longest Symmetric String**

1. 一行：

   ```c++
   //1
   #include<string>
   char str[1000];
   cin.getline(str, 1000);
   int len=strlen(str);
   //2
   #include<string>
   string s;
   getline(cin,s);
   int len=s.size();
   //3
   do:scanf("%c",c) while(c!='\n')
   //4 gets()在C11标准中被删除
   ```

2. 当长度为1/2时，答案错误（但过）

```c++
#include<iostream>
#include<cstring>
#include<cstdio>
using namespace std;
int main(){
    char s[1004];
    cin.getline(s,1004);
    //int slen=strlen(s);
    int len=0;
    int slen=strlen(s);
    bool ifs[slen][slen]={{0}};
    int ans=1;
    for(int i=0;i<slen;i++){
        ifs[i][i]=true;
    }
    for(int i=0;i+1<slen;i++){
        ifs[i][i+1]=s[i]==s[i+1];
    }
    for(int len=3;len<=slen;len++){
        for(int i=0;i+len-1<slen;i++){
            int j=i+len-1;
            if(s[i]==s[j]&&ifs[i+1][j-1]){
                ifs[i][j]=true;
                ans=len;
                }
        }
    }
    printf("%d",ans);
    return 0;
}
```

