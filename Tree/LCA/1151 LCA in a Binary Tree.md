# 1151 LCA in a Binary Tree

1. 用map记录位置，可以避免测试点四TLE

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<vector>
   #include<map>
   #include<math.h>
   using namespace std;
   const int maxN=1e4+5;
   //const int int_max=2147483647;
   int inorder[maxN]={0},preorder[maxN]={0};
   int n,m,arr[maxN];
   map<int,int> ifin;
   int findAncestor(int inLeft,int inRight,int preLeft,int preRight,int x,int y){
       if(inLeft==inRight)return inorder[inRight];
       int i=ifin[preorder[preLeft]];
       //while(i<=inRight&&inorder[i]!=preorder[preLeft])i++;
       if(x<=i&&y>=i){
           return inorder[i];
       }
       if(y<i)return findAncestor(inLeft,i-1,preLeft+1,preLeft+i-inLeft, x, y);
       else return findAncestor(i+1,inRight,preRight+i+1-inRight,preRight, x, y);
   }
   int main(){
       cin>>m>>n;
       for(int i=1;i<=n;i++){
           scanf("%d",&inorder[i]);
           ifin[inorder[i]]=i;
       }
       for(int i=1;i<=n;i++){
           scanf("%d",&preorder[i]);
       }
       for(int i=0;i<m;i++){
           int a,b;
           scanf("%d %d",&a,&b);
           bool findx=ifin[a];//(ifin.find(x)!=ifin.end());2TLE
           bool findy=ifin[b];//search(root,y);3TLE
           if(findx&&findy){
               int anc=findAncestor(1,n,1,n,min(ifin[a],ifin[b]),max(ifin[a],ifin[b]));
               if(anc==a){
                   printf("%d is an ancestor of %d.",a,b);
               }else if(anc==b){
                   printf("%d is an ancestor of %d.",b,a);
               }else{
                   printf("LCA of %d and %d is %d.",a,b,anc);
               }
           }else{
               if(!findx&&!findy){
                   printf("ERROR: %d and %d are not found.",a,b);
               }else if(!findx){
                   printf("ERROR: %d is not found.",a);
               }else{
                   printf("ERROR: %d is not found.",b);
               }
           }
           cout<<endl;
       }
       return 0;
   }
   ```

   

   