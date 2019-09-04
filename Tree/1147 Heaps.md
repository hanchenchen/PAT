# 1147 Heaps

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<map>
#include<math.h>
using namespace std;
const int maxN=1e3+5;
const int int_max=2147483647;
int levelOrder[maxN]={0};
int n,m,arr[maxN];
bool ifMaxHeap(int x){
    if(x>n)return true;
    if(2*x<=n&&levelOrder[2*x]>levelOrder[x])return false;
    if(2*x+1<=n&&levelOrder[2*x+1]>levelOrder[x])return false;
    return ifMaxHeap(2*x)&&ifMaxHeap(2*x+1);
}
bool ifMinHeap(int x){
    if(x>n)return true;
    if(2*x<=n&&levelOrder[2*x]<levelOrder[x])return false;
    if(2*x+1<=n&&levelOrder[2*x+1]<levelOrder[x])return false;
    return ifMinHeap(2*x)&&ifMinHeap(2*x+1);
}
void postorderTraversal(int x){
    if(x>n)return;
    postorderTraversal(x*2);
    postorderTraversal(x*2+1);
    cout<<levelOrder[x]<<" ";
}
int main(){
    cin>>m>>n;
    for(int i=0;i<m;i++){
        for(int j=1;j<=n;j++){
            scanf("%d",&levelOrder[j]);
        }
        if(ifMaxHeap(1)){
            cout<<"Max Heap"<<endl;
        }else if(ifMinHeap(1)){
            cout<<"Min Heap"<<endl;
        }else{
            cout<<"Not Heap"<<endl;
        }
        postorderTraversal(2);
        postorderTraversal(3);
        cout<<levelOrder[1]<<endl;
    }
    return 0;
}

```

