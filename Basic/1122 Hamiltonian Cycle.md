# **1122** **Hamiltonian Cycle** 

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<string.h>
#include<set>
#include<math.h>
using namespace std;
const int maxN=200+5;
int n,arr[maxN][maxN]={0},m;
int main(){
    scanf("%d %d",&n,&m);
    int x,y;
    for(int i=0;i<m;i++){
        scanf("%d %d",&x,&y);
        arr[x][y]=arr[y][x]=1;
    }
    int k,start,pre,len;
    scanf("%d",&k);
    for(int i=0;i<k;i++){
        int flag=1,vis[maxN]={0};
        scanf("%d %d",&len,&start);
        pre=start;
        if(len!=n+1)flag=0;
        for(int j=1;j<len;j++){
            scanf("%d",&x);
            vis[x]++;
            if(!arr[x][pre])flag=0;
            pre=x;
        }
        if(pre!=start)flag=0;
        if(flag){
            for(int i=1;i<=n;i++){
                if(vis[i]==2&&i==start)continue;
                if(vis[i]!=1){
                    flag=0;
                    break;
                }
            }
        }
        if(!flag){
            printf("NO\n");
        }else{
            printf("YES\n");
        }
    }
    return 0;
}
```

