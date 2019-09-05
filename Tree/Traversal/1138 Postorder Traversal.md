# 1138 Postorder Traversal

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<map>
#include<math.h>
using namespace std;
const int maxN=50000;
//const int int_max=2147483647;
int inorder[maxN]={0},preorder[maxN]={0};
int n,m,arr[maxN],ans=-1;
map<int,int> ifin;
void findAncestor(int inLeft,int inRight,int preLeft,int preRight){
    //cout<<inLeft<<" "<<inRight<<" "<<preLeft<<" "<<preRight<<endl;
    if(ans>0||inLeft>inRight)return;
    if(inLeft==inRight){
        if(ans<0)ans=preorder[preLeft];
        return;
    }
    int i=ifin[preorder[preLeft]];
    //while(i<=inRight&&inorder[i]!=preorder[preLeft])i++;
    findAncestor(inLeft,i-1,preLeft+1,preLeft+i-inLeft);
    findAncestor(i+1,inRight,preRight+i+1-inRight,preRight);
    if(ans<0)ans=preorder[preLeft];
}
int main(){
    cin>>n;
    for(int i=1;i<=n;i++){
        scanf("%d",&preorder[i]);
    }
    for(int i=1;i<=n;i++){
        scanf("%d",&inorder[i]);
        ifin[inorder[i]]=i;
    }
    findAncestor(1,n,1,n);
    cout<<ans<<endl;
    return 0;
}
```

