# **1150** **Travelling Salesman Problem** **(25** **point(s)****)**

```c++
#include <iostream>
#include <string.h>
#include <vector>
#include <math.h>
#include <algorithm>
#include <climits>
using namespace std;
const int maxN=200+5;
int n,m,k,arr[maxN][maxN]={0};
int main() {
    cin>>n>>m;
    int c1,c2;
    memset(arr,-1,sizeof(arr));
    for(int i=0;i<m;i++){
        cin>>c1>>c2;
        cin>>arr[c1][c2];
        arr[c2][c1]=arr[c1][c2];
    }
    cin>>k;int pathLen,x=0,pre,ansPath=-1,ansLen=INT_MAX;
    for(int i=1;i<=k;i++){
        cin>>pathLen>>pre;
        int len=0,start,vis[maxN]={0},ifDis=1,ifSimple=1,ifEvery=1,ifCycle=0;
        start=pre;
        for(int j=1;j<pathLen;j++){
            cin>>x;
            vis[x]++;
            if(arr[x][pre]>0)len+=arr[x][pre];
            else ifDis=0;
            pre=x;
        }
        for(int j=1;j<=n;j++){
            if(vis[j]>1)ifSimple=0;
            if(vis[j]==0)ifEvery=0;
        }
        ifCycle=(x==start);
        if(ifEvery&&ifDis&&ifSimple&&ifCycle){
            printf("Path %d: %d (TS simple cycle)\n",i,len);
            if(len<ansLen){
                ansLen=len;ansPath=i;
            }
        }else if(ifEvery&&ifDis&&ifCycle){
            printf("Path %d: %d (TS cycle)\n",i,len);
            if(len<ansLen){
                ansLen=len;ansPath=i;
            }
        }else if(ifDis){
            printf("Path %d: %d (Not a TS cycle)\n",i,len);
        }else{
            printf("Path %d: NA (Not a TS cycle)\n",i);
        }
    }
    printf("Shortest Dist(%d) = %d\n",ansPath,ansLen);
    return 0;
}
```

