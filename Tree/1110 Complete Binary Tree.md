# 1110 **Complete Binary Tree**

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<queue>
#include<math.h>
using namespace std;
const int maxN=25;
int n,l[maxN]={0},r[maxN]={0},father[maxN];
int tonum(string s){
    int x=0;
    for(int i=0;i<s.size();i++){
        x*=10;
        x+=s[i]-'0';
    }
    return x;
}
int main(){
    int n=0;string s;
    cin>>n;
    fill(father,father+maxN,-1);
    fill(l,l+maxN,-1);
    fill(r,r+maxN,-1);
    for(int i=0;i<n;i++){
        cin>>s;
        if(s!="-"){
            l[i]=tonum(s);
            father[l[i]]=i;
        }
        cin>>s;
        if(s!="-"){
            r[i]=tonum(s);
            father[r[i]]=i;
        }
    }
    int root=0,after=0,flag=1,last=-1;
    while(father[root]!=-1)root=father[root];
    queue<int> q;
    q.push(root);
    while(!q.empty()){
        int x=q.front();
        last=x;
        q.pop();
        if(l[x]!=-1){
            if(after)flag=0;
            q.push(l[x]);
        }else{
            after=1;
        }
        if(r[x]!=-1){
            if(after)flag=0;
            q.push(r[x]);
        }else{
            after=1;
        }
    }
    if(flag){
        cout<<"YES "<<last<<endl;
    }else{
        cout<<"NO "<<root<<endl;
    }
    return 0;
}
```

