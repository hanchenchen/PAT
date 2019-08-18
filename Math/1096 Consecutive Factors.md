# 1096 Consecutive Factors

1. 暴力

2. `n`为质数时，输出

   ```
   1
   n
   ```

```c++
#include<iostream>
#include<math.h>
using namespace std;
int main(){
    int n;
    cin>>n;
    int sqr=(int)sqrt(n*1.0);
    int ans=0;int len=0;
    for(int i=2;i<=sqr;i++){
        int temp=1;int j=i;
        for(;temp<n;j++){
            temp*=j;
            if(n%temp!=0)break;
        }
        if(len<j-i){
            len=j-i;
            ans=i;
        }
    }
    if(len==0){
        printf("1\n%d",n);
        return 0;
    }
    printf("%d\n%d",len,ans);
    for(int i=ans+1;i<ans+len;i++){
        printf("*%d",i);
    }
}

```

