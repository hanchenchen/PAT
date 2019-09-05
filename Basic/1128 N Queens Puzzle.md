# 1128 N Queens Puzzle

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<map>
#include<queue>
#include<math.h>
using namespace std;
const int maxN=1e4+5;
int n,k,visR[maxN]={0},visL[maxN]={0},vis[maxN]={0};
int main(){
    scanf("%d",&k);
    for(int i=0;i<k;i++){
        scanf("%d",&n);
        fill(vis,vis+maxN,0);
        fill(visR,visR+maxN,0);
        fill(visL,visL+maxN,0);
        int x,flag=1;
        for(int j=1;j<=n;j++){
            scanf("%d",&x);
            //cout<<x<<endl;
            if(visR[x-j+n]){
                flag=0;//break;
            }
            if(visL[x+j]){
                flag=0;//break;
            }
            if(vis[x]){
                flag=0;//break;
            }
            vis[x]=visL[x+j]=visR[x-j+n]=1;
        }
        if(flag){
            printf("YES\n");
        }else{
            printf("NO\n");
        }
    }
    return 0;
}
```

