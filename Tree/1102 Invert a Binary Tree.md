# 1102 Invert a Binary Tree

1. `Invert`

2. 1

3. ```c++
   #include<iostream>
   #include<queue>
   #include<string.h>
   using namespace std;
   int l[15][2]={0};
   int if_out=0;
   int Root[15]={0};
   void func(int root){
       if(root==-1)return;
       if(l[root][0]!=-1)func(l[root][0]);
       if(if_out)cout<<" ";
       else if_out=1;
       cout<<root;
       if(l[root][1]!=-1)func(l[root][1]);
   }
   int main(){
       memset(l,-1,sizeof(l));
       memset(Root,-1,sizeof(Root));
       int n;
       char left,right;
       cin>>n;
       for(int i=0;i<n;i++){
           cin>>right>>left;
           if(left!='-'){
               l[i][0]=left-'0';
               Root[left-'0']=i;
           }
           if(right!='-'){
               l[i][1]=right-'0';
               Root[right-'0']=i;
           }
       }
       int root=0;
       while(Root[root]!=-1)root=Root[root];
       queue<int> qe;
       qe.push(root);
       while(!qe.empty()){
           if(l[qe.front()][0]!=-1)qe.push(l[qe.front()][0]);
           if(l[qe.front()][1]!=-1)qe.push(l[qe.front()][1]);
           if(if_out)cout<<" ";
           else if_out=1;
           cout<<qe.front();qe.pop();
       }
       cout<<endl;
       if_out=0;
       func(l[root][0]);
       if(if_out)cout<<" ";
       else if_out=1;
       cout<<root;
       func(l[root][1]);
       return 0;
   }
   ```

   