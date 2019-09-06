# 1125 **Chain the Ropes**

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<string.h>
#include<map>
#include<math.h>
using namespace std;
const int maxN=10000+5;
int n,arr[maxN],ans;
int main(){
    scanf("%d",&n);
    for(int i=0;i<n;i++){
        scanf("%d",&arr[i]);
    }
    sort(arr,arr+n);
    ans=arr[0];
    for(int i=1;i<n;i++){
        ans=(ans+arr[i])/2;
    }
    cout<<ans<<endl;
    return 0;
}
```

