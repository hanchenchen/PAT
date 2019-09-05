# 1127 **ZigZagging on a Tree**

1. 数组越界有时也会导致超时

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<map>
#include<queue>
#include<math.h>
using namespace std;
const int maxN=40;
map<int,int> in;
int n,l[maxN]={0},r[maxN]={0},inorder[maxN],postorder[maxN];
int func(int il,int ir,int pl,int pr){
    if(il>ir)return -1;
    if(il==ir)return il;
    int i=in[postorder[pr]];
    l[i]=func(il,i-1,pl,pl+i-1-il);
    r[i]=func(i+1,ir,pr-1+i+1-ir,pr-1);
    return i;
}
int main(){
    int n=0;string s;
    cin>>n;
    fill(l,l+maxN,-1);
    fill(r,r+maxN,-1);
    for(int i=0;i<n;i++){
        cin>>inorder[i];
        in[inorder[i]]=i;
    }
    for(int i=0;i<n;i++){
        cin>>postorder[i];
    }
    int root=func(0,n-1,0,n-1);
    queue<int> q;vector<int> ans;
    q.push(root);q.push(-1);
    cout<<inorder[root];
    while(q.size()>1||!ans.empty()){
        int x=q.front();
        //cout<<x<<endl;
        q.pop();
        if(x<0){
            q.push(x-1);
            if((-x)%2==1){
                for(int i=(int)ans.size()-1;i>=0;i--){
                    if(ans[i]!=root)cout<<" "<<inorder[ans[i]];
                }
            }else{
                for(int i=0;i<ans.size();i++){
                    if(ans[i]!=root)cout<<" "<<inorder[ans[i]];
                }
            }
            ans.clear();
            continue;
        }
        ans.push_back(x);
        if(l[x]!=-1){
            q.push(l[x]);
        }
        if(r[x]!=-1){
            q.push(r[x]);
        }
    }
    return 0;
}
```

