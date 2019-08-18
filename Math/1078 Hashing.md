# **1078** **Hashing**

1. 第`i`个查找位置`Ni=(x+i*i)%TSize`，`TSize`为表长

2. 查找`TSize`个位置后结束查找，而非`x+i*i`>`TSize`时

3. `1`既不是合数也不是素数

   ```c++
   #include<iostream>
   #include<string.h>
   using namespace std;
   const int MAX=700000;
   int arr[MAX];
   void ifprime(){
       for(int i=2;i<MAX;i++){
           if(arr[i]==-1){
               for(int j=2;j*i<MAX;j++){
                   arr[j*i]=0;
               }
           }
       }
   }
   int main(){
       memset(arr,-1,sizeof(arr));
       arr[1]=0;arr[0]=0;
       ifprime();
       int m,n;
       cin>>m>>n;
       while(arr[m]!=-1)m++;
       int table[m]={0};
       int x;
       for(int k=0;k<n;k++){
           if(k!=0)printf(" ");
           cin>>x;
           x=x%m;int i=0;
           for(;i<m;i++){
               if(table[(x+i*i)%m]==0)break;
           };
           if(table[(x+i*i)%m]==1){printf("-");}
           else {
               printf("%d",(x+i*i)%m);
               table[(x+i*i)%m]=1;
           }
       }
       return 0;
   }
   ```

   