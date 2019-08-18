# 1015 Reversible Primes

```c++
#include<iostream>
#include<string.h>
using namespace std;
const int m=10000001;
int arr[m];
int reverse(int x,int radix){
    int re=0;
    while(x>0){
        re=re*radix;
        re+=(x%radix);
        x/=radix;
    }
    return re;
}
void ifprime(){
    for(int i=2;i<m;i++){
        if(arr[i]==-1){
            for(int j=2;j*i<m;j++){
                arr[j*i]=0;
            }
        }
    }
}
int main(){
    memset(arr,-1,sizeof(arr));
    arr[1]=0;
    ifprime();
    int n,d;
    while(cin>>n){
        if(n<0)return 0;
        cin>>d;
        if(arr[n]==-1&&arr[reverse(n,d)]==-1)printf("Yes\n");
        else printf("No\n");
        
    }
    return 0;
}

```

1. `1`既不属于质数也不属于合数