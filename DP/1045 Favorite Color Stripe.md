# **1045** **Favorite Color Stripe**

LCS（最长公共子序列）:

```c++
#include<iostream>
using namespace std;
int main(){
  int n,m;
  scanf("%d %d",&n,&m);
  int order[n+1]={0};
  int k=0;
  for(int i=1;i<=m;i++){
      scanf("%d",&order[i]);
  }
  scanf("%d",&k);
  int arr=0;
  int dp[m+1]={0};
  int ans=0;
  for(int i=0;i<k;i++){
      scanf("%d",&arr);
      for(int j=1;j<=m;j++){
          dp[j]=max(dp[j],dp[j-1]);
          if(arr==order[j])dp[j]++;
      }
  }
  printf("%d\n",dp[m]);
  return 0;
}
```

LIS（最长不下降子序列）:

```c++
#include<iostream>
using namespace std;
int main(){
  int n,m;
  scanf("%d %d",&n,&m);
  int order[n+1]={0};
  int k=0;
  for(int i=1;i<=m;i++){
      scanf("%d",&k);
      order[k]=i;
  }
  scanf("%d",&k);
  int arr[k]={0};
  int dp[k]={0};
  int ans=0;
  for(int i=0;i<k;i++){
      scanf("%d",&arr[i]);
      if(order[arr[i]]==0)continue;
      dp[i]=1;
      for(int j=0;j<i;j++){
          if(order[arr[i]]>=order[arr[j]]){
              dp[i]=max(dp[i],dp[j]+1);
          }
      }
      ans=max(dp[i],ans);
  }
  printf("%d\n",ans);
  return 0;
}
```

