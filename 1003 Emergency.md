# 1003 Emergency

1. 先生

   ```c++
   #include <iostream>
   #include <vector>
   using namespace std;
   const int MAX_N = 500+5;
   const int INF = 1000000000;
   
   int N, M, C1, C2;
   int t[MAX_N];
   int d[MAX_N][MAX_N];
   vector<vector<int> > prevPoints;
   int spn = 0, mtn = 0;
   
   void dijkstra() {
       vector<bool> visited(N, false);
       visited[C1] = true;
       // init prevPoints
       for (int i = 0; i < N; ++i) {
           if (d[C1][i] < INF) {
               prevPoints.push_back(vector<int>(1,C1));
           } else {
               prevPoints.push_back(vector<int>(1,-1));
           }
       }
   
       for (int i = 0; i < N; ++i) {
           int closest = INF;
           int toVisit = -1;
           for (int j = 0; j < N; ++j) {
               if (!visited[j] && d[C1][j] < closest) {
                   closest = d[C1][j];
                   toVisit = j;
               }
           }
           if (toVisit != -1) {
               visited[toVisit] = true;
               for (int k = 0; k < N; k++) {
                   if (d[toVisit][k]<INF && !visited[k]) {
                       if (d[C1][k] > d[C1][toVisit]+d[toVisit][k]) {
                           d[C1][k] = d[C1][toVisit] + d[toVisit][k];
                           prevPoints[k].clear();
                           prevPoints[k].push_back(toVisit);
                       } else if (d[C1][k] == d[C1][toVisit]+d[toVisit][k]) {
                           prevPoints[k].push_back(toVisit);
                       }
                   }
               }
           } else {
               break;
           }
       }
   }
   
   void dfs(int p, int tn) {
       tn += t[p];
       if(p==C1) {
           spn++;
           mtn = tn>mtn ? tn:mtn;
       }
       for (unsigned int i = 0; i < prevPoints[p].size(); ++i) {
           if (prevPoints[p][i]!=-1) {
               dfs(prevPoints[p][i], tn);
           }
       }
   }
   
   int main() {
       // init
       for(int i=0; i<MAX_N; i++) {
           for(int j=0; j<MAX_N; j++) {
               d[i][j] = INF;
           }
       }
       // input
       cin >> N >> M >> C1 >> C2;
       for(int i=0; i<N; i++) {
           cin >> t[i];
       }
       for(int i=0; i<M; i++) {
           int a, b, c;
           cin >> a >> b >> c;
           d[a][b] = d[b][a] = c;
       }
       // solve
       dijkstra();
       /*
       for(int i=0; i<N; i++) {
           for(int j=0; j<prevPoints[i].size(); j++) {
               cout<<prevPoints[i][j]<<" ";
           }
           cout<<endl;
       }*/
       dfs(C2, 0);
       // output
       cout << spn << " " << mtn << endl;
       return 0;
   }
   ```

2. cc

   ```c++
   #include<iostream>
   #include<cstdio>
   #include<cstring>
   using namespace std;
   const int cc=501;
   int hh=2147483647;
   int n,m,c1,c2;
   int dis[cc]={0};
   int vis[cc]={0};
   int path[cc][cc]={0};
   int path_num[cc]={0};
   int city[cc]={0};
   int roads[cc][cc]={{0}};
   int paths=0,teams=0;
   void dfs(int x,int t){
       if(x==c1){
           paths++;
           teams=max(t+city[x],teams);
           return;
       }
       for(int i=0;i<path_num[x];i++){
           dfs(path[x][i],t+city[x]);
       }
   }
   int main(){
       scanf("%d %d %d %d",&n,&m,&c1,&c2);
       for(int j=0;j<n;j++){
           for(int i=0;i<n;i++){
               roads[j][i]=hh;
           }
       }
       for(int i=0;i<n;i++){
           scanf("%d",&city[i]);
       }
       int x=0,y=0;
       for(int i=0;i<m;i++){
           scanf("%d %d ",&x,&y);
           scanf("%d",&roads[x][y]);
           roads[y][x]=roads[x][y];
       }
       for(int i=0;i<n;i++){
           //roads[i][i]=0;
           dis[i]=roads[i][c1];
           
           if(dis[i]!=hh&&i!=c1){
               path[i][path_num[i]++]=c1;
           }
       }
       vis[c1]=1;
       while(!vis[c2]){
           int min_dis=hh;
           int min_city=-1;
           for(int i=0;i<n;i++){
               if(vis[i]==0&&min_dis>dis[i]){
                   min_dis=dis[i];
                   min_city=i;
               }
           }
           vis[min_city]=1;
           for(int i=0;i<n;i++){
               if(!vis[i]&&roads[i][min_city]!=hh){
                   if(min_dis+roads[i][min_city]<dis[i]){
                       dis[i]=min_dis+roads[i][min_city];
                       path_num[i]=1;
                       path[i][0]=min_city;
                   }else if(min_dis+roads[i][min_city]==dis[i]){
                       path[i][path_num[i]++]=min_city;
                   }
               }
           }
       }
       dfs(c2,0);
       printf("%d %d",paths,teams);
       
       return 0;
   }
   /*
    5 6 0 2
    1 2 1 5 3
    0 1 1
    0 2 2
    0 3 1
    1 2 1
    2 4 1
    3 4 1
    */
   
   ```

   

memset 只赋值0、-1，否则容易出错