# 1087 All Roads Lead to Rome

1. #### ~~`Dijkstra`+`DFS`+`Hash`~~：*Memory Limit Exceeded*

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<vector>
   #include<math.h>
   #include<string.h>
   using namespace std;
   const int MAX=2147483647;
   const int maxN=26*26*26;
   int n,k;
   string starting;
   int dis[maxN];
   vector<int> path[maxN];
   int happiness[maxN];
   int happinessOfCity[maxN];
   int road[maxN][maxN];
   int vis[maxN]={0};
   string toString(int x){
       string s="";
       while(x>0){
           s=(char)(x%26+'A')+s;
           x/=26;
       }
       while(s.size()<3)s='A'+s;
       return s;
   }
   int toNum(string s){
       int x=0;
       for(int i=0;i<s.size();i++){
           x*=26;
           x+=(s[i]-'A');
       }
       return x;
   }
   int maxHappy=-1,ansNum=-1,diffrent=0;
   vector<int> route;
   vector<int> ansRoute;
   void dfs(int x,int h,int num){
       if(x==toNum("ROM")){
           diffrent++;
           if(h>maxHappy){
               maxHappy=h;
               ansRoute=route;
               ansNum=num;
           }else if(h==maxHappy&&num<ansNum){
               maxHappy=h;
               ansRoute=route;
               ansNum=num;
           }
           return;
       }
       for(int i=0;i<path[x].size();i++){
           route.push_back(path[x][i]);
           dfs(path[x][i],h+happinessOfCity[path[x][i]],num+1);
           route.pop_back();
       }
   }
   void dijkstra(int loc){
       fill(dis,dis+maxN,MAX);
       /*for(int i=1;i<=n;i++){
           dis[i]=road[loc][i];
       }*/
       memset(vis,0,sizeof(vis));
       //vis[loc]=1;
       dis[loc]=0;
       for(int i=0;i<n;i++){
           int mini=MAX,pos=-1;
           for(int j=0;j<maxN;j++){
               if(!vis[j]&&mini>dis[j]){
                   mini=dis[j];
                   pos=j;
               }
           }
           if(pos==-1)break;
           vis[pos]=1;
           for(int j=0;j<maxN;j++){
               if(vis[j]||road[pos][j]==MAX)continue;
               if(dis[j]>mini+road[pos][j]){
                   dis[j]=mini+road[pos][j];
                   path[j].clear();
                   path[j].push_back(pos);
               }else if(dis[j]==mini+road[pos][j]){
                   path[j].push_back(pos);
               }
           }
       }
   }
   
   int main(){
       cin>>n>>k>>starting;
       string a,b;int x,y;
       fill(road[0],road[0]+maxN*maxN,MAX);
       for(int i=1;i<n;i++){
           cin>>a;
           cin>>happinessOfCity[toNum(a)];
       }
       for(int i=0;i<k;i++){
           cin>>a>>b;
           x=toNum(a);
           y=toNum(b);
           cin>>road[x][y];
           road[y][x]=road[x][y];
       }
       x=toNum("ROM");
       y=toNum(starting);
       dijkstra(x);
       dfs(y,happinessOfCity[y],0);
       cout<<diffrent<<" "<<dis[y]<<" "<<maxHappy<<" "<<maxHappy/ansNum<<endl;
       cout<<toString(y);
       for(int i=0;i<ansRoute.size();i++){
           cout<<"->"<<toString(ansRoute[i]);
       }
       return 0;   
   }
   ```

2. #### `Dijkstra`+`DFS`+`Map`：==AC==

   | Submit Time         | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
   | ------------------- | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
   | 8/30/2019, 10:36:10 | Accepted | 30    | [1087](https://pintia.cn/problem-sets/994805342720868352/problems/994805379664297984) | C++ (g++) | 3 ms     | cc   |

   | Case | Result   | Run Time | Memory |
   | ---- | -------- | -------- | ------ |
   | 0    | Accepted | 2 ms     | 608 KB |
   | 1    | Accepted | 2 ms     | 512 KB |
   | 2    | Accepted | 2 ms     | 608 KB |
   | 3    | Accepted | 3 ms     | 512 KB |
   | 4    | Accepted | 3 ms     | 640 KB |

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<vector>
   #include<map>
   #include<math.h>
   #include<string.h>
   using namespace std;
   const int MAX=2147483647;
   const int maxN=220;
   int n,k;
   string starting;
   int dis[maxN];
   vector<int> path[maxN];
   int happiness[maxN];
   int happinessOfCity[maxN];
   int road[maxN][maxN];
   int vis[maxN]={0};
   map<string,int> cityIndex;
   map<int,string> indexCity;
   int maxHappy=-1,ansNum=-1,diffrent=0;
   vector<int> route;
   vector<int> ansRoute;
   void dfs(int x,int h,int num){
       if(x==cityIndex["ROM"]){
           diffrent++;
           if(h>maxHappy){
               maxHappy=h;
               ansRoute=route;
               ansNum=num;
           }else if(h==maxHappy&&num<ansNum){
               maxHappy=h;
               ansRoute=route;
               ansNum=num;
           }
           return;
       }
       for(int i=0;i<path[x].size();i++){
           route.push_back(path[x][i]);
           dfs(path[x][i],h+happinessOfCity[path[x][i]],num+1);
           route.pop_back();
       }
   }
   void dijkstra(int loc){
       fill(dis,dis+maxN,MAX);
       /*for(int i=1;i<=n;i++){
           dis[i]=road[loc][i];
       }*/
       memset(vis,0,sizeof(vis));
       //vis[loc]=1;
       dis[loc]=0;
       for(int i=0;i<n;i++){
           int mini=MAX,pos=-1;
           for(int j=0;j<maxN;j++){
               if(!vis[j]&&mini>dis[j]){
                   mini=dis[j];
                   pos=j;
               }
           }
           if(pos==-1||pos==cityIndex[starting])break;
           vis[pos]=1;
           for(int j=0;j<maxN;j++){
               if(vis[j]||road[pos][j]==MAX)continue;
               if(dis[j]>mini+road[pos][j]){
                   dis[j]=mini+road[pos][j];
                   path[j].clear();
                   path[j].push_back(pos);
               }else if(dis[j]==mini+road[pos][j]){
                   path[j].push_back(pos);
               }
           }
       }
   }
   int main(){
       cin>>n>>k>>starting;
       string a,b;int x,y;
       fill(road[0],road[0]+maxN*maxN,MAX);
       for(int i=1;i<n;i++){
           cin>>a;
           cityIndex[a]=i;
           indexCity[i]=a;
           cin>>happinessOfCity[i];
       }
       for(int i=0;i<k;i++){
           cin>>a>>b;
           x=cityIndex[a];
           y=cityIndex[b];
           cin>>road[x][y];
           road[y][x]=road[x][y];
       }
       x=cityIndex["ROM"];
       y=cityIndex[starting];
       dijkstra(x);
       dfs(y,happinessOfCity[y],0);
       cout<<diffrent<<" "<<dis[y]<<" "<<maxHappy<<" "<<maxHappy/ansNum<<endl;
       cout<<starting;
       for(int i=0;i<ansRoute.size();i++){
           cout<<"->"<<indexCity[ansRoute[i]];
       }
       return 0;   
   }
   ```

