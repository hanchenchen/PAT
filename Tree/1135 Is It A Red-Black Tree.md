1135 Is It A Red-Black Tree

1. 红黑树也是二叉查找树

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<vector>
   #include<map>
   #include<queue>
   #include<math.h>
   using namespace std;
   struct NODE{
       int val;
       NODE *left,*right;
   };
   int n,k,preorder[50],ifpath=1;
   void build(int x,NODE* &node){
       if(node!=NULL){
           if(abs(x)<abs(node->val)){
               build(x,node->left);
           }else{
               build(x,node->right);
           }
       }else{
           node=new NODE();
           node->val=x;
       }
   }
   bool judge1(NODE* &node){
       if(node==NULL)return true;
       if(node->val<0){
           if(node->left&&node->left->val<0)return false;
           if(node->right&&node->right->val<0)return false;
       }
       return judge1(node->left)&&judge1(node->right);
   }
   int getNum(NODE* &node){
       if(node==NULL)return 0;
       int l=getNum(node->left);
       int r=getNum(node->right);
       if(l!=r)ifpath=0;
       return l+(node->val>0);
   }
   int main(){
       cin>>k;
       for(int j=0;j<k;j++){
           cin>>n;
           NODE *root=NULL;ifpath=1;
           for(int i=0;i<n;i++){
               scanf("%d",&preorder[i]);
               build(preorder[i], root);
           }
           getNum(root);
           if(judge1(root)&&ifpath&&preorder[0]>0){
               cout<<"Yes"<<endl;
           }else{
               cout<<"No"<<endl;
           }
       }
       return 0;
   }
   ```

   

