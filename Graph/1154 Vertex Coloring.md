# 1154 **Vertex Coloring** 

```c++
#include <iostream>
#include <string>
#include <vector>
#include <unordered_set>
#include <algorithm>
using namespace std;
const int maxN=1e4+5;
int n,m,k;
int l[maxN],r[maxN];
int main() {
    scanf("%d %d",&n,&m);
    int x,y;
    for(int i=0;i<m;i++){
        scanf("%d %d",&x,&y);
        l[i]=x;r[i]=y;
    }
    scanf("%d",&k);
    for(int i=0;i<k;i++){
        int flag=1,color[maxN]={0};
        unordered_set<int> property;
        for(int j=0;j<n;j++){
            scanf("%d",&color[j]);
            property.insert(color[j]);
        }
        for(int j=0;j<m;j++){
            if(color[l[j]]==color[r[j]]){
                flag=0;break;
            }
        }
        
        if(!flag){
            printf("No\n");
        }else{
            printf("%d-coloring\n",(int)property.size());
        }
    }
    return 0;
}
```

