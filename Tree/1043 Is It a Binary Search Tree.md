# 1043 Is It a Binary Search Tree

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

