# 1066 Root of AVL Tree

1. 使用引用，可以不用修改父节点的孩子指针

2. 找最小的不平衡树

3. 数组链表

4. ```c++
   #include<iostream>
   using namespace std;
   int lost=-1;
   struct NODE{
       int val;
       int left=-1;
       int right=-1;
       int height=1;
       int factor=0;
   }node[100];
   void insert(int root,int x){
       if(node[root].val>node[x].val){
           if(node[root].left!=-1)insert(node[root].left,x);
           else {
               node[root].left=x;
           }
       }else{
           if(node[root].right!=-1)insert(node[root].right,x);
           else {
               node[root].right=x;
           }
       }
   }
   int update(int root){
       int l=0,r=0;
       if(node[root].left!=-1)l=update(node[root].left);
       if(node[root].right!=-1)r=update(node[root].right);
       node[root].height=max(l,r)+1;
       node[root].factor=l-r;
       if(lost==-1&&abs(node[root].factor)>1)lost=root;
       return node[root].height;
   }
   void rebalance(int x){
       int y,z;
       if(node[x].factor>1){
           y=node[x].left;
           if(node[y].factor>0){
               z=node[y].left;
               int temp=node[x].val;
               node[x].val=node[y].val;
               node[y].val=temp;
               node[y].left=node[y].right;
               node[y].right=node[x].right;
               node[x].left=z;
               node[x].right=y;
           }else{
               z=node[y].right;
               int temp=node[z].val;
               node[z].val=node[x].val;
               node[x].val=temp;
               
               node[y].right=node[z].left;
               node[z].left=node[z].right;
               node[z].right=node[x].right;
               
               node[x].left=y;
               node[x].right=z;
           }
       }else{
           y=node[x].right;
           if(node[y].factor<0){
               z=node[y].right;
               int temp=node[x].val;
               node[x].val=node[y].val;
               node[y].val=temp;
               node[y].right=node[y].left;
               node[y].left=node[x].left;
               node[x].right=z;
               node[x].left=y;
           }else{
               z=node[y].left;
               int temp=node[z].val;
               node[z].val=node[x].val;
               node[x].val=temp;
               
               node[y].left=node[z].right;
               node[z].right=node[z].left;
               node[z].left=node[x].left;
               
               node[x].left=z;
               node[x].right=y;
           }
       }
   }
   void preorder(int root){
       if(root==-1)return;
       cout<<node[root].val<<endl;
       cout<<" ";
       preorder(node[root].left);
       preorder(node[root].right);
   }
   int main(){
       int n=0,x;
       cin>>n;
       cin>>x;
       node[0].val=x;
       for(int i=1;i<n;i++){
           cin>>x;
           lost=-1;
           node[i].val=x;
           insert(0,i);
           update(0);
           if(lost!=-1)rebalance(lost);
           update(0);
           //preorder(0);
           //cout<<endl;
       }
       cout<<node[0].val<<endl;
   }
   ```

   

5. 