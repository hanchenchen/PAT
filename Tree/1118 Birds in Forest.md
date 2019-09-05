# 1118 Birds in Forest

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<map>
#include<queue>
#include<math.h>
using namespace std;
const int maxN=1e4+5;
int n,m,b_k,root[maxN]={0},x,birdNum=0,treeNum=0,vis[maxN]={0};
int getRoot(int x){
    int y=x;
    while(x!=root[x])x=root[x];
    root[y]=x;
    return x;
}
int main(){
    scanf("%d",&n);
    for(int i=1;i<=maxN;i++)root[i]=i;
    for(int i=0;i<n;i++){
        scanf("%d %d",&m,&x);
        birdNum=max(birdNum,x);
        for(int j=1;j<m;j++){
            scanf("%d",&b_k);
            birdNum=max(birdNum,b_k);
            //cout<<getRoot(b_k)<<" "<<b_k<<" "<<getRoot(x)<<" "<<x<<endl;
            if(getRoot(b_k)!=getRoot(x))root[getRoot(b_k)]=getRoot(x);
        }
    }
    for(int i=1;i<=birdNum;i++){
        if(vis[getRoot(i)])continue;
        vis[getRoot(i)]=1;
        treeNum++;
    }
    printf("%d %d\n",treeNum,birdNum);
    scanf("%d",&n);
    for(int i=0;i<n;i++){
        scanf("%d %d",&m,&x);
        if(getRoot(m)==getRoot(x)){
            printf("Yes\n");
        }else{
            printf("No\n");
        }
    }
    return 0;
}
```

