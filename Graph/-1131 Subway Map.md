# **1131** **Subway Map** 

1. `DFS`

   时而超时..

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<vector>
   #include<map>
   #include<queue>
   #include<math.h>
   using namespace std;
   const int maxX=10005;
   vector<int> station[maxX];
   int n,m,k,line[maxX][maxX];
   int vis[maxX],start,distination,ansLen=2147483647,ansTransfer=0;
   vector<int> ans,temp;
   int transfer(){
       int x=0;
       for(int i=1;i<temp.size()-1;i++){
           if(line[temp[i-1]][temp[i]]!=line[temp[i+1]][temp[i]])
               x++;
       }
       return x;
   }
   void dfs(int x,int len){
       if(len>ansLen)return;
       if(x==distination){
           if(len<ansLen){
               ans=temp;
               ansLen=len;
               ansTransfer=transfer();
           }else if(len==ansLen){
               int mid=transfer();
               if(mid<ansTransfer){
                   ansTransfer=mid;
                   ans=temp;
               }
           }
           return;
       }
       for(int i=0;i<station[x].size();i++){
           if(vis[station[x][i]])continue;
           vis[station[x][i]]=1;
           temp.push_back(station[x][i]);
           dfs(station[x][i],len+1);
           temp.pop_back();
           vis[station[x][i]]=0;
       }
   }
   int main(){
       cin>>n;
       int pre,x;
       for(int i=1;i<=n;i++){
           scanf("%d %d",&m,&pre);
           for(int j=1;j<m;j++){
               scanf("%d",&x);
               station[x].push_back(pre);
               station[pre].push_back(x);
               line[x][pre]=line[pre][x]=i;
               pre=x;
           }
       }
       cin>>k;
       for(int i=0;i<k;i++){
           //fill(vis,vis+maxX,0);
           ans.clear();//temp.clear();
           ansLen=ansTransfer=2147483647;
           scanf("%d %d",&start,&distination);
           vis[start]=1;
           temp.push_back(start);
           dfs(start,0);
           temp.pop_back();
           vis[start]=0;
           pre=line[ans[0]][ans[1]];int s=start;
           printf("%d\n",ansLen);
           for(int i=1;i<ans.size()-1;i++){
               //cout<<ans[i]<<endl;
               if(pre!=line[ans[i+1]][ans[i]]){
                   printf("Take Line#%d from %04d to %04d.\n",pre,s,ans[i]);
                   pre=line[ans[i+1]][ans[i]];
                   s=ans[i];
               }
           }
           printf("Take Line#%d from %04d to %04d.\n",pre,s,distination);
       }
       return 0;
   }
   ```

2. 1

