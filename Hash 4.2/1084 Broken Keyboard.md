# 1084 **Broken Keyboard** 

```c++
#include<iostream>
#include<map>
#include<vector>
#include<string.h>
#include<set>
#include<algorithm>
using namespace std;
/*
const int maxN=10005;
const int maxK=80005;
const int maxS=24*60*60;
//const int maxInt=2147483647;
struct STU{
    int times,getIn=-1;
    char id[10];
}stu[maxN];*/
//int n,k;
int main(){
    string str1,str2;
    cin>>str1>>str2;
    int j=0;
    int vis[300]={0};
    for(int i=0;i<str2.size();i++,j++){
        //cout<<str1[j];
        while(j<str1.size()&&str2[i]!=str1[j]){
            if(str1[j]<='z'&&str1[j]>='a')str1[j]=str1[j]-'a'+'A';
            if(!vis[str1[j]])cout<<str1[j];
            vis[str1[j++]]=1;
        }
    }
    while(j<str1.size()){
        if(str1[j]<='z'&&str1[j]>='a')str1[j]=str1[j]-'a'+'A';
        if(!vis[str1[j]])cout<<str1[j];
        vis[str1[j++]]=1;
    }
    return 0;
}
```

