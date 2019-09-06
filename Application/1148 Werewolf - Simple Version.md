# 1148 **Werewolf - Simple Version**

```c++
#include <iostream>
#include <string>
#include <vector>
#include <math.h>
#include <algorithm>
using namespace std;
const int maxN=1e2+5;
int n,arr[maxN]={0};
int main() {
    cin>>n;
    for(int i=1;i<=n;i++){
        cin>>arr[i];
    }
    for(int i=1;i<=n;i++){
        for(int j=i+1;j<=n;j++){
            int whoLie[maxN]={0};
            for(int k=1;k<=n;k++){
                if(arr[k]<0){
                    if(-arr[k]!=i&&-arr[k]!=j)whoLie[k]++;
                }else{
                    if(arr[k]==i||arr[k]==j)whoLie[k]++;
                }
            }
            int wolfLie=whoLie[i]+whoLie[j],humanLie=0;
            for(int k=1;k<=n;k++){
                if(k==i||k==j)continue;
                if(whoLie[k])humanLie++;
            }
            if(wolfLie==1&&humanLie==1){
                cout<<i<<" "<<j<<endl;
                return 0;
            }
        }
    }
    cout<<"No Solution"<<endl;
    return 0;
}
```

