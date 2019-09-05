# 1155 **Heap Paths**

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<map>
#include<queue>
#include<math.h>
using namespace std;
const int maxN=1005;
int n,level[maxN]={0},ifmax=0,ifmin=0;
vector<int> path;
void func(int x){
    path.push_back(x);
    if(2*x+1<=n){
        func(2*x+1);
        if(level[x]>level[2*x+1])ifmax=1;
        if(level[x]<level[2*x+1])ifmin=1;
    }
    if(2*x<=n){
        func(2*x);
        if(level[x]>level[2*x])ifmax=1;
        if(level[x]<level[2*x])ifmin=1;
    }
    else{
        cout<<level[path[0]];
        for(int i=1;i<path.size();i++){
            cout<<" "<<level[path[i]];
        }
        cout<<endl;
    }
    path.pop_back();
}
int main(){
    cin>>n;
    for(int i=1;i<=n;i++){
        scanf("%d",&level[i]);
    }
    func(1);
    if(ifmax&&!ifmin){
        printf("Max Heap\n");
    }else if(!ifmax&&ifmin){
        printf("Min Heap\n");
    }else{
        printf("Not Heap\n");
    }
    return 0;
}
```

