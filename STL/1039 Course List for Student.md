# 1039 Course List for Student

1. `Map` 、`String`、`cin`、`cout` 会导致超时

2. 

3. `TLE`？？？

   `if(n==0)return 0;` （否则最后一个测试用例TLE）

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<map>
   #include<vector>
   using namespace std;
   map<string,vector<int>> m;
   int main(){
       int n,k;
       if(n==0)return 0;//???为什么加这儿可以AC
       map<string,vector<int>>::iterator iter;
       cin>>n>>k;
       for(int i=0;i<k;i++){
           int course,stu;
           cin>>course>>stu;
           for(int j=0;j<stu;j++){
               string name;
               cin>>name;
               iter=m.find(name);
               if(iter==m.end()){
                   m.insert(pair<string,vector<int>>(name,vector<int>(1,course)));
               }else
                   iter->second.push_back(course);
           }
       }
       for(int i=0;i<n;i++){
           string name;
           cin>>name;
           cout<<name<<" "<<m[name].size();
           sort(m[name].begin(),m[name].end());
           for(int j=0;j<m[name].size();j++){
               cout<<" "<<m[name][j];
           }
           cout<<endl;
       }
       return 0;
   }
   ```

4. `TLE`

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<map>
   #include<vector>
   using namespace std;
   const int MAX=2505;
   vector<string> v[MAX];
   int main(){
       int n,k;
       cin>>n>>k;
       for(int i=0;i<n;i++){
           string stu;int num;
           cin>>stu>>num;
           for(int j=0;j<num;j++){
               int course;
               cin>>course;
               v[course].push_back(stu);
           }
       }
       for(int i=1;i<=k;i++){
           cout<<i<<" "<<v[i].size()<<endl;
           sort(v[i].begin(),v[i].end());
           for(int j=0;j<v[i].size();j++){
               cout<<v[i][j]<<endl;
           }
       }
       return 0;
   }
   ```

5. 1