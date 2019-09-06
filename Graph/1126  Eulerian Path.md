# 1126  **Eulerian Path**

测试点三：判断是否连通

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<string.h>
#include<map>
#include<math.h>
using namespace std;
const int maxN=500+5;
int n,m,arr[maxN],odd=0,even=0,root[maxN];
int getroot(int x){
    int y=x;
    while(x!=root[x])x=root[x];
    root[y]=x;
    return x;
}
int main(){
    scanf("%d %d",&n,&m);
    for(int i=1;i<=n;i++){
        root[i]=i;
    }
    int x,y;
    for(int i=0;i<m;i++){
        scanf("%d %d",&x,&y);
        arr[x]++;
        arr[y]++;
        if(getroot(x)!=getroot(y))root[getroot(x)]=getroot(y);
    }
    int r=getroot(1),flag=1;
    for(int i=1;i<=n;i++){
        if(i!=1)cout<<" ";
        cout<<arr[i];
        if(getroot(i)!=r)flag=0;
        if(arr[i]%2)odd++;
        else even++;
    }
    cout<<endl;
    if(flag&&!odd){
        cout<<"Eulerian"<<endl;
    }else if(flag&&odd==2){
        cout<<"Semi-Eulerian"<<endl;
    }else{
        cout<<"Non-Eulerian"<<endl;
    }
    return 0;
}
```

