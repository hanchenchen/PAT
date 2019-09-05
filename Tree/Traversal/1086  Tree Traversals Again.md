# 1086  **Tree Traversals Again** 

```c++
#include<iostream>
#include<stack>
#include<string.h>
using namespace std;
int l[35][2]={0};
int if_out=0;
void func(int root){
    if(root==0)return;
    if(l[root][0])func(l[root][0]);
    if(l[root][1])func(l[root][1]);
    if(if_out)cout<<" ";
    else if_out=1;
    cout<<root;
}
int main(){
    memset(l,0,sizeof(l));
    int n,node,lr=0,x;
    string s;
    stack<int> st;
    cin>>n;
    cin>>s>>node;
    int root=node;
    st.push(node);
    for(int i=1;i<2*n;i++){
        cin>>s;
        if(s=="Push"){
            cin>>x;
            l[node][lr]=x;
            node=x;
            st.push(x);
            lr=0;
        }else{
            node=st.top();
            lr=1;
            st.pop();
        }
    }
    func(l[root][0]);
    func(l[root][1]);
    if(if_out)cout<<" ";
    else if_out=1;
    cout<<root;
    return 0;
}

```

