# 1043 Is It a Binary Search Tree

1. 以BST^1^的先序遍历的次序，依次插入BST^2^，那么BST^1^==BST^2^
2. 先序遍历的结果为 ： 根 左子树（小于根） 右子树（大于等于根），找到右子树的位置，再把左子树和右子树放入递归。如果左右皆满足BST规则，则该树为BST

```c++
#include<iostream>
#include<string.h>
using namespace std;
int n,arr[1005]={0};
int l[1005],r[1005];
int flag=0;
bool bst(int left,int right){
    if(left>=right)return true;
    int index,root=left;
    for(index=left+1;arr[index]<arr[root]&&index<=right;index++);
    for(int i=index;i<=right;i++)if(arr[i]<arr[root])return false;
    if(arr[left+1]<arr[root])l[root]=left+1;
    if(index<=right)r[root]=index;
    if(bst(left+1,index-1)&&bst(index,right))return true;
    return false;
}
bool Mirror(int left,int right){
    if(left>=right)return true;
    int index,root=left;
    for(index=left+1;arr[index]>=arr[root]&&index<=right;index++);
    for(int i=index;i<=right;i++)if(arr[i]>=arr[root])return false;
    if(arr[left+1]>arr[root])l[root]=left+1;
    if(index<=right)r[root]=index;
    if(Mirror(left+1,index-1)&&Mirror(index,right))return true;
    return false;
}
void post(int index){
    if(index==-1)return;
    post(l[index]);
    post(r[index]);
    if(!flag)flag=1;
    else cout<<" ";
    cout<<arr[index];
}
int main(){
    memset(l,-1,sizeof(l));memset(r,-1,sizeof(r));
    cin>>n;
    for(int i=0;i<n;i++){
        cin>>arr[i];
    }
    if(bst(0,n-1)){flag=0;cout<<"YES"<<endl;post(0);return 0;}
    memset(l,-1,sizeof(l));memset(r,-1,sizeof(r));
    if(Mirror(0,n-1)){flag=0;cout<<"YES"<<endl;post(0);return 0;}
    cout<<"NO"<<endl;
    return 0;
}

```

