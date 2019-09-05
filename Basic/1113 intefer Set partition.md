# 1113 intefer Set partition

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<map>
#include<queue>
#include<math.h>
using namespace std;
const int maxN=1e5+5;
int n,arr[maxN]={0},i;
int s1,s2;
int main(){
    cin>>n;
    for(i=0;i<n;i++){
        scanf("%d",&arr[i]);
    }
    sort(arr,arr+n);
    i=0;
    for(;i<n/2;i++){
        s1+=arr[i];
    }
    for(;i<n;i++){
        s2+=arr[i];
    }
    printf("%d %d\n",n-n/2-n/2,s2-s1);
    return 0;
}
```

