# 1101 **Quick Sort** 

```c++
#include<iostream>
#include<algorithm>
#include<vector>
using namespace std;
const int maxN =100006;
int l[maxN],r[maxN]={0},arr[maxN];
int main(){
    int n;
    cin>>n;
    l[0]=0;
    for(int i=1;i<=n;i++){
        scanf("%d",&arr[i]);
        l[i]=max(l[i-1],arr[i]);
    }
    r[n+1]=2147483647;
    for(int i=n;i>=1;i--){
        r[i]=min(r[i+1],arr[i]);
    }
    int ans=0;int pivot[maxN]={0};
    for(int i=1;i<=n;i++){
        //cout<<l[i]<<" "<<arr[i]<<" "<<r[i]<<endl;
        if(arr[i]>=l[i]&&arr[i]<=r[i]){
            pivot[ans++]=arr[i];
        }
    }
    if(ans==0){
        cout<<"0"<<endl<<endl;
        return 0;
    }
    cout<<ans<<endl<<pivot[0];
    for(int i=1;i<ans;i++){
        cout<<" "<<pivot[i];
    }
    return 0;
}

```

