# 1120 **Friend Numbers** 

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<map>
#include<set>
#include<math.h>
using namespace std;
const int maxN=100;
int n,arr[maxN]={0},x;
int getNum(int x){
    int id=0;
    while(x>0){
        id+=x%10;
        x/=10;
    }
    return id;
}
int main(){
    scanf("%d",&n);
    for(int i=0;i<n;i++){
        scanf("%d",&x);
        arr[getNum(x)]++;
    }
    vector<int> ans;
    for(int i=0;i<maxN;i++){
        if(arr[i]>0)ans.push_back(i);
    }
    printf("%d\n",(int)ans.size());
    if(!ans.size())return 0;
    cout<<ans[0];
    for(int i=1;i<ans.size();i++){
        printf(" %d",ans[i]);
    }
    return 0;
}
```

