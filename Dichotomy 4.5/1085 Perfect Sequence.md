# 1085 Perfect Sequence 

1. ##### 二分

   ```c++
   #include<iostream>
   #include<algorithm>
   using namespace std;
   const int maxN=100005;
   int n,p;
   int arr[maxN];
   int main(){
       cin>>n>>p;
       for(int i=0;i<n;i++){
           scanf("%d",&arr[i]);
       }
       sort(arr,arr+n);
       int left=0,right=n,ans=0;
       for(int i=0;i<n;i++){
           left=i+1;right=n;
           while(left<right){
               int mid=(left+right)/2;
               if(arr[mid]<=arr[i]*p){
                   left=mid+1;
               }else{
                   right=mid;
               }
           }
           ans=max(left-i,ans);
       }
       cout<<ans;
       return 0;
   }
   ```

2. ##### `two points`

   ```c++
   #include<iostream>
   #include<algorithm>
   using namespace std;
   const int maxN=100005;
   int n,p;
   int arr[maxN];
   int main(){
       cin>>n>>p;
       for(int i=0;i<n;i++){
           scanf("%d",&arr[i]);
       }
       sort(arr,arr+n);
       int ans=0;
       for(int i=0;i<n;i++){
           while(ans+i<n&&(long long)arr[i]*p>=arr[ans+i])ans++;
       }
       cout<<ans;
       return 0;
   }
   ```

3. #####  upper_bound

   `lower_bound(first, last,val)`......`[first,last)` 中第一个值大于等于`val`的元素的位置，返回指针/迭代器

   `upper_bound(first, last,val)`......`[first,last)` 中第一个值大于`val`的元素的位置，返回指针/迭代器

   取得下标：`int index=lower_bound(arr, arr+n,4)-arr;`

   ```c++
   #include<iostream>
   #include<stdio.h>
   #include<algorithm>
   using namespace std;
   const int maxN=100005;
   int n,p;
   int arr[maxN];
   int main(){
       cin>>n>>p;
       for(int i=0;i<n;i++){
           scanf("%d",&arr[i]);
       }
       sort(arr,arr+n);
       int ans=0;
       for(int i=0;i<n;i++){
           int j=upper_bound(arr,arr+n,(long long)arr[i]*p)-arr;
           ans=max(ans,j-i);
       }
       cout<<ans;
       return 0;
   }
   ```

4. 1