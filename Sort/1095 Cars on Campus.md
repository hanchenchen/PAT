# 1095 **Cars on Campus** 

1. `map<char*,int>`，即使`strcmp(str1,str2)==0`，但是它们地址是不一样的，所以键值也是不一样的。

2. 放弃`char[]`好写多了

   ```c++
   #include<iostream>
   #include<map>
   #include<vector>
   #include<string.h>
   #include<set>
   #include<algorithm>
   using namespace std;
   int getSecond(int hh,int mm,int ss){
       return hh*60*60+mm*60+ss;
   }
   const int maxN=10005;
   const int maxK=80005;
   const int maxS=24*60*60;
   //const int maxInt=2147483647;
   struct STU{
       int times,getIn=-1;
       string id;
   }stu[maxN];
   int n,k;//records queries
   int charNum[maxS]={0};
   int main(){
       cin>>n>>k;int hh,mm,ss;string s;
       for(int i=0;i<n;i++){
           cin>>stu[i].id;
           scanf("%d:%d:%d",&hh,&mm,&ss);
           stu[i].times=getSecond(hh,mm,ss);
           cin>>s;
           if(s=="in")stu[i].getIn=1;
       }
       sort(stu,stu+n,[](const STU a,const STU b){
           if(a.id!=b.id){
               return a.id<b.id;
           }
           return a.times<b.times;
       });
       map<string,int> time_of_car;
       vector<int> longestCar;int longestMunite=0;
       for(int i=0;i<n;i++){
           if(stu[i].getIn!=1)continue;
           int j=i+1;if(j>=n)break;
           if(stu[i].id!=stu[j].id||stu[j].getIn!=-1)continue;
           charNum[stu[i].times]++;
           charNum[stu[j].times]--;
           time_of_car[stu[i].id]=time_of_car[stu[i].id]+stu[j].times-stu[i].times;
           if(longestMunite<time_of_car[stu[i].id]){
               longestMunite=time_of_car[stu[i].id];
               longestCar.clear();
               longestCar.push_back(i);
           }else if(longestMunite==time_of_car[stu[i].id]){
               longestCar.push_back(i);
           }
       }
       for(int i=1;i<maxS;i++){
           charNum[i]+=charNum[i-1];
           //cout<<charNum[i]<<" ";
       }
       for(int i=0;i<k;i++){
           scanf("%d:%d:%d",&hh,&mm,&ss);
           printf("%d\n",charNum[getSecond(hh,mm,ss)]);
       }
       if(longestCar.size()==0)return 0;
       cout<<stu[longestCar[0]].id;
       for(int i=1;i<longestCar.size();i++){
           cout<<" "<<stu[longestCar[i]].id;
       }
       printf(" %02d:%02d:%02d",longestMunite/3600,(longestMunite%3600)/60,longestMunite%60);
       return 0;
   }
   
   ```

   