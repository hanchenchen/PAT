# **1131** **Subway Map** 

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<map>
#include<queue>
using namespace std;
const int maxN=1e4+5;
const int int_max=2147483647;
map<int,map<int,int>> lines;
//map<int,vector<int>> line;
//map<int,vector<int>> lineNum;
int n,m,start,distinction;
map<int,map<int,int>>::iterator iter;
map<int,int>::iterator c;
int main(){
    //memset(lineNum,-1,sizeof(lineNum));
    cin>>n;
    int k,pre=-1,x;
    for(int i=1;i<=n;i++){
        scanf("%d",&k);
        for(int j=0;j<k;j++){
            scanf("%d",&x);
            if(pre!=-1){
                lines[x][pre]=lines[pre][x]=i;
            }
            pre=x;
        }
        pre=-1;
    }
    scanf("%d",&m);
    for(int i=0;i<m;i++){
        cin>>distinction>>start;
        int path[maxN]={0},pathline[maxN]={0},transfer[maxN],len[maxN];
        fill(transfer,transfer+maxN,int_max);
        fill(len,len+maxN,int_max);
        fill(path,path+maxN,-1);
        queue<int> qe,l,level;
        qe.push(start);
        level.push(1);
        l.push(-1);
        len[start]={0};
        path[start]=start;
        transfer[start]=0;int minilevel=int_max;
        //cout<<start<<distinction<<endl;
        while(/*qe.front()!=distinction*/!qe.empty()){
            cout<<qe.front()<<" ";
            if(minilevel<level.front())break;
            if(qe.front()==distinction&&minilevel<int_max)minilevel=level.front();
            iter=lines.find(qe.front());
            c=iter->second.begin();
            for(;c!=iter->second.end();c++){//
                qe.push(c->first);
                l.push(c->second);
                level.push(level.front()+1);
                if(len[c->first]>len[qe.front()]+1){
                    len[c->first]=len[qe.front()]+1;
                    transfer[c->first]=transfer[qe.front()]+(c->second!=l.front());
                    path[c->first]=qe.front();
                    pathline[c->first]=c->second;
                }else if(len[c->first]==len[qe.front()]+1){
                    if(transfer[c->first]>transfer[qe.front()]+(c->second!=l.front())){
                        path[c->first]=qe.front();
                        pathline[c->first]=c->second;
                        transfer[c->first]=transfer[qe.front()]+(c->second!=l.front());
                    }
                }
            }
            qe.pop();
            l.pop();
            level.pop();
        }
        int x=distinction;
        int at=-2;
        vector<int> ans,ansLine;
        int m=0;
        while(x!=start){
            m++;
            if(at!=pathline[x]){
                at=pathline[x];
                ansLine.push_back(at);
                ans.push_back(x);
                //cout<<pathline[x]<<" "<<x<<endl;
            }
            x=path[x];
        }
        cout<<m<<endl;
        ans.push_back(x);
        for(int i=0;i<ans.size()-1;i++){
            cout<<"Take Line#"<<ansLine[i]<<" from "<<ans[i]<<" to "<<ans[i+1]<<"."<<endl;
        }
    }
    
    return 0;
}

```

