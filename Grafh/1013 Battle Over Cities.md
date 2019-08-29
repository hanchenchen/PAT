# 1031 Battle Over Cities

1. 并查集？

2. `BFS`

   ```c++
   #include<iostream>
   #include<vector>
   #include<algorithm>
   #include<string.h>
   using namespace std;
   //const int INT_MAX=2147483647;
   int highways[1000][1000];
   int vis[1000]={0};
   int n,m,k;
   void dfs(int city,int closed){
       if(vis[city]||city==closed)return;
       vis[city]=1;
       for(int i=1;i<=n;i++){
           if(highways[city][i]&&i!=closed)
               dfs(i,closed);
       }
   }
   int main(){
       cin>>n>>m>>k;
       memset(highways,0,sizeof(highways));
       int x,y;
       for(int i=0;i<m;i++){
           cin>>x>>y;
           highways[x][y]=highways[y][x]=1;
       }
       for(int i=0;i<k;i++){
           int ans=0;
           cin>>x;
           memset(vis,0,sizeof(vis));
           for(int i=1;i<=n;i++){
               if(!vis[i]&&i!=x){
                   dfs(i,x);
                   ans++;
               }
           }
           cout<<ans-1<<endl;
       }
       return 0;
   }
   
   ```
