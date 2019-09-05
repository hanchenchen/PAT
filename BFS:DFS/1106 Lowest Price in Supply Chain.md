# 1106 Lowest Price in Supply Chain

1. TLE*1

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<vector>
   #include<map>
   #include<string.h>
   #include<math.h>
   using namespace std;
   const int maxN=1e5+5;
   const int int_max=2147483647;
   double p,r,price[maxN];
   int n,arr[maxN],vis[maxN];
   int main(){
       cin>>n>>p>>r;
       int x,y;
       price[0]=p;
       memset(arr,-1,sizeof(arr));
       for(int i=0;i<n;i++){
           scanf("%d",&x);
           if(x==0)vis[i]=1;
           for(int j=0;j<x;j++){
               scanf("%d",&y);
               arr[y]=i;
           }
           price[i+1]=price[i]+0.01*price[i]*r;
       }
       
       int mini=int_max;int retailer=0;
       for(int i=0;i<n;i++){
           if(!vis[i])continue;
           x=1;
           y=i;
           while(y!=-1){
               y=arr[y];x++;
               if(x>mini)break;
           }
           if(x<mini){
               mini=x;retailer=1;
           }else if(x==mini){
               retailer++;
           }
       }//cout<<mini<<endl;
       printf("%.4f %d\n",price[mini-2],retailer);
       return 0;
   }
   ```

2. ==AC==

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<vector>
   #include<map>
   #include<string.h>
   #include<math.h>
   using namespace std;
   const int maxN=1e5+5;
   const int int_max=2147483647;
   double p,r;
   int n;
   vector<int> arr[maxN];
   double mini=int_max;int retailer=0;
   void dfs(int x,double price){
       //cout<<x<<" "<<price<<endl;
       if(price>mini)return;
       if(arr[x].size()==0){
           if(price<mini){
               mini=price;retailer=1;
               return;
           }else if(arr[x].size()==0&&fabs(price-mini)<1e-6)
           {retailer++;return ;}
       }
       for(int i=0;i<arr[x].size();i++){
           dfs(arr[x][i],price+price*r*0.01);
       }
   }
   int main(){
       cin>>n>>p>>r;
       int x,y;
       for(int i=0;i<n;i++){
           scanf("%d",&x);
           for(int j=0;j<x;j++){
               scanf("%d",&y);
               arr[i].push_back(y);
           }
       }
       dfs(0,p);
       printf("%.4f %d\n",mini,retailer);
       return 0;
   }
   ```

   