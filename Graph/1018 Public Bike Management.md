# **1018** **Public Bike Management** 

1. 在到达时就已经使路径上每个车站达到完美状态

```c++
#include<iostream>
#include<vector>
#include<queue>
#include<string.h>
using namespace std;
int road[505][505];
vector<int> path[505];
int bike[505]={0};
int dis[505]={0};
int vis[505]={0};
const int MAX=1e9;
int c_max,n,s_p,m;
vector<int> ans;
int back=MAX;int bring=MAX;
vector<int> v;
void findPath(int x,int tempBack,int tempBring){
    tempBack+=bike[x];
    if(tempBack<0){tempBring-=tempBack;tempBack=0;}
    if(x==s_p){
        if(bring>tempBring)
        {
            back=tempBack;
            bring=tempBring;
            ans=v;
        }
        else if(bring==tempBring&&tempBack<back)
        {
            back=tempBack;
            bring=tempBring;
            ans=v;
        }        return ;
    }
    for(int i=0;i<path[x].size();i++){
        v.push_back(path[x][i]);
        findPath(path[x][i],tempBack,tempBring);
        v.pop_back();
    }
    
}
int main(){
    
    cin>>c_max>>n>>s_p>>m;
    for(int i=0;i<=n;i++){
        dis[i]=MAX;
        for(int j=0;j<=n;j++){
            road[i][j]=MAX;
        }
    }
    c_max/=2;
    for(int i=1;i<=n;i++){
        cin>>bike[i];
        bike[i]-=c_max;
    }
    int x,y,times;
    for(int i=1;i<=m;i++){
        cin>>x>>y>>times;
        road[x][y]=road[y][x]=times;
        if(x==s_p){
            dis[y]=times;
            path[y].push_back(s_p);
        }else if(y==s_p){
            dis[x]=times;
            path[x].push_back(s_p);
        }
    }
    dis[s_p]=0;
    vis[s_p]=1;
    for(int i=1;i<=n;i++){
        int city=-1,minDis=MAX;
        for(int j=0;j<=n;j++){
            if(!vis[j]&&minDis>dis[j]){
                minDis=dis[j];
                city=j;
            }
        }
        if(city==-1||city==0)break;
        vis[city]=1;
        for(int j=0;j<=n;j++){
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
    findPath(0,0,0);
    cout<<bring<<" 0";
    for(int i=0;i<ans.size();i++){
        cout<<"->"<<ans[i];
    }
    cout<<" "<<back;
    return 0;
}

```

