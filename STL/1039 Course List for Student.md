# 1039 Course List for Student

1. `Map` 、`String`、`cin\cout` 会导致超时


2. `TLE`

      ```c++
   #include<iostream>
      #include<algorithm>
      #include<map>
      #include<vector>
   std::ios::sync_with_stdio(false);
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
   
3. 莫名其妙AC

   `TLE`？？？

   添加`if(n==0)return 0;`后 通过最后一个测试用例

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

4.  把`cin\cout `换成`scanf\printf` ,AC

      | Case | Result   | Run Time | Memory   |
      | ---- | -------- | -------- | -------- |
      | 0    | Accepted | 3 ms     | 512 KB   |
      | 1    | Accepted | 2 ms     | 512 KB   |
      | 2    | Accepted | 3 ms     | 384 KB   |
      | 3    | Accepted | 3 ms     | 384 KB   |
      | 4    | Accepted | 3 ms     | 384 KB   |
      | 5    | Accepted | 446 ms   | 22784 KB |
      
      ```c++
      #include<iostream>
      #include<algorithm>
      #include<map>
      #include<vector>
      using namespace std;
      map<string,vector<int>> m;
      int main(){
          int n,k;
          //if(n==0)return 0;
          map<string,vector<int>>::iterator iter;
          scanf("%d %d",&n,&k);
          for(int i=0;i<k;i++){
              int course,stu;
              scanf("%d %d",&course,&stu);
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
                  printf(" %d",m[name][j]);
              }
              printf("\n");
          }
          return 0;
      }
      ```

5. `Hash`

   | Submit Time         | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
   | ------------------- | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
   | 8/19/2019, 20:33:47 | Accepted | 25    | [1039](https://pintia.cn/problem-sets/994805342720868352/problems/994805447855292416) | C++ (g++) | 285 ms   | cc   |

   | Case | Result   | Run Time | Memory   |
   | ---- | -------- | -------- | -------- |
   | 0    | Accepted | 13 ms    | 11048 KB |
   | 1    | Accepted | 13 ms    | 11048 KB |
   | 2    | Accepted | 11 ms    | 10976 KB |
   | 3    | Accepted | 10 ms    | 11008 KB |
   | 4    | Accepted | 10 ms    | 11048 KB |
   | 5    | Accepted | 285 ms   | 17536 KB |

   ```c++
   #include<iostream>
   #include<algorithm>
   //#include<map>
   #include<vector>
   using namespace std;
   const int MAX=26*26*26*26+1;
   vector<int> v[MAX];
   int getnum(string s){
       int x=0;
       for(int i=0;i<3;i++){
           x*=26;
           x+=(s[i]-'A');
       }
       x*=26;
       x+=s[3]-'0';
       return x;
   }
   int main(){
       int n,k;
       scanf("%d %d",&n,&k);
       for(int i=0;i<k;i++){
           int course,stu;
           scanf("%d %d",&course,&stu);
           for(int j=0;j<stu;j++){
               string name;
               cin>>name;
               v[getnum(name)].push_back(course);
           }
       }
       for(int i=0;i<n;i++){
           string name;
           cin>>name;
           int x=getnum(name);
           cout<<name<<" "<<v[x].size();
           sort(v[x].begin(),v[x].end());
           for(int j=0;j<v[x].size();j++){
               printf(" %d",v[x][j]);
           }
           printf("\n");
       }
       return 0;
   }
   
   ```

   

