# 1105 Spiral Matrix

```c++
#include<iostream>
#include<vector>
#include<stack>
#include<algorithm>
#include<math.h>

using namespace std;
const int maxN=1000005;
int arr[maxN]={0};
int main(){
    int n,k,l=1;
    cin>>n;
    for(int i=0;i<n;i++){
        cin>>arr[i];
    }
    sort(arr,arr+n,[](int a,int b){return a>b;});
    k=sqrt(n);
    while(k>0){
        l=n/k;
        if(l*k==n)break;
        k--;
    }
    int matrix[l][k];
    int vis[l][k];
    fill(vis[0],vis[0]+l*k,0);
    int i=1,x=0,y=0;
    vis[0][0]=1;
    matrix[0][0]=arr[0];
    int dire[4][2]={{0,1},{1,0},{0,-1},{-1,0}};
    while(i<n){
        for(int j=0;j<4;j++){
            while(x+dire[j][0]<l&&y+dire[j][1]<k&&!vis[x+dire[j][0]][y+dire[j][1]]){
                x+=dire[j][0];
                y+=dire[j][1];
                vis[x][y]=1;
                matrix[x][y]=arr[i++];
            }
        }
    }
    for(i=0;i<l;i++){
        cout<<matrix[i][0];
        for(int j=1;j<k;j++){
            cout<<" "<<matrix[i][j];
        }
        cout<<endl;
    }
    return 0;
}
```



