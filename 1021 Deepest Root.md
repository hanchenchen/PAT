# 1021 Deepest Root

关于连通分量：

1. 每个连通分量中选择最小的那个作为标志，arr[n]的数组记每个节点的标志

2. 在input为每次添加一个叶子结点的条件下，可以每次判断是否添加到已添加过的连通分量

   ```c++
   int com=1;
   for(int i=0;i<n-1;i++){
                   cin>>x;cin>>y;
                   arr[x][y]=arr[y][x]=1;
                   g[x]++;g[y]++;
                   if(vis[x]&&vis[y])com++;
                   vis[x]=1;vis[y]=1;
           }
           if(com>1){
                   cout<<"Error: "<<com<<" components"<<endl;
                   return 0;
           }
   ```



```c++
//
//  main.cpp
//  1021 pat
//
//  Created by cc on 2019/7/1.
//  Copyright © 2019 cc. All rights reserved.
//

#include <iostream>
#include <vector>
#include <algorithm>
#define M 10050
using namespace std;
int arr[M][M]={0};
int n=0;
int g[M]={0};
int maxlen=0;
int func(int root,int pre){
        if(pre&&g[root]==1)return 1;
        if(arr[pre][root]>1)return arr[pre][root];
        //cout<<root<<" "<<pre<<endl;
        int re=0;
        for(int i=1;i<=n;i++){
                if(i!=pre&&arr[root][i]){
                        re=max(re,func(i,root));
                }
        }
        arr[pre][root]=re+1;
        return re+1;
}
int main(){
        cin>>n;
        int x,y;
        int com=1;
        int vis[M]={0};
        for(int i=0;i<n-1;i++){
                cin>>x;cin>>y;
                arr[x][y]=arr[y][x]=1;
                g[x]++;g[y]++;
                if(vis[x]&&vis[y])com++;
                vis[x]=1;vis[y]=1;
        }
        if(com>1){
                cout<<"Error: "<<com<<" components"<<endl;
                return 0;
        }
        for(int i=1;i<=n;i++){
                if(g[i]==1)maxlen=max(func(i,0),maxlen);
        }
        for(int i=1;i<=n;i++){
                if(arr[0][i]==maxlen)
                        cout<<i<<endl;
        }
        return 0;
}

```
