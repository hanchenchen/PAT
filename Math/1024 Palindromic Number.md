# 1024 Palindromic Number

1. 有两个测试样例过不了`2147483647 99`: `long long`溢出

   ```c++
   #include<iostream>
   #include<math.h>
   using namespace std;
   long long reverse(long long x){
       long long n=0;
       while(x>0){
           n*=10;
           n+=(x%10);
           x=x/10;
       }
       return n;
   }
   int main(){
       long long n;
       int k;
       cin>>n>>k;
       int i;
       for(i=0;i<k;i++){
           if(reverse(n)==n){
               printf("%lld\n%d",n,i);
               return 0;
           }
           n=n+reverse(n);
       }
       printf("%lld\n%d",n,i);
       return 0;   
   }
   ```

2. 1