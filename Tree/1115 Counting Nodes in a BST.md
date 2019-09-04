# 1115 Counting Nodes in a BST

1. 数组指针越界了，最大高度为1000，需要数组长度为2^1000^-1

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<math.h>
   using namespace std;
   const int maxN=1e6+5;
   const int int_max=2147483647;
   struct NODE{
       int val=int_max,sum=0;
   }node[maxN];
   int n,maxx=0,x;
   int getHeight(int n){
       int h=0;
       for(int i=n;i;i>>=1){
           h++;
       }
       return h;
   }
   void insert(int x,int num){
       node[x].sum++;
       maxx=max(maxx,x);
       if(node[x].val!=int_max){
           if(num<=node[x].val){
               insert(x*2,num);
           }else{
               insert(x*2+1,num);
           }
       }else{
           node[x].val=num;
       }
   }
   int main(){
       cin>>n;
       //cout<<h<<endl;
       for(int i=0;i<n;i++){
           scanf("%d",&x);
           insert(1,x);
       }
       int h=getHeight(maxx);
       //
       /*
        for(int i=1;i<=maxx;i++){
           cout<<node[i].val<<endl;
       }//*/
       int n1=0,n2=0;
       for(int i=pow(2,h-1);i<=maxx;i++){
           if(node[i].val!=int_max)n1++;
       }
       for(int i=pow(2,h-2);i<pow(2,h-1);i++){
           if(node[i].val!=int_max)n2++;
       }
       cout<<n1<<" + "<<n2<<" = "<<n1+n2<<endl;
       return 0;
   }
   ```

2. ==AC==

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<vector>
   #include<map>
   #include<math.h>
   using namespace std;
   const int maxN=1e3+5;
   const int int_max=2147483647;
   int sum[maxN]={0};
   struct NODE{
       int val=int_max,level=0;
       NODE *left,*right;
   }*root;
   int n,maxLevel=0,x;
   int getHeight(int n){
       int h=0;
       for(int i=n;i;i>>=1){
           h++;
       }
       return h;
   }
   void insert(NODE* &x,int num,int l){
       if(x!=NULL){
           if(num<=x->val){
               insert(x->left,num,l+1);
           }else{
               
               insert(x->right,num,l+1);
           }
       }else{
           x=new NODE();
           x->val=num;
           x->level=l;
           maxLevel=max(maxLevel,x->level);
           sum[x->level]++;
           //cout<<l<<endl;
       }
   }
   int main(){
       cin>>n;
       for(int i=0;i<n;i++){
           scanf("%d",&x);
           insert(root,x,1);
       }
       cout<<sum[maxLevel]<<" + "<<sum[maxLevel-1]<<" = "<<sum[maxLevel-1]+sum[maxLevel]<<endl;
       return 0;
   }
   ```

   

