#  1123  Is It a Complete AVL Tree

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<queue>
#include<string.h>
#include<math.h>
using namespace std;
struct NODE{
    int val,height;
    NODE *left,*right;
}*root,*lost;
int n;
void insert(NODE * &node,int x){
    if(node!=NULL){
        if(node->val>x){
            insert(node->left,x);
        }else{
            insert(node->right,x);
        }
    }else{
        node=new NODE();
        node->val=x;
    }
}
int getFactor(NODE* &node){
    if(node->right&&node->left)
        return node->left->height-node->right->height;
    else if(node->left)
        return node->left->height;
    else if(node->right)
        return -node->right->height;
    else return 0;
}
void R(NODE* &node){
    NODE* b=node->left,*c;
    if(getFactor(b)>0){
        c=b->left;
        b->left=b->right;
        b->right=node->right;
        node->left=c;
        node->right=b;
        int temp=node->val;
        node->val=b->val;
        b->val=temp;
    }else{
        c=b->right;
        b->right=c->left;
        c->left=c->right;
        c->right=node->right;
        node->left=b;
        node->right=c;
        int temp=node->val;
        node->val=c->val;
        c->val=temp;
    }
}
void L(NODE* &node){
    NODE* b=node->right,*c;
    if(getFactor(b)<0){
        c=b->right;
        b->right=b->left;
        b->left=node->left;
        node->left=b;
        node->right=c;
        int temp=node->val;
        node->val=b->val;
        b->val=temp;
    }else{
        c=b->left;
        b->left=c->right;
        c->right=c->left;
        c->left=node->left;
        node->left=c;
        node->right=b;
        int temp=node->val;
        node->val=c->val;
        c->val=temp;
    }
}
int update(NODE* &node){
    if(node==NULL)return 0;
    int l=update(node->left);
    int r=update(node->right);
    if(l-r>1){
        R(node);
        l=update(node->left);
        r=update(node->right);
    }
    if(r-l>1){
        L(node);
        l=update(node->left);
        r=update(node->right);
    }
    node->height=max(l,r)+1;
    return node->height;
}

int main(){
    cin>>n;
    int x,flag=1,after=0;
    for(int i=0;i<n;i++){
        scanf("%d",&x);
        insert(root,x);
        update(root);
    }
    queue<NODE*> q;
    q.push(root);
    cout<<root->val;
    while(!q.empty()){
        NODE *node=q.front();
        q.pop();
        if(node->val!=root->val)cout<<" "<<node->val;
        if(node->left){
            if(after)flag=0;
            q.push(node->left);
        }
        else after=1;
        if(node->right){
            if(after)flag=0;
            q.push(node->right);
        }
        else after=1;
    }
    cout<<endl;
    if(flag){
        printf("YES\n");
    }else{
        printf("NO\n");
    }
    return 0;
}
```

