# 1091 Acute Strock

1. `Stack` 

2. | Submit Time         | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
   | ------------------- | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
   | 8/21/2019, 20:09:26 | Accepted | 30    | [1091](https://pintia.cn/problem-sets/994805342720868352/problems/994805375457411072) | C++ (g++) | 589 ms   | cc   |

   | Case | Result   | Run Time | Memory   |
   | ---- | -------- | -------- | -------- |
   | 0    | Accepted | 215 ms   | 38944 KB |
   | 1    | Accepted | 184 ms   | 38912 KB |
   | 2    | Accepted | 198 ms   | 38912 KB |
   | 3    | Accepted | 125 ms   | 39040 KB |
   | 4    | Accepted | 589 ms   | 43160 KB |
   | 5    | Accepted | 579 ms   | 43008 KB |

3. ```c++
   #include<iostream>
   #include<algorithm>
   #include<vector>
   #include<queue>
   #include<math.h>
   #include<string.h>
   using namespace std;
   int m,n,l,t;
   int arr[60][1286][128];
   int vis[60][1286][128];
   struct NODE{
       int x;int y;int z;
   }node;
   int bfs(int i,int j,int k){
       vis[i][j][k]=1;
       node.x=i;node.y=j;node.z=k;
       queue<NODE> q;
       q.push(node);int ans=0;
       while(!q.empty()){
           node=q.front();q.pop();ans++;
           i=node.x;j=node.y;k=node.z;
           if(i<l-1&&arr[i+1][j][k]&&!vis[i+1][j][k]){
               node.x=i+1;node.y=j;node.z=k;
               vis[i+1][j][k]=1;
               q.push(node);
           }
           if(i>0&&arr[i-1][j][k]&&!vis[i-1][j][k]){
               node.x=i-1;node.y=j;node.z=k;
               vis[i-1][j][k]=1;
               q.push(node);
           }
           if(j<m-1&&arr[i][j+1][k]&&!vis[i][j+1][k]){
               node.x=i;node.y=j+1;node.z=k;
               vis[i][j+1][k]=1;
               q.push(node);
           }
           if(j>0&&arr[i][j-1][k]&&!vis[i][j-1][k]){
               node.x=i;node.y=j-1;node.z=k;
               vis[i][j-1][k]=1;
               q.push(node);
           }
           if(k<n-1&&arr[i][j][k+1]&&!vis[i][j][k+1]){
               node.x=i;node.y=j;node.z=k+1;
               vis[i][j][k+1]=1;
               q.push(node);
           }
           if(k>0&&arr[i][j][k-1]&&!vis[i][j][k-1]){
               node.x=i;node.y=j;node.z=k-1;
               vis[i][j][k-1]=1;
               q.push(node);
           }
       }
       return ans;
   }
   int main(){
       int x;
       cin>>m>>n>>l>>t;
       memset(vis,0,sizeof(vis));
       for(int i=0;i<l;i++){
           for(int j=0;j<m;j++){
               for(int k=0;k<n;k++){
                   cin>>x;
                   arr[i][j][k]=x;
               }
           }
       }
       int ans=0;
       for(int i=0;i<l;i++){
           for(int j=0;j<m;j++){
               for(int k=0;k<n;k++){
                   if(arr[i][j][k]==1&&vis[i][j][k]==0){
                       int x=bfs(i,j,k);
                       if(x>=t)ans+=x;
                   }
               }
           }
       }
       cout<<ans<<endl;
       return 0;   
   }
   ```

4. 

5. 1