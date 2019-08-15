# **1049** **Counting Ones**

```c++
#include<iostream>
using namespace std;
int main(){
    int n,ans=0;
    int i=1;
    scanf("%d",&n);
    int x=0;
    for(int i=1;n/i>=1;i*=10){
        x=n/i;
        ans+=(x/10)*i;
        x=x%10;
        if(x>1)ans+=i;
        if(x==1){
            ans+=(n%i+1);
        }
    }
    printf("%d\n",ans);
    return 0;
}
```

