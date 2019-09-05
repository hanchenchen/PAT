# 1116 **Come on! Let's C** 

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<map>
#include<queue>
#include<math.h>
using namespace std;
const int maxN=1e4+5;
int n,m,arr[maxN]={0},x,vis[maxN]={0};
bool notPrime[maxN];
void findprime(){
    for(int i=2;i<=maxN;i++){
        if(notPrime[i])continue;
        for(int j=2;j*i<=maxN;j++){
            notPrime[j*i]=true;
        }
    }
}
int main(){
    cin>>n;
    findprime();
    notPrime[0]=notPrime[1]=true;
    for(int i=1;i<=n;i++){
        scanf("%d",&x);
        arr[x]=i;
    }
    cin>>m;
    for(int i=1;i<=m;i++){
        scanf("%d",&x);
        if(vis[x]){
            printf("%04d: Checked\n",x);
            continue;
        }
        if(arr[x]==0){
            printf("%04d: Are you kidding?\n",x);
            continue;
        }
        if(arr[x]==1){
            printf("%04d: Mystery Award\n",x);
        }else if(!notPrime[arr[x]]){
            printf("%04d: Minion\n",x);
        }else{
            printf("%04d: Chocolate\n",x);
        }
        vis[x]=1;
    }
    return 0;
}
```

