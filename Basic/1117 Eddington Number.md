# 1117 **Eddington Number** 

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<map>
#include<queue>
#include<math.h>
using namespace std;
const int maxN=1e5+5;
int n,m,arr[maxN]={0},x,sum[maxN]={0};
int main(){
    cin>>n;
    for(int i=1;i<=n;i++){
        scanf("%d",&arr[i]);
    }
    int x;
    for(int i=n;i>0;i--){
        x=0;
        for(int j=1;j<=n;j++){
            x+=(arr[j]>i);
        }
        if(x>=i){
            cout<<i<<endl;return 0;
        }
    }
    cout<<"0"<<endl;
    return 0;
}
```

