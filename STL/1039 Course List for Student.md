# 1039 Course List for Student

1. `Map` + `Vector`

2. `if(n==0)return 0;` （最后一个测试用例）

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<map>
   #include<vector>
   using namespace std;
   map<string,vector<int>> m;
   int main(){
       int n,k;
       if(n==0)return 0;
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

   