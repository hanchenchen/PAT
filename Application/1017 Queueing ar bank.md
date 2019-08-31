# 1017 Queueing ar bank

1. 只要是17:00:00及之前来的客人，即使办理时间超过了17:00:00，也计算在内

   ```c++
   #include<iostream>
   #include<vector>
   #include<map>
   #include<algorithm>
   #include<math.h>
   
   using namespace std;
   const int maxN=10005;
   const int maxK=105;
   const int MAX=1e9;
   int table[maxN];
   map<int,int> cust;
   int getsecond(int h,int m,int s){
       return 3600*h+60*m+s;
   }
   int main(){
       int n,k;
       cin>>n>>k;
       int hh,mm,ss;int x;
       for(int i=0;i<n;i++){
           scanf("%d:%d:%d %d",&hh,&mm,&ss,&x);
           if(getsecond(hh,mm,ss)<=getsecond(17,0,0)){
               cust[getsecond(hh,mm,ss)]=x;
           }
           //cout<<getsecond(hh,mm,ss)<<" "<< cust[getsecond(hh,mm,ss)]<<endl;
           
       }
       int stTime=getsecond(8,0,0);
       int edTime=getsecond(17,0,0);
       
       for(int i=0;i<k;i++){
           table[i]=stTime;
       }
       double ans=0;int count=0;
       map<int,int>::iterator iter=cust.begin();
       for(;iter!=cust.end();iter++){
           //cout<<iter->first<<endl;
           int t=0;
           int endTime=MAX;
           for(int i=0;i<k;i++){
               if(endTime>table[i]){
                   t=i;
                   endTime=table[i];
               }
           }
           if(endTime>=iter->first){
               ans=ans-iter->first+endTime;
               table[t]+=60*iter->second;
               count++;
           }else{
               table[t]=60*iter->second+iter->first;
               count++;
           }
           //cout<<ans<<endl;
       }
       //cout<<ans<<endl;
       printf("%.1f",ans/count/60.0);
       return 0;
   }
   ```

   