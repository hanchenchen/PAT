# 1053 Path of Equal Weight

1. 终点为非叶子结点！（测试点1）

2. ```c++
   #include<iostream>
   #include<vector>
   #include<algorithm>
   using namespace std;
   int weight[100]={0};
   int s;
   vector<int> child[100];
   int ans[100]={0};
   void dfs(int x,int sum,int n){
       //cout<<x<<" "<<sum<<" "<<n<<endl;
       ans[n]=weight[x];
       if(sum>s)return;
       if(sum==s&&child[x].size()==0){
           cout<<ans[0];
           for(int i=1;i<=n;i++){
               cout<<" "<<ans[i];
           }
           cout<<endl;
           return;
       }
       for(int i=0;i<child[x].size();i++){
           dfs(child[x][i],sum+weight[child[x][i]],n+1);
       }
   }
   int main(){
       int n,m;
       cin>>n>>m>>s;
       for(int i=0;i<n;i++){
           cin>>weight[i];
       }
       int node,num,children;
       for(int i=0;i<m;i++){
           cin>>node>>num;
           for(int j=0;j<num;j++){
               cin>>children;
               child[node].push_back(children);
           }
           sort(child[node].begin(),child[node].end(),[](int a,int b){
               return weight[a]>weight[b];
           });
       }
       dfs(0,weight[0],0);
       return 0;
   }
   ```

3. 