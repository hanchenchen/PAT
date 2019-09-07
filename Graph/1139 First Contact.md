# 1139 First Contact

```c++
#include <iostream>
#include <string.h>
#include <vector>
#include <math.h>
#include <algorithm>
#include <unordered_map>
#include <climits>
using namespace std;
const int maxN=1e4+5;
int n,m;
unordered_map<int,vector<int> > relation;
int main() {
    cin>>n>>m;
    int x,y;int i=0;
    for(;i<m;i++){
        cin>>x>>y;
        relation[x].push_back(y);
        relation[y].push_back(x);
    }
    struct p{int af;int bf;};
    /*for(auto it :relation){
     sort(it.second.begin(),it.second.end(),[](const int &a,const int &b){
     return abs(a)<abs(b);
     });
     }*/
    int k;
    cin>>k;
    for(i=0;i<k;i++){
        cin>>x>>y;
        vector<p>  ans;
        for(auto aFriend :relation[x]){
            if(aFriend*x<0||aFriend==y)continue;
            for(auto aFriendFriend :relation[aFriend]){
                for(auto bFriend :relation[y]){
                    if(bFriend*y<0||bFriend==x)continue;
                    if(aFriendFriend==bFriend){
                        ans.push_back({abs(aFriend),abs(bFriend)});
                        //printf("%04d %04d\n",aFriend,bFriend);
                    }
                }
            }
        }
        sort(ans.begin(),ans.end(),[](const p &x,const p &y){
            if(x.af!=y.af)
                return x.af<y.af;
            return x.bf<y.bf;
        });
        cout<<ans.size()<<endl;
        for(int i=0;i<ans.size();i++){
            printf("%04d %04d\n",ans[i].af,ans[i].bf);
        }
    }
    return 0;
}
```

