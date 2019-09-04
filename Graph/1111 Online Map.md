# 1111 **Online Map**

`Dijkstra*2`

```c++
#include<iostream>
#include<algorithm>
#include<vector>
using namespace std;
const int maxN=505;
const int int_max=2147483647;
int length[maxN][maxN];
int costTime[maxN][maxN];
int shortPath[maxN]={0},fastPath[maxN]={0};
int dis[maxN]={0},t[maxN]={0},intersection[maxN]={0},vis[maxN]={0};
int n,m,start,distinction;
void dijkstra1(){
    fill(vis,vis+maxN,0);
    fill(shortPath,shortPath+maxN,-1);
    fill(dis,dis+maxN,int_max);
    fill(t,t+maxN,int_max);
    //fill(intersection,intersection+maxN,int_max);
    dis[start]=0;
    t[start]=0;
    shortPath[start]=start;
    for(int i=0;i<n;i++){
        int mini=int_max,pos=-1;
        for(int j=0;j<n;j++){
            if(!vis[j]&&dis[j]<mini){
                mini=dis[j];
                pos=j;
            }
        }
        if(pos==-1)break;
        //cout<<pos<<endl;
        vis[pos]=1;
        for(int j=0;j<n;j++){
            if(vis[j]||length[pos][j]==int_max)continue;
            if(dis[j]>dis[pos]+length[pos][j]){
                dis[j]=dis[pos]+length[pos][j];
                shortPath[j]=pos;
                t[j]=t[pos]+costTime[pos][j];
            }else if(dis[j]==dis[pos]+length[pos][j]){
                if(t[j]>t[pos]+costTime[pos][j]){
                    shortPath[j]=pos;
                    t[j]=t[pos]+costTime[pos][j];
                }
            }
        }
    }
}
void dijkstra2(){
    fill(vis,vis+maxN,0);
    fill(fastPath,fastPath+maxN,-1);
    fill(intersection,intersection+maxN,int_max);
    fill(t,t+maxN,int_max);
    intersection[start]=0;
    t[start]=0;
    fastPath[start]=start;
    for(int i=0;i<n;i++){
        int mini=int_max,pos=-1;
        for(int j=0;j<n;j++){
            if(!vis[j]&&t[j]<mini){
                mini=t[j];
                pos=j;
            }
        }
        if(pos==-1)break;
        vis[pos]=1;
        for(int j=0;j<n;j++){
            if(vis[j]||costTime[pos][j]==int_max)continue;
            if(t[j]>t[pos]+costTime[pos][j]){
                intersection[j]=intersection[pos]+1;
                fastPath[j]=pos;
                t[j]=t[pos]+costTime[pos][j];
            }else if(t[j]==t[pos]+costTime[pos][j]){
                if(intersection[j]>intersection[pos]+1){
                    intersection[j]=intersection[pos]+1;
                    fastPath[j]=pos;
                }
            }
        }
    }
}
int main(){
    fill(length[0],length[0]+maxN*maxN,int_max);
    fill(costTime[0],costTime[0]+maxN*maxN,int_max);
    cin>>n>>m;
    int v1,v2,one;
    for(int i=0;i<m;i++){
        scanf("%d %d %d",&v1,&v2,&one);
        scanf("%d %d",&length[v1][v2],&costTime[v1][v2]);
        if(!one){
            length[v2][v1]=length[v1][v2];
            costTime[v2][v1]=costTime[v1][v2];
        }
    }
    
    cin>>start>>distinction;
    dijkstra1();
    int i=distinction;
    vector<int> ans1;
    ans1.insert(ans1.begin(),distinction);
    while(i!=start){
        i=shortPath[i];
        ans1.insert(ans1.begin(),i);
        //cout<<"->"<<i;
    }
    
    dijkstra2();
    i=distinction;
    vector<int> ans2;
    ans2.insert(ans2.begin(),distinction);
    while(i!=start){
        i=fastPath[i];
        ans2.insert(ans2.begin(),i);
        //cout<<"->"<<i;
    }
    if(ans1==ans2){
        cout<<"Distance = "<<dis[distinction]<<"; Time = "<<t[distinction]<<": "<<ans1[0];
        for(int i=1;i<ans1.size();i++){
            cout<<" -> "<<ans1[i];
        }
    }else{
        cout<<"Distance = "<<dis[distinction]<<": "<<ans1[0];
        for(int i=1;i<ans1.size();i++){
            cout<<" -> "<<ans1[i];
        }
        cout<<endl;
        cout<<"Time = "<<t[distinction]<<": "<<ans2[0];
        for(int i=1;i<ans2.size();i++){
            cout<<" -> "<<ans2[i];
        }
    }
    return 0;
}
```

