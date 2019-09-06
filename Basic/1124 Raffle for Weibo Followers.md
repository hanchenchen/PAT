# 1124 **Raffle for Weibo Followers**

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<string.h>
#include<map>
#include<math.h>
using namespace std;
const int maxN=1000+5;
int n,m,s;
map<string,int> ifWin;
int main(){
    scanf("%d %d %d",&m,&n,&s);
    string name;int c=-1,flag=0;
    for(int i=1;i<=m;i++){
        cin>>name;
        if(ifWin[name])continue;
        if(i==s)c=1;
        c--;
        if(c==0){
            flag=1;
            cout<<name<<endl;
            ifWin[name]=1;
            c=n;
        }
    }
    if(!flag)cout<<"Keep going..."<<endl;
    return 0;
}
```

