# **1067** **Sort with Swap(0, i)**

```c++
#include<iostream>
#include<map>
#include<vector>
#include<string.h>
#include<set>
#include<algorithm>
using namespace std;
const int maxN=100005;
//const int maxInt=2147483647;
/*
struct STU{
    double price=0.0,amount=0.0;
}stu[maxN];//*/
int n,ans,arr[maxN],pos[maxN];
int main(){
    cin>>n;
    int ans=0;
    set<int> q;
    for(int i=0;i<n;i++){
        scanf("%d",&arr[i]);
        pos[arr[i]]=i;
        if(arr[i]!=i&&arr[i]>0)q.insert(arr[i]);
    }
    while(!q.empty()){
        if(pos[0]==0){
            pos[0]=pos[*q.begin()];
            pos[*q.begin()]=0;
            //q.erase(q.begin());
        }else{
            int x=pos[0];
            pos[0]=pos[x];
            pos[x]=x;
            q.erase(x);
            //cout<<x<<endl;
        }
        ans++;
    }
    printf("%d",ans);
    return 0;
}

```

