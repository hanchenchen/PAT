# **1144** **The Missing Number**

```c++
#include <iostream>
#include <string.h>
#include <vector>
#include <math.h>
#include <algorithm>
#include <unordered_map>
#include <climits>
using namespace std;
const int maxN=1e5+5;
int n,arr[maxN],x;
int main() {
    cin>>n;
    for(int i=0;i<n;i++){
        cin>>x;
        if(x>0&&x<=n)arr[x]=1;
    }
    for(int i=1;i<=n+1;i++){
        if(arr[i]==0){
            cout<<i<<endl;
            return 0;
        }
    }
    return 0;
}
```