3. `Dijkstra`+`Map`：==AC==

   | Submit Time         | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
   | ------------------- | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
   | 8/30/2019, 10:52:15 | Accepted | 30    | [1087](https://pintia.cn/problem-sets/994805342720868352/problems/994805379664297984) | C++ (g++) | 3 ms     | cc   |

   | Case | Result   | Run Time | Memory |
   | ---- | -------- | -------- | ------ |
   | 0    | Accepted | 2 ms     | 480 KB |
   | 1    | Accepted | 3 ms     | 552 KB |
   | 2    | Accepted | 2 ms     | 512 KB |
   | 3    | Accepted | 2 ms     | 600 KB |
   | 4    | Accepted | 3 ms     | 612 KB |

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<vector>
   #include<map>
   #include<math.h>
   #include<string.h>
   using namespace std;
   const int MAX=2147483647;
   const int maxN=220;
   int n,k;
   string starting;
   int dis[maxN];
   int path[maxN];
   int happiness[maxN];
   int happinessOfCity[maxN];
   int road[maxN][maxN];
   int vis[maxN]={0};
   int len[maxN]={0};
   int routeNum[maxN]={0};
   map<string,int> cityIndex;
   map<int,string> indexCity;
   int maxHappy=-1,ansNum=-1,diffrent=0;
   vector<int> route;
   vector<int> ansRoute;
   void dijkstra(int loc){
       fill(dis,dis+maxN,MAX);
       memset(vis,0,sizeof(vis));
       memset(routeNum,0,sizeof(routeNum));
       memset(len,0,sizeof(len));
       memset(happiness,0,sizeof(happiness));
       dis[loc]=0;
       routeNum[loc]=1;
       happiness[loc]=happinessOfCity[loc];
       for(int i=0;i<n;i++){
           int mini=MAX,pos=-1;
           for(int j=0;j<maxN;j++){
               if(!vis[j]&&mini>dis[j]){
                   mini=dis[j];
                   pos=j;
               }
           }
           if(pos==-1||pos==cityIndex[starting])break;
           vis[pos]=1;
           for(int j=0;j<maxN;j++){
               if(vis[j]||road[pos][j]==MAX)continue;
               if(dis[j]>mini+road[pos][j]){
                   dis[j]=mini+road[pos][j];
                   path[j]=pos;
                   len[j]=len[pos]+1;
                   routeNum[j]=routeNum[pos];
                   happiness[j]=happiness[pos]+happinessOfCity[j];
               }else if(dis[j]==mini+road[pos][j]){
                   routeNum[j]+=routeNum[pos];
                   if(happiness[j]<happiness[pos]+happinessOfCity[j]){
                       path[j]=pos;
                       len[j]=len[pos]+1;
                       happiness[j]=happiness[pos]+happinessOfCity[j];
                   }else if(happiness[j]==happiness[pos]+happinessOfCity[j]){
                       if(len[j]>len[pos]+1){
                           path[j]=pos;
                           len[j]=len[pos]+1;
                       }
                   }
               }
           }
       }
   }
   
   int main(){
       cin>>n>>k>>starting;
       string a,b;int x,y;
       fill(road[0],road[0]+maxN*maxN,MAX);
       for(int i=1;i<n;i++){
           cin>>a;
           cityIndex[a]=i;
           indexCity[i]=a;
           cin>>happinessOfCity[i];
       }
       for(int i=0;i<k;i++){
           cin>>a>>b;
           x=cityIndex[a];
           y=cityIndex[b];
           cin>>road[x][y];
           road[y][x]=road[x][y];
       }
       x=cityIndex["ROM"];
       y=cityIndex[starting];
       dijkstra(x);
       cout<<routeNum[y]<<" "<<dis[y]<<" "<<happiness[y]<<" "<<happiness[y]/(len[y])<<endl;
       cout<<starting;
       while(y!=x){
           y=path[y];
           cout<<"->"<<indexCity[y];
       }
       return 0;
   }
   ```

4. 1

   

   