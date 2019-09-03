# 1048 Find Coins

1. `Hash`

   ```c++
   #include<iostream>
   #include<algorithm>
   using namespace std;
   int arr[1005]={0};
   int main(){
       int n,m;
       scanf("%d %d",&n,&m);
       int x;
       int v1=2147483647,v2=-1;
       for(int i=0;i<n;i++){
           scanf("%d",&x);
           if(arr[m-x]&&(min(x,m-x)<v1)){
               if(x<=m-x){
                   v1=x;v2=m-x;
               }
               else {
                   v2=x;v1=m-x;
               }
           }
           arr[x]=1;
       }
       if(v2>0)printf("%d %d",v1,v2);
       else printf("No Solution");   
   }
   ```

2. `Two Pointers`

   ```c++
   #include<iostream>
   #include<algorithm>
   using namespace std;
   int arr[100005]={0};
   int main(){
       int n,m;
       scanf("%d %d",&n,&m);
       for(int i=0;i<n;i++){
           scanf("%d",&arr[i]);
       }
       sort(arr,arr+n);
       for(int i=0;i<n;i++){
           int j=lower_bound(arr,arr+n,m-arr[i])-arr;
           if(i!=j&&arr[i]+arr[j]==m){//不能重复使用
               printf("%d %d",arr[i],arr[j]);
               return 0;
           }
       }
       printf("No Solution");
       return 0;   
   }
   ```

   

