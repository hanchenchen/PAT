# 1030 Travel Plan

`Dijkstra`+`DFS`

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

