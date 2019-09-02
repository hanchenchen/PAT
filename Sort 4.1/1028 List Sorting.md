# 1028 List Sorting

1. `cin/cout`会超时

   ```c++
   #include<iostream>
   #include<queue>
   #include<vector>
   #include<string.h>
   #include<set>
   #include<algorithm>
   using namespace std;
   const int maxN=100005;
   //const int maxInt=2147483647;
   int n,c;
   struct STU{
       int id;
       char name[10];
       int grade;
   }stu[maxN];
   int main(){
       cin>>n>>c;
       for(int i=0;i<n;i++){
           scanf("%d %s %d",&stu[i].id,stu[i].name,&stu[i].grade);
       }
       if(c==1){
           sort(stu,stu+n,[](STU a,STU b){
               return a.id<b.id;
           });
       }else if(c==2){
           sort(stu,stu+n,[](STU a,STU b){
               if(strcmp(a.name,b.name)==0)return a.id<b.id;
               return strcmp(a.name,b.name)<0;
           });
       }else if(c==3){
           sort(stu,stu+n,[](STU a,STU b){
               if(a.grade==b.grade)return a.id<b.id;
               return a.grade<b.grade;
           });
       }
       for(int i=0;i<n;i++){
           printf("%06d %s %d\n",stu[i].id,stu[i].name,stu[i].grade);
       }
       return 0;
   }
   ```

   