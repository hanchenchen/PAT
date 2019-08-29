# 1030 Travel Plan

## `Dijkstra`+`DFS`

| Submit Time         | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
| ------------------- | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
| 8/29/2019, 14:10:03 | Accepted | 30    | [1030](https://pintia.cn/problem-sets/994805342720868352/problems/994805464397627392) | C++ (g++) | 7 ms     | cc   |

| Case | Result   | Run Time | Memory  |
| ---- | -------- | -------- | ------- |
| 0    | Accepted | 4 ms     | 352 KB  |
| 1    | Accepted | 4 ms     | 424 KB  |
| 2    | Accepted | 7 ms     | 2304 KB |

```c++
#include<iostream>
#include<vector>
#include<queue>
#include<string.h>
using namespace std;
int road[505][505];
vector<int> path[505];
int cost[505][505]={0};
int dis[505]={0};
int vis[505]={0};
const int MAX=1e9;
int n,m,s,d;
vector<int> ans;
int amount=MAX;
vector<int> v;
void findPath(int x,int amountTemp){
    if(x==s){
        if(amount>amountTemp)
        {
            amount=amountTemp;
            ans=v;
        }
        return ;
    }
    for(int i=0;i<path[x].size();i++){
        v.push_back(path[x][i]);
        findPath(path[x][i],amountTemp+cost[path[x][i]][x]);
        v.pop_back();
    }
    
}
int main(){
    
    cin>>n>>m>>d>>s;
    for(int i=0;i<n;i++){
        dis[i]=MAX;
        for(int j=0;j<n;j++){
            road[i][j]=MAX;
        }
    }
    int x,y;
    for(int i=0;i<m;i++){
        cin>>x>>y;
        cin>>road[x][y];
        road[y][x]=road[x][y];
        cin>>cost[x][y];
        cost[y][x]=cost[x][y];
    }
    dis[s]=0;
    vis[s]=1;
    for(int i=0;i<n;i++){
        if(road[s][i]==MAX)continue;
        dis[i]=road[s][i];
        path[i].push_back(s);
    }
    for(int i=0;i<n;i++){
        int city=-1,minDis=MAX;
        for(int j=0;j<n;j++){
            if(!vis[j]&&minDis>dis[j]){
                minDis=dis[j];
                city=j;
            }
        }
        if(city==-1||city==d)break;
        vis[city]=1;
        for(int j=0;j<n;j++){
            if(vis[j]||road[city][j]==MAX)continue;
            if(dis[j]>road[city][j]+minDis){
                path[j].clear();
                dis[j]=road[city][j]+minDis;
                path[j].push_back(city);
            }else if(dis[j]==road[city][j]+minDis){
                path[j].push_back(city);
            }
        }
    }
    findPath(d,0);
    cout<<d;
    for(int i=0;i<ans.size();i++){
        cout<<" "<<ans[i];
    }
    cout<<" "<<dis[d]<<" "<<amount<<endl;
    return 0;
}

```

### `Dijkstra`

| Submit Time         | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
| ------------------- | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
| 8/29/2019, 14:33:59 | Accepted | 30    | [1030](https://pintia.cn/problem-sets/994805342720868352/problems/994805464397627392) | C++ (g++) | 6 ms     | cc   |

| Case | Result   | Run Time | Memory  |
| ---- | -------- | -------- | ------- |
| 0    | Accepted | 3 ms     | 416 KB  |
| 1    | Accepted | 3 ms     | 416 KB  |
| 2    | Accepted | 6 ms     | 2304 KB |

```c++
#include<iostream>
#include<vector>
#include<queue>
#include<string.h>
using namespace std;
int road[505][505];
int cost[505][505]={0};
int dis[505]={0};
int c[505]={0};
int vis[505]={0};
int path[505]={0};
const int MAX=1e9;
int n,m,s,d;
int main(){
    cin>>n>>m>>d>>s;
    for(int i=0;i<n;i++){
        dis[i]=MAX;
        for(int j=0;j<n;j++){
            road[i][j]=MAX;
        }
    }
    int x,y;
    for(int i=0;i<m;i++){
        cin>>x>>y;
        cin>>road[x][y];
        road[y][x]=road[x][y];
        cin>>cost[x][y];
        cost[y][x]=cost[x][y];
    }
    dis[s]=0;
    vis[s]=1;
    for(int i=0;i<n;i++){
        if(road[s][i]==MAX)continue;
        dis[i]=road[s][i];
        c[i]=cost[s][i];
        path[i]=s;
    }
    for(int i=0;i<n;i++){
        int city=-1,minDis=MAX;
        for(int j=0;j<n;j++){
            if(!vis[j]&&minDis>dis[j]){
                minDis=dis[j];
                city=j;
            }
        }
        if(city==-1||city==d)break;
        vis[city]=1;
        for(int j=0;j<n;j++){
            if(vis[j]||road[city][j]==MAX)continue;
            if(dis[j]>road[city][j]+minDis){
                dis[j]=road[city][j]+minDis;
                path[j]=city;
                c[j]=cost[city][j]+c[city];
            }else if(dis[j]==road[city][j]+minDis){
                if(c[j]>cost[city][j]+c[city]){
                    dis[j]=road[city][j]+minDis;
                    c[j]=cost[city][j]+c[city];
                    path[j]=city;
                }
            }
        }
    }
    cout<<d;
    x=d;
    while(d!=s){
        d=path[d];
        cout<<" "<<d;
    }
    cout<<" "<<dis[x]<<" "<<c[x]<<endl;
    return 0;
}
```

