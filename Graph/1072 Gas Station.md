# **1072** **Gas Station** 

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<math.h>
#include<string.h>
using namespace std;
const int MAX=2147483647;
int n,m,k,ds;
int dis[1100];
int road[1100][1100];
int vis[1100]={0};
int toNum(string s){
    if(s[0]=='G'){
        if(s.size()==2)return s[1]-'0'+n;
        if(s.size()==3)return 10+n;
    }
    int x=0;
    for(int i=0;i<s.size();i++){
        x*=10;
        x+=s[i]-'0';
    }
    return x;
}
bool dijkstra(int loc){
    fill(dis,dis+1100,MAX);
    for(int i=1;i<=n+m;i++){
        dis[i]=road[loc][i];
    }
    memset(vis,0,sizeof(vis));
    vis[loc]=1;
    dis[loc]=0;
    for(int i=0;i<n+m;i++){
        int mini=MAX,pos=-1;
        for(int j=1;j<=n+m;j++){
            if(!vis[j]&&mini>dis[j]){
                mini=dis[j];
                pos=j;
            }
        }
        if(pos==-1)return true;
        vis[pos]=1;
        for(int j=1;j<=n+m;j++){
            if(vis[j]||road[pos][j]==MAX)continue;
            if(dis[j]>mini+road[pos][j]){
                dis[j]=mini+road[pos][j];
            }
        }
    }
    return true;
}
int location=-1;double average=MAX,minimum=-1;
void ifBest(int loc){
    if(!dijkstra(loc))return;
    double averageTemp=0;
    int minimumTemp=MAX;
    for(int i=1;i<=n;i++){
        if(dis[i]>ds)return;
        if(dis[i]<minimumTemp)minimumTemp=dis[i];
        averageTemp+=1.0*dis[i];
    }
    averageTemp/=n;
    if(minimumTemp>minimum){
        location=loc;
        minimum=minimumTemp;
        average=averageTemp;
    }else if(minimumTemp==minimum&&averageTemp<average){
        location=loc;
        average=averageTemp;
    }
}
int main(){
    cin>>n>>m>>k>>ds;
    string a,b;int x,y;
    fill(road[0],road[0]+1100*1100,MAX);
    for(int i=0;i<k;i++){
        cin>>a>>b;
        x=toNum(a);
        y=toNum(b);
        cin>>road[x][y];
        road[y][x]=road[x][y];
    }
    for(int i=n+1;i<=n+m;i++){
        ifBest(i);
    }
    if(location==-1){
        cout<<"No Solution"<<endl;
        return 0;
    }
    cout<<"G"<<location-n<<endl;
    printf("%.1f %.1f\n",minimum,average);
    return 0;
}
```

