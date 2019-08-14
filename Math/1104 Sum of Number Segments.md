# ?**1104** **Sum of Number Segments** 

1. ac

   ```c++
   #include<iostream>
   using namespace std;
   int main(){
       int n;
       scanf("%d",&n);
       double ans=0;
       double arr;
       for(int i=0;i<n;i++){
           scanf("%lf",&arr);
           ans=ans+arr*(i+1)*(n-i);
       }
       printf("%0.2f",ans);
       return 0;
   }
   
   
   ```

2. wa(2/4)

   ```c++
   #include<iostream>
   using namespace std;
   int main(){
       int n;
       scanf("%d",&n);
       double ans=0;
       double arr;
       for(int i=0;i<n;i++){
           scanf("%lf",&arr);
           ans=ans+(i+1)*(n-i)*arr;
       }
       printf("%0.2f",ans);
       return 0;
   }
   
   ```

   