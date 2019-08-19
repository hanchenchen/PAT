# 1059 Prime Factors 

1. 特殊测试用例：`1` 、质数

```c++
#include<iostream>
#include<math.h>
using namespace std;
bool ifprime(int x){
    if(x<2)return false;
    int sqr=(int)sqrt(x*1.0);
    for(int i=2;i<=sqr;i++){
        if(x%i==0)return false;
    }
    return true;
}
int main(){
    int n;
    cin>>n;
    if(ifprime(n)||n==1){
        printf("%d=%d",n,n);
        return 0;
    }
    printf("%d=",n);
    int sqr=(int)sqrt(n*1.0);
    for(int i=2;i<=sqr;i++){
        int num=0;
        if(ifprime(i)){
            while(n%i==0){num++;n/=i;}
        }
        if(num>1){
            printf("%d^%d",i,num);
        }else if(num==1){
            printf("%d",i);
        }
        if(n>1&&num!=0)printf("*");
        if(n<=1)return 0;
    }
    return 0;
}

```

