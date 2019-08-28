# **1076** **Forwards on Weibo** 

1. `DFS`最后一个测试样例会超时

2. 输入的是每个用户的关注，而非订阅者

3. `BFS`

4. ```c++
   #include<iostream>
   #include<vector>
   #include<queue>
   #include<string.h>
   using namespace std;
   vector<int> arr[1001];
   int vis[1001]={0};
   int main(){
       int n,l,m,x,k;
       cin>>n>>l;
       for(int i=1;i<=n;i++){
           cin>>m;
           for(int j=0;j<m;j++){
               cin>>x;
               arr[x].push_back(i);
           }
       }
       cin>>k;
       for(int i=0;i<k;i++){
           cin>>x;
           memset(vis,0,sizeof(vis));
           queue<int> level,qe;
           int ll=0,ans=0;
           level.push(0);qe.push(x);vis[x]=1;
           while(!qe.empty()){
               x=qe.front();qe.pop();
               
               ll=level.front();level.pop();
               if(ll>l)break;
               ans++;
               for(int i=0;i<arr[x].size();i++){
                   if(vis[arr[x][i]])continue;
                   vis[arr[x][i]]=1;
                   qe.push(arr[x][i]);
                   level.push(ll+1);
               }
           }
           cout<<ans-1<<endl;
       }
       return 0;
   }
   ```

   