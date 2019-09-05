# **1020** Tree Traversals

```c++
//
//  main.cpp
//  1020pat
//
//  Created by cc on 2019/6/26.
//  Copyright © 2019 cc. All rights reserved.
//

#include <iostream>
#include <map>
#include <vector>
#include <queue>
using namespace std;
map<int,int> l;
map<int,int> r;
vector<int> postorder;
vector<int> inorder;
void func(int l1,int r1,int l2,int r2){
    if(l1==r1)return;
    int root=postorder[r1];
    //cout<<l1<<r1<<l2<<r2<<" "<<root<<endl;
    int p=l2;
    while(inorder[p]!=root)p++;
    //cout<<postorder[p-l2+l1-1]<<" "<<postorder[r1-1]<<endl;
    if(p!=l2){
        l.insert(pair<int,int>(root,postorder[p-l2+l1-1]));
        func(l1,p-l2+l1-1,l2,p-1);
    }
    if(p!=r2){
        r.insert(pair<int,int>(root,postorder[r1-1]));
        func(l1+p-l2,r1-1,p+1,r2);
    }
}
int main() {
    int n;
    cin>>n;
    int x;
    for(int i=0;i<n;i++){
        cin>>x;
        postorder.push_back(x);
    }
    for(int i=0;i<n;i++){
        cin>>x;
        inorder.push_back(x);
    }
    func(0,n-1,0,n-1);
    queue<int> q;
    q.push(postorder[n-1]);
    int flag=1;
    while(!q.empty()){
        int i=q.front();
        q.pop();
        if(l.find(i)!=l.end())q.push(l[i]);
        if(r.find(i)!=r.end())q.push(r[i]);
        if(flag){
            flag=0;
        }else
            cout<<" ";
        cout<<i;
    }
    
    return 0;
}

```

