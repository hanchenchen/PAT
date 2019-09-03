# **1044** **Shopping in Mars** 

1. `lower_bound`

   ```c++
   #include<iostream>
   #include<queue>
   #include<vector>
   #include<string.h>
   #include<map>
   #include<stdio.h>
   #include<algorithm>
   using namespace std;
   int n,m;
   int arr[(int)1e5+1]={0};
   int main(){
       scanf("%d %d",&n,&m);
       for(int i=1;i<=n;i++){
           scanf("%d",&arr[i]);
           arr[i]+=arr[i-1];
       }
       int ans=2147483647;
       for(int i=1;i<=n;i++){
           int j=lower_bound(arr,arr+n+1,m+arr[i-1])-arr;
           //cout<<j<<endl;
           if(arr[j]-arr[i-1]==m){
               ans=m;
               break;
           }
           if(arr[j]-arr[i-1]>m){
               ans=min(ans,arr[j]-arr[i-1]);
           }
       }
       //cout<<ans<<endl;
       m=ans;
       for(int i=1;i<=n;i++){
           int j=lower_bound(arr,arr+n+1,m+arr[i-1])-arr;
           if(arr[j]-arr[i-1]==m){
               printf("%d-%d\n",i,j);
           }
       }
       return 0;
   }
   ```

2. 最小值最大值的初始化一定要在范围之外

   ```c++
   #include<iostream>
   #include<queue>
   #include<vector>
   #include<string.h>
   #include<map>
   #include<stdio.h>
   #include<algorithm>
   using namespace std;
   int n,m;
   int arr[(int)1e5+1]={0};
   int main(){
       scanf("%d %d",&n,&m);
       for(int i=0;i<n;i++){
           scanf("%d",&arr[i]);
       }
       int right=0,left=0,ans=2147483647,sum=0;
       while(left<n){
           while(right<n&&sum<m){
               sum+=arr[right++];
           }
           if(sum>=m&&sum-m<ans-m)ans=sum;
           if(sum==m&&left<right){
               printf("%d-%d\n",left+1,right);
               if(right==n)break;
           }
           sum-=arr[left++];
       }
       if(ans==m)return 0;
       sum=right=left=0;
       m=ans;
       while(left<n){
           while(right<n&&sum<m){
               sum+=arr[right++];
           }
           if(sum==m){
               printf("%d-%d\n",left+1,right);
               if(right==n)break;
           }
           sum-=arr[left++];
       }
       return 0;
   }
   
   ```

   