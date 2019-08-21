# 1054 The Dominant Color

1. TLE  

   输入过程中判断最大数量

   | Submit Time         | Status             | Score | Problem                                                      | Compiler  | Run Time | User |
   | ------------------- | ------------------ | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
   | 8/21/2019, 12:31:22 | Partially Accepted | 18    | [1054](https://pintia.cn/problem-sets/994805342720868352/problems/994805422639136768) | C++ (g++) | 27 ms    | cc   |

   | Case | Result              | Run Time | Memory  |
   | ---- | ------------------- | -------- | ------- |
   | 0    | Accepted            | 3 ms     | 424 KB  |
   | 1    | Accepted            | 3 ms     | 392 KB  |
   | 2    | Time Limit Exceeded | --       | 0 KB    |
   | 3    | Accepted            | 27 ms    | 1116 KB |
   | 4    | Accepted            | 3 ms     | 384 KB  |

2. ```c++
   #include<iostream>
   #include<algorithm>
   #include<map>
   #include<string.h>
   using namespace std;
   map<string,int> m;
   string arr[200];
   int main(){
       int k,n;
       cin>>k>>n;
       string s;
       map<string,int>::iterator iter;
       int num=0;string ans="";
       for(int i=0;i<k*n;i++){
           cin>>s;
           iter=m.find(s);
           if(iter!=m.end()){
               m[s]++;
           }else{
               m.insert(pair<string,int>(s,1));
           }
           if(num<m[s]){
               num=m[s];
               ans=s;
           }
       }
       cout<<s<<endl;
       return 0;
   }
   ```

3. AC

   输入完成后再循环外判断，`map.size()`<`矩阵的元素个数`

   | Submit Time         | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
   | ------------------- | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
   | 8/21/2019, 12:34:25 | Accepted | 20    | [1054](https://pintia.cn/problem-sets/994805342720868352/problems/994805422639136768) | C++ (g++) | 111 ms   | cc   |

   | Case | Result   | Run Time | Memory  |
   | ---- | -------- | -------- | ------- |
   | 0    | Accepted | 3 ms     | 416 KB  |
   | 1    | Accepted | 3 ms     | 416 KB  |
   | 2    | Accepted | 111 ms   | 320 KB  |
   | 3    | Accepted | 14 ms    | 1184 KB |
   | 4    | Accepted | 3 ms     | 384 KB  |

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<map>
   #include<string.h>
   using namespace std;
   map<string,int> m;
   string arr[200];
   int main(){
       int k,n;
       cin>>k>>n;
       string s;
       map<string,int>::iterator iter;
       int num=0;string ans="";
       for(int i=0;i<k*n;i++){
           cin>>s;
           iter=m.find(s);
           if(iter!=m.end()){
               m[s]++;
           }else{
               m.insert(pair<string,int>(s,1));
           }
       }
       for(iter=m.begin();iter!=m.end();iter++){
           if(num<iter->second){
               num=iter->second;
               ans=iter->first;
           }
       }
       cout<<s<<endl;
       return 0;
   }
   ```

4. 1