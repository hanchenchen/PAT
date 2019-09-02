# 1037 **Magic Coupon**

```
#include<iostream>
#include<map>
#include<vector>
#include<string.h>
#include<set>
#include<algorithm>
using namespace std;
const int maxN=100005;
//const int maxInt=2147483647;
/*
struct STU{
    double price=0.0,amount=0.0;
}stu[maxN];//*/
int n,m,coupon[maxN],product[maxN];
int main(){
    cin>>n;
    for(int i=0;i<n;i++){
        scanf("%d",&coupon[i]);
    }
    cin>>m;
    for(int i=0;i<m;i++){
        scanf("%d",&product[i]);
    }
    sort(coupon,coupon+n);
    sort(product,product+m);
    long long ans=0;
    for(int i=0,j=0;i<n&&j<m&&coupon[i]<0&&product[j]<0;i++,j++){
        ans+=coupon[i]*product[j];
        //cout<<coupon[i]<<" "<<product[j]<<endl;
    }
    for(int i=n-1,j=m-1;i>=0&&j>=0&&coupon[i]>0&&product[j]>0;i--,j--){
        ans+=coupon[i]*product[j];
        //cout<<ans<<endl;
    }
    printf("%lld",ans);
    return 0;
}


```

