# 1149 **Dangerous Goods Packaging**

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
int n,m,k;
unordered_map<int,vector<int>> arr;
int main() {
    cin>>n>>m;
    int x,y;
    for(int i=0;i<n;i++){
        cin>>x>>y;
        arr[x].push_back(y);
        arr[y].push_back(x);
    }
    for(int i=0;i<m;i++){
        cin>>k;
        int vis[maxN]={0},flag=1;
        for(int j=0;j<k;j++){
            cin>>x;
            vis[x]=1;
            for(auto it:arr[x]){
                if(vis[it]==1)flag=0;
            }
        }
        if(flag){
            cout<<"Yes"<<endl;
        }else{
            cout<<"No"<<endl;
        }
    }
    return 0;
}
```

