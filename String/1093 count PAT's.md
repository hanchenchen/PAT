# 1093 count PAT's

```c++
#include<iostream>
#include<algorithm>
#include<vector>
using namespace std;
const int MOD =1000000007;
int p=0,pa=0,pat=0;
int main(){
    char c;
    while(scanf("%c",&c)){
        if(c=='\n')break;
        if(c=='P'){
            p++;
        }else if(c=='A'){
            pa=(pa+p)%MOD;
        }else{
            pat=(pat+pa)%MOD;
        }
    }
    cout<<pat;
    return 0;
}
```

