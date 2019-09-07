# 1114 Family Property

```c++
#include <iostream>
#include <string.h>
#include <vector>
#include <math.h>
#include <algorithm>
#include <unordered_map>
#include <climits>
using namespace std;
const int maxN=1e4+5;
struct p{
    int n=0;
    double set=0,area=0;
    p(){};
    p(int x,double y,double z){
        this->n=x;this->set=y;this->area=z;
    }
};
int n,m,root[maxN]={0},vis[maxN]={0};
int getRoot(int x){
    int y=x;
    while(root[x]!=x)x=root[x];
    while(y!=x){
        int t=y;
        y=root[y];
        root[t]=x;
    }
    return x;
}
int main() {
    for(int i=0;i<maxN;i++){
        root[i]=i;
    }
    cin>>n;
    vector<p> v(n);
    int id,father,mother,k,child,r;
    for(int i=0;i<n;i++){
        cin>>id;
        vis[id]=1;
        cin>>father>>mother;
        if(father!=-1){
            vis[father]=1;
            root[max(getRoot(id),getRoot(father))]=min(getRoot(id),getRoot(father));
        }
        if(mother!=-1){
            vis[mother]=1;
            root[max(getRoot(id),getRoot(mother))]=min(getRoot(id),getRoot(mother));
        }
        cin>>k;
        for(int j=0;j<k;j++){
            cin>>child;
            vis[child]=1;
            root[max(getRoot(id),getRoot(child))]=min(getRoot(id),getRoot(child));
        }
        double set,area;
        cin>>set>>area;
        v[i]=p(id,set,area);
    }
    unordered_map<int,p> um;
    for(int i=0;i<maxN;i++){
        if(!vis[i])continue;
        //cout<<i<<" "<<getRoot(i)<<endl;
        um[getRoot(i)].n++;
    }
    for(int i=0;i<v.size();i++){
        um[getRoot(v[i].n)].set+=v[i].set;
        um[getRoot(v[i].n)].area+=v[i].area;
    }
    struct l{int id;int num;double avgSet;double avgArea;};
    vector<l> ans;
    for(auto it:um){
        ans.push_back
        ({it.first,it.second.n,it.second.set/(double)it.second.n,it.second.area/(double)it.second.n});
    }
    sort(ans.begin(),ans.end(),[](const l &a,const l &b){
        if(a.avgArea!=b.avgArea)return a.avgArea>b.avgArea;
        return a.id<b.id;
    });
    cout<<ans.size()<<endl;
    for(int i=0;i<ans.size();i++){
        printf("%04d %d %.3f %.3f\n",ans[i].id,ans[i].num,ans[i].avgSet,ans[i].avgArea);
    }
    return 0;
}
```

