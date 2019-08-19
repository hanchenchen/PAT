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

2. AC

   ```c++
   #include<iostream>
   #include<math.h>
   using namespace std;
   string reverse(string x){
       string n="";
       int i=0;
       for(;i<x.size();i++){
           n=x[i]+n;
       }i=0;
       while(n[i]=='0')i++;
       return n.substr(i);
   }
   void add(string &s1,string s2){
       int c=0;string num="";
       int x=0;
       while(s2.size()<s1.size())s2='0'+s2;
       for(int i=(int)s1.size()-1;i>=0;i--){
           x=s1[i]+s2[i]-2*'0'+c;
           c=x/10;
           x=x%10;
           s1[i]=x+'0';
       }
       if(c)s1=(char)('0'+c)+s1;
   }
   int main(){
       string n;
       int k;
       cin>>n>>k;
       int i;
       for(i=0;i<k;i++){
           if(reverse(n)==n){
               cout<<n<<endl<<i;
               return 0;
           }
           add(n,reverse(n));
       }
       cout<<n<<endl<<i;
       return 0;
   }
   
   ```

   