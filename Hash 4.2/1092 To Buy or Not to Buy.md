# 1092 **To Buy or Not to Buy**

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
    int arr1[300]={0};
    for(int i=0;i<str1.size();i++){
        arr1[str1[i]]++;
    }
    int arr2[300]={0};
    for(int i=0;i<str2.size();i++){
        arr2[str2[i]]++;
    }
    int more=0,less=0;
    for(int i=0;i<300;i++){
        int x=arr1[i]-arr2[i];
        if(x>0)more+=x;
        else less-=x;
    }
    if(less){
        cout<<"No "<<less;
    }else{
        cout<<"Yes "<<more;
    }
    return 0;
}
```

