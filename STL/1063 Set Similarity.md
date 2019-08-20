# 1063 Set Similarity

1. AC

   | Submit Time         | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
   | ------------------- | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
   | 8/20/2019, 14:55:27 | Accepted | 25    | [1063](https://pintia.cn/problem-sets/994805342720868352/problems/994805409175420928) | C++ (g++) | 490 ms   | cc   |

   | Case | Result   | Run Time | Memory  |
   | ---- | -------- | -------- | ------- |
   | 0    | Accepted | 2 ms     | 380 KB  |
   | 1    | Accepted | 3 ms     | 384 KB  |
   | 2    | Accepted | 4 ms     | 416 KB  |
   | 3    | Accepted | 8 ms     | 408 KB  |
   | 4    | Accepted | 490 ms   | 2816 KB |

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<set>
   #include<string.h>
   using namespace std;
   int main(){
       int n,m;int x;
       scanf("%d",&n);
       set<int> arr[55];
       for(int i=1;i<=n;i++){
           scanf("%d",&m);
           for(int j=0;j<m;j++){
               scanf("%d",&x);
               arr[i].insert(x);
           }
       }
       int k=0;
       scanf("%d",&k);
       int q1,q2;
       set<int>::iterator iter1,iter2;
       for(int i=0;i<k;i++){
           scanf("%d %d",&q1,&q2);
           double nc=0.0,nt=0.0;
           iter1=arr[q1].begin();
           iter2=arr[q2].begin();
           set<int> se;
           while(iter1!=arr[q1].end()){
               se.insert(*iter1);
               iter1++;
           }
           while(iter2!=arr[q2].end()){
               se.insert(*iter2);
               iter2++;
           }
           nt=se.size();
           nc=arr[q1].size()+arr[q2].size()-nt;
           printf("%.1lf%%\n",(nc/nt)*100);
       }
       return 0;
   }
   ```

2. 1

3. 1