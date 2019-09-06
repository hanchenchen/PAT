# 1121 Damn Single

```
#include<iostream>
#include<algorithm>
#include<vector>
#include<string.h>
#include<set>
#include<math.h>
using namespace std;
const int maxN=100000;
int n,arr[maxN]={0},m;
set<int> single;
int main(){
    memset(arr,-1,sizeof(arr));
    scanf("%d",&n);
    int x,y;
    for(int i=0;i<n;i++){
        scanf("%d %d",&x,&y);
        arr[x]=y;
        arr[y]=x;
    }
    scanf("%d",&n);
    for(int i=0;i<n;i++){
         scanf("%d",&x);
        if(single.find(arr[x])!=single.end()){
            single.erase(arr[x]);
        }else{
            single.insert(x);
        }
    }
    printf("%d\n",(int)single.size());
    set<int>::iterator iter=single.begin();
    if(iter!=single.end())printf("%05d",*iter++);
    for(;iter!=single.end();iter++){
        printf(" %05d",*iter);
    }
    return 0;
}
```

