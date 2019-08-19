# 1047 Student List for Course

1. TLE

   `Map`+`String`+`Vector`+`cin`+`cout`

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<map>
   #include<vector>
   using namespace std;
   map<int,vector<string>> m;
   int main(){
       int n,k;
       map<int,vector<string>>::iterator iter;
       cin>>n>>k;
       for(int i=0;i<n;i++){
           string stu;int num;
           cin>>stu>>num;
           for(int j=0;j<num;j++){
               int course;
               cin>>course;
               iter=m.find(course);
               if(iter==m.end()){
                   m.insert(pair<int,vector<string>>(course,vector<string>(1,stu)));
               }
               else
                   iter->second.push_back(stu);
           }
       }
       for(int i=1;i<=k;i++){
           cout<<i<<" "<<m[i].size()<<endl;
           sort(m[i].begin(),m[i].end());
           for(int j=0;j<m[i].size();j++){
               cout<<m[i][j]<<endl;
           }
       }
       return 0;
   }
   ```

2. AC

   ⚠️：vector push `char*`，放入的是地址，之后对`char*`的修改，会改变`vector`的值。

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<vector>
   using namespace std;
   const int MAX=2505;
   vector<char*> v[MAX];
   int main(){
       int n,k;
       cin>>n>>k;char stu[n+1][5];
       for(int i=1;i<=n;i++){
           int num;
           scanf("%s",stu[i]);
           scanf("%d",&num);
           for(int j=0;j<num;j++){
               int course;
               scanf("%d",&course);
               v[course].push_back(stu[i]);
           }
           //cout<<num<<endl;
       }
       for(int i=1;i<=k;i++){
           printf("%d %d\n",i,(int)v[i].size());
           sort(v[i].begin(),v[i].end(),[](char *a,char *b){
               for(int i=0;i<4;i++){
                   if(a[i]==b[i])continue;
                   return a[i]<b[i];
               }
               return false;
           });
           for(int j=0;j<v[i].size();j++){
               printf("%s\n",v[i][j]);
           }
       }
       return 0;
   }
   ```

3. `Hash`?



