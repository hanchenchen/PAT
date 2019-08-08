# **1068** **Find More Coins** 

照着背包问题做的

```c++
#include<iostream>
#include<algorithm>
#include<cstring>
using namespace std;
int main(){
  int n,m;
  scanf("%d %d",&n,&m);
  int arr[n]={0};
  for(int i=0;i<n;i++){
      scanf("%d",&arr[i]);
  }
  sort(arr,arr+n,[](int &a,int &b){return a>b;});
  int dp[n][m+1]={{0}};
  memset(dp,0,sizeof(dp));
  dp[0][m]=1;dp[0][m-arr[0]]=1;
    for(int i=1;i<n;i++){
        for(int j=m;j>=0;j--){
            dp[i][j]=dp[i-1][j]||(j+arr[i]<=m&&dp[i-1][j+arr[i]]);
        }
    }
    int i=n-1;
    int cc=0;
    while(!dp[i][0]&&i>=0)i--;
    if(i<0){
        printf("No Solution\n");
        return 0;
    }
    while(i>0){
        if(dp[i-1][cc+arr[i]]>0){
            printf("%d",arr[i]);
            cc+=arr[i];
            if(cc==m)break;
            else printf(" ");
        }
        i--;
    }
    if(cc<m)printf("%d",m-cc);
  return 0;
}
```

