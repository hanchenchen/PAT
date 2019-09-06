# 1130 **Infix Expression** 

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<string.h>
#include<map>
#include<math.h>
using namespace std;
const int maxN=20+5;
int n,root[maxN]={0},first=1;
struct NODE{
    string val;
    int left,right;
    NODE(){left=-1;right=-1;}
    NODE(string s,int l,int r){
        this->val=s;
        this->left=l;
        this->right=r;
    }
}node[maxN];
void inorder(int x){
    if(x>n||x==-1)return;
    if(node[x].left==-1&&node[x].right==-1){
        cout<<node[x].val;
        return;
    }
    if(x!=first)cout<<"(";
    inorder(node[x].left);
    cout<<node[x].val;
    inorder(node[x].right);
    if(x!=first)cout<<")";
}
int main(){
    scanf("%d",&n);
    string s;int l,r;
    for(int i=1;i<=n;i++){
        cin>>s>>l>>r;
        node[i]=NODE(s,l,r);
        root[l]=root[r]=i;
    }
    while(root[first]!=0)first=root[first];
    inorder(first);
    return 0;
}
```

