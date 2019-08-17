# 1048 Find Coins

```c++
#include<iostream>
#include<algorithm>
using namespace std;
int arr[1005]={0};
int main(){
    int n,m;
    scanf("%d %d",&n,&m);
    int x;
    int v1=2147483647,v2=-1;
    for(int i=0;i<n;i++){
        scanf("%d",&x);
        if(arr[m-x]&&(min(x,m-x)<v1)){
            if(x<=m-x){
                v1=x;v2=m-x;
            }
            else {
                v2=x;v1=m-x;
            }
        }
        arr[x]=1;
    }
    if(v2>0)printf("%d %d",v1,v2);
    else printf("No Solution");
    
}

```

