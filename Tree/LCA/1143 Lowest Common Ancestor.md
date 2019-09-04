# **1143 Lowest Common Ancestor** 

1. `TLE*2`

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<vector>
   #include<map>
   #include<math.h>
   using namespace std;
   const int maxN=1e4+5;
   //const int int_max=2147483647;
   int preorder[maxN]={0};
   int n,m,arr[maxN];
   struct NODE{
       int val;
       NODE *left,*right;
   }*root;
   map<int,int> ifin;
   void insert(NODE* &node,int x){
       if(node!=NULL){
           if(x< node->val){
               return insert(node->left,x);
           }else{
               return insert(node->right,x);
           }
       }else{
           node=new NODE();
           node->val=x;
       }
   }
   bool search(NODE* &node,int x){
       if(node!=NULL){
           if(x< node->val){
               return search(node->left,x);
           }else if(x> node->val){
               return search(node->right,x);
           }else{
               return true;
           }
       }else return false;
   }
   int findAncestor(int x,int y,NODE *node){
       //if(node==NULL)return 2147483647;
       //cout<<x<<" "<<y<<" "<<node->val<<endl;
       if(x<=node->val&&y>=node->val)return node->val;
       if(x<node->val&&y<node->val)return findAncestor(x,y,node->left);
       else return findAncestor(x,y,node->right);
   }
   int main(){
       cin>>m>>n;
       int x;
       for(int i=0;i<n;i++){
           scanf("%d",&x);
           insert(root,x);
           ifin[x]=1;
       }
       for(int i=0;i<m;i++){
           int a,b;
           scanf("%d %d",&a,&b);
           int x=min(a,b),y=max(a,b);
           bool findx=(ifin.find(x)!=ifin.end());//(ifin.find(x)!=ifin.end());2TLE
           bool findy=(ifin.find(y)!=ifin.end());//search(root,y);3TLE
           if(findx&&findy){
               int anc=findAncestor(x,y,root);
               if(anc==x){
                   printf("%d is an ancestor of %d.",x,y);
               }else if(anc==y){
                   printf("%d is an ancestor of %d.",y,x);
               }else{
                   printf("LCA of %d and %d is %d.",a,b,anc);
               }
           }else{
               if(!findx&&!findy){
                   printf("ERROR: %d and %d are not found.",a,b);
               }else if(!findx){
                   printf("ERROR: %d is not found.",x);
               }else if(!findy){
                   printf("ERROR: %d is not found.",y);
               }
           }
           cout<<endl;
       }
       return 0;
   }
   ```

2. ==AC==

   ......

   BST的查找过程就是先根，后左右，和先序遍历一致。

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<vector>
   #include<map>
   #include<math.h>
   using namespace std;
   const int maxN=1e4+5;
   //const int int_max=2147483647;
   int preorder[maxN]={0};
   int n,m;
   map<int,int> ifin;
   int main(){
       cin>>m>>n;
       int x;
       for(int i=0;i<n;i++){
           scanf("%d",&preorder[i]);
           ifin[preorder[i]]=1;
       }
       for(int i=0;i<m;i++){
           int a,b;
           scanf("%d %d",&a,&b);
           int x=min(a,b),y=max(a,b);
           bool findx=(ifin.find(x)!=ifin.end());//(ifin.find(x)!=ifin.end());2TLE
           bool findy=(ifin.find(y)!=ifin.end());//search(root,y);3TLE
           if(findx&&findy){
               int anc=-1;
               for(int i=0;i<n;i++){
                   if(preorder[i]>=x&&preorder[i]<=y){anc=preorder[i];break;}
               }
               if(anc==x){
                   printf("%d is an ancestor of %d.",x,y);
               }else if(anc==y){
                   printf("%d is an ancestor of %d.",y,x);
               }else{
                   printf("LCA of %d and %d is %d.",a,b,anc);
               }
           }else{
               if(!findx&&!findy){
                   printf("ERROR: %d and %d are not found.",a,b);
               }else if(!findx){
                   printf("ERROR: %d is not found.",x);
               }else if(!findy){
                   printf("ERROR: %d is not found.",y);
               }
           }
           cout<<endl;
       }
       return 0;
   }
   ```

   