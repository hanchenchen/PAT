# 1134 **Vertex Cover**

```c++
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
using namespace std;
const int maxN=1e4+5;
int n,m,k;
vector<int> vertics[maxN];
int main() {
    scanf("%d %d",&n,&m);
    int x,y;
    for(int i=0;i<m;i++){
        scanf("%d %d",&x,&y);
        vertics[x].push_back(i);
        vertics[y].push_back(i);
    }
    scanf("%d",&k);
    for(int i=0;i<k;i++){
        int num,vis[maxN]={0},visited=0;
        scanf("%d",&num);
        for(int j=0;j<num;j++){
            scanf("%d",&x);
            for(int k=0;k<vertics[x].size();k++){
                if(vis[vertics[x][k]]==1){
                    
                }else{
                    vis[vertics[x][k]]=1;
                    visited++;
                }
            }
        }
        if(visited==m)printf("Yes\n");
        else printf("No\n");
    }
    return 0;
}
```

