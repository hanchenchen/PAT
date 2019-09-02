# 1062 Talent and Virtue

1. 使用函数再便利一遍有时会超时

   ```c++
   #include<iostream>
   #include<queue>
   #include<vector>
   #include<algorithm>
   using namespace std;
   const int maxN=100005;
   struct PEOPLE{
       string id;
       int grade=100;
       int virtue=0;
       int talent=0;
   }people[maxN];
   int n,m;
   int l,h;
   void update(){
       for(int i=0;i<n;i++){
           if(people[i].virtue<l||people[i].talent<l){
               m--;continue;
           }
           if(people[i].virtue>=h){
               if(people[i].talent>=h){
                   people[i].grade=1;
               }else{
                   people[i].grade=2;
               }
           }else if(people[i].virtue>=l&&people[i].virtue<h){
               if(people[i].virtue>=people[i].talent){
                   people[i].grade=3;
               }else{
                   people[i].grade=4;
               }
           }
       }
   }
   int main(){
       
       cin>>n>>l>>h;m=n;
       for(int i=0;i<n;i++){
           cin>>people[i].id>>people[i].virtue>>people[i].talent;
       }
       update();
       sort(people,people+n,[](PEOPLE a,PEOPLE b){
           if(a.grade==b.grade){
               if(a.talent+a.virtue==b.talent+b.virtue){
                   if(a.virtue==b.virtue){
                       return a.id<b.id;
                   }else{
                       return a.virtue>b.virtue;
                   }
               }else{
                   return a.talent+a.virtue>b.talent+b.virtue;
               }
           }else{
               return a.grade<b.grade;
           }
       });
       cout<<m<<endl;
       for(int i=0;i<m;i++){
           cout<<people[i].id<<" "<<people[i].virtue<<" "<<people[i].talent<<endl;
       }
       return 0;
   }
   ```

2. 输入时判断

   | Submit Time        | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
   | ------------------ | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
   | 9/1/2019, 09:36:43 | Accepted | 25    | [1062](https://pintia.cn/problem-sets/994805342720868352/problems/994805410555346944) | C++ (g++) | 320 ms   | cc   |

   | Case | Result   | Run Time | Memory  |
   | ---- | -------- | -------- | ------- |
   | 0    | Accepted | 7 ms     | 4964 KB |
   | 1    | Accepted | 8 ms     | 4992 KB |
   | 2    | Accepted | 160 ms   | 5252 KB |
   | 3    | Accepted | 320 ms   | 6568 KB |
   | 4    | Accepted | 297 ms   | 6568 KB |
   | 5    | Accepted | 6 ms     | 5032 KB |

   ```c++
   #include<iostream>
   #include<queue>
   #include<vector>
   #include<algorithm>
   using namespace std;
   const int maxN=100005;
   struct PEOPLE{
       string id;
       int grade=100;
       int virtue=0;
       int talent=0;
   }people[maxN];
   int n,m;
   int l,h;
   int main(){
       
       cin>>n>>l>>h;m=n;
       for(int i=0;i<n;i++){
           cin>>people[i].id>>people[i].virtue>>people[i].talent;
           if(people[i].virtue<l||people[i].talent<l){
               m--;continue;
           }
           if(people[i].virtue>=h){
               if(people[i].talent>=h){
                   people[i].grade=1;
               }else{
                   people[i].grade=2;
               }
           }else if(people[i].virtue>=l&&people[i].virtue<h){
               if(people[i].virtue>=people[i].talent){
                   people[i].grade=3;
               }else{
                   people[i].grade=4;
               }
           }
       }
       sort(people,people+n,[](PEOPLE a,PEOPLE b){
           if(a.grade==b.grade){
               if(a.talent+a.virtue==b.talent+b.virtue){
                   if(a.virtue==b.virtue){
                       return a.id<b.id;
                   }else{
                       return a.virtue>b.virtue;
                   }
               }else{
                   return a.talent+a.virtue>b.talent+b.virtue;
               }
           }else{
               return a.grade<b.grade;
           }
       });
       cout<<m<<endl;
       for(int i=0;i<m;i++){
           cout<<people[i].id<<" "<<people[i].virtue<<" "<<people[i].talent<<endl;
       }
       return 0;
   }
   ```

   