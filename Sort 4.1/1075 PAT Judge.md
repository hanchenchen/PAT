# **1075** **PAT Judge**

1. 在`sort()`函数中，当`a.total_score==0`时，要把`a.solve`（成功提交过）移到前面，否则会影响排名输出

```
8 3 8
10 10 10
1 1 -1
1 2 -1
1 3 -1
1 4 0
2 1 -1
3 1 0
5 3 1
5 3 9
1 00005 9 - - 9
2 00001 0 0 0 0
2 00003 0 0 - -
```

```c++
#include<iostream>
#include<queue>
#include<vector>
#include<string.h>
#include<set>
#include<algorithm>
using namespace std;
const int maxN=10005;
const int maxK=10;
const int maxM=1e5+5;
//const int maxInt=2147483647;
struct STR{
    int id;
    int solved[maxK];
    int perfectlySolved=0;
    int solve=0;
    int total_score=0;
    STR(){
        fill(solved,solved+maxK,-10);
    }
}str[maxN];
int n,k,m,fullMark[maxK];
int main(){
    cin>>n>>k>>m;//user problem submission
    for(int i=1;i<=k;i++){
        scanf("%d",&fullMark[i]);
    }
    int x,y=0,z;
    for(int i=0;i<m;i++){
        cin>>x>>y>>z;
        //cout<<x<<y<<z<<endl;
        str[x].id=x;
        if(str[x].solved[y]<z)str[x].solved[y]=z;
        if(z>-1)str[x].solve=1;
    }
    for(int i=1;i<=n;i++){
        for(int j=1;j<=k;j++){
            if(str[i].solved[j]>0)str[i].total_score+=str[i].solved[j];
            if(str[i].solved[j]==fullMark[j])str[i].perfectlySolved++;
            if(str[i].solved[j]==-1)str[i].solved[j]=0;
        }
    }
    sort(str+1,str+n+1,[](const STR a,const STR b){
        if(a.total_score!=b.total_score)
            return a.total_score>b.total_score;
        if(a.perfectlySolved!=b.perfectlySolved)
            return a.perfectlySolved>b.perfectlySolved;
        if(a.total_score==0)return a.solve>b.solve;
        return a.id<b.id;
    });
    int r=1;
    for(int i=1;i<=n;i++){
        if(str[i].solve==0){break;}
        if(i>1&&str[i].total_score!=str[i-1].total_score){
            r=i;
        }
        printf("%d %05d %d ",r,str[i].id,str[i].total_score);
        if(str[i].solved[1]<0)printf("-");
        else printf("%d",str[i].solved[1]);
        for(int j=2;j<=k;j++){
            if(str[i].solved[j]<0)printf(" -");
            else printf(" %d",str[i].solved[j]);
        }
        printf("\n");
    }
    return 0;
}
```

