# 1004 Counting Leaves

```c++
#include<stdio.h>
#include<iostream>
using namespace std;
int degree[105]={0};
int level[105]={0};
int child[105][105]={{}};
int main(){
    int n,m;
    scanf("%d",&n);
    if(n==0)return 0;
    scanf("%d",&m);
    level[1]=1;
    for(int i=0;i<m;i++){
        int root,d;
        scanf("%d %d",&root,&d);
        degree[root]=d;
        for(int j=0;j<d;j++){
            int children;
            scanf("%d",&children);
            child[root][j]=children;
        }
    }
    int flag=1;
    while(flag){
        flag=0;
        for(int i=1;i<=n;i++){
            if(level[i]==0){
                flag=1;
                continue;
            }
            for(int j=0;j<degree[i];j++){
                level[child[i][j]]=level[i]+1;
            }
        }
    }
    int ans[105]={0};
    int max_level=1;
    for(int i=1;i<=n;i++){
        if(degree[i]==0){
            ans[level[i]]++;
        }
        max_level=max(max_level,level[i]);
    }
    for(int i=1;i<=max_level;i++){
        printf("%d",ans[i]);
        if(i!=max_level)printf(" ");
        else printf("\n");
    }
    return 0;
}
```

