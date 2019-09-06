# 1146 **Topological Order**

```
#include <iostream>
#include <string.h>
#include <vector>
#include <math.h>
#include <algorithm>
#include <unordered_map>
#include <climits>
using namespace std;
const int maxN=1e3+5;
int n,m,k,inDegree[maxN]={0};
unordered_map<int,vector<int>> arr;
int main() {
    cin>>n>>m;
    int x,y;
    for(int i=0;i<m;i++){
        cin>>x>>y;
        arr[x].push_back(y);
        inDegree[y]++;
    }
    cin>>k;int ifFirst=1;
    for(int i=0;i<k;i++){
        int flag=1,mid[maxN];
        copy(inDegree,inDegree+n+1,mid);
        for(int j=0;j<n;j++){
            cin>>x;
            if(mid[x]!=0)flag=0;
            for(auto it:arr[x]){
                mid[it]--;
            }//cout<<flag;
        }
        //cout<<endl;
        if(flag){
            
        }else{
            if(ifFirst)cout<<i;
            else cout<<" "<<i;
            ifFirst=0;
        }
    }
    return 0;
}
```

