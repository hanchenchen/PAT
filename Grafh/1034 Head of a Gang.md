# **1034** **Head of a Gang** 

`Hash`+`DFS`

```c++
#include<iostream>
#include<vector>
#include<map>
#include<string.h>
using namespace std;
const int MAX=26*26*26+1;
int vis[MAX]={0};
int w[MAX]={0};
vector<int> calls[MAX];
string getname(int x){
    string s;
    while(x>0){
        s=(char)(x%26+'A')+s;
        x/=26;
    }
    while(s.size()<3)s='A'+s;
    return s;
}
int getnum(string s){
    int num=0;
    for(int i=0;i<3;i++){
        num*=26;
        num+=(s[i]-'A');
    }
    return num;
}
void dfs(int x,int &weight,int &member,int &head,int &head_weight){
    if(vis[x])return;
    vis[x]=1;
    weight+=w[x];
    member++;
    if(w[x]>head_weight){
        head=x;head_weight=w[x];
    }
    for(int i=0;i<calls[x].size();i++){
        if(!vis[calls[x][i]]){
            dfs(calls[x][i],weight,member,head,head_weight);
        }
    }
}
int main(){
    int n,k;
    cin>>n>>k;k*=2;
    //memset(calls,0,sizeof(calls));
    string a,b;int t;
    for(int i=0;i<n;i++){
        cin>>a>>b>>t;
        int x=getnum(a);
        int y=getnum(b);
        w[x]+=t;
        w[y]+=t;
        calls[x].push_back(y);
        calls[y].push_back(x);
    }
    int count=0;
    map<string,int> out;
    for(int i=0;i<MAX;i++){
        if(!vis[i]){
            int weight=0,member=0,head=i,head_weight=w[i];
            dfs(i,weight,member,head,head_weight);
            if(weight<=k||member<3)continue;
            count++;
            out.insert(pair<string,int>(getname(head),member));
        }
    }
    cout<<count<<endl;
    if(!count)return 0;
    map<string,int>::iterator iter;
    for(iter=out.begin();iter!=out.end();iter++){
        cout<<iter->first<<" "<<iter->second<<endl;
    }
    return 0;
}


```

