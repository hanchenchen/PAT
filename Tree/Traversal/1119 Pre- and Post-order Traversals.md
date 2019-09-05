# **1119** **Pre- and Post-order Traversals** 

1. ⚠️最后一行endl

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<vector>
   using namespace std;
   const int maxN=35;
   const int int_max=2147483647;
   int preOrder[maxN]={0},postOrder[maxN]={0};
   int n,if_unique=1;
   vector<int> ans;
   void func(int preLeft,int preRight,int postLeft,int postRight){
       //cout<<preLeft<<" "<<preRight<<" "<<postLeft<<" "<<postRight<<endl;
       if(preLeft==preRight){
           ans.push_back(preOrder[preLeft]);
           return;
       }
       if(preOrder[preLeft]==postOrder[postRight]){
           int i=postRight-1;
           while(i>=postLeft&&preOrder[preLeft+1]!=postOrder[i])i--;
           if(i==postRight-1)if_unique=0;
           func(preLeft+1,preLeft+1+i-postLeft,postLeft,i);
           ans.push_back(preOrder[preLeft]);
           if(i<postRight-1)func(preRight+i+1-postRight+1,preRight,i+1,postRight-1);
       }
   }
   int main(){
       cin>>n;
       for(int i=0;i<n;i++){
           scanf("%d",&preOrder[i]);
       }
       for(int i=0;i<n;i++){
           scanf("%d",&postOrder[i]);
       }
       func(0,n-1,0,n-1);
       if(if_unique)
           cout<<"Yes"<<endl;
       else cout<<"No"<<endl;
       cout<<ans[0];
       for(int i=1;i<ans.size();i++){
           cout<<" "<<ans[i];
       }
       return 0;
   }
   ```

   