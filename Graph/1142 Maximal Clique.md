# **1142** **Maximal Clique**

```c++
#include <iostream>
#include <string.h>
#include <vector>
#include <math.h>
#include <algorithm>
#include <unordered_map>
#include <climits>
using namespace std;
const int maxNv=200+5;
int nv,ne,m,arr[maxNv][maxNv];
int main() {
    cin>>nv>>ne;
    int x,y;int i=0;
    memset(arr,0,sizeof(arr));
    for(;i<ne;i++){
        cin>>x>>y;
        arr[x][y]=arr[y][x]=1;
    }
    int m;
    cin>>m;
    for(i=0;i<m;i++){
        int k; cin>>k;
        vector<int> v(k);int vis[maxNv]={0};
        for(int j=0;j<k;j++){
            cin>>v[j];
            vis[v[j]]=1;
        }
        int ifClique=1,ifMaximal=0;
        for(int j=0;j<k;j++){
            for(int q=1;q<=nv;q++){
                if(arr[v[j]][q])vis[q]++;
            }
        }
        for(int j=0;j<k;j++){
            //cout<<" "<<vis[v[j]];
            if(vis[v[j]]!=k)ifClique=0;
        }
        if(!ifClique){
            printf("Not a Clique\n");
            continue;
        }
        for(int q=1;q<=nv;q++){
            if(vis[q]==k)ifMaximal++;
        }
        if(ifMaximal==k){
            printf("Yes\n");
        }else{
            printf("Not Maximal\n");
        }
    }
    return 0;
}
```

