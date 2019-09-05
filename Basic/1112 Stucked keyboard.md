# 1112 Stucked keyboard

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<map>
#include<queue>
#include<math.h>
using namespace std;
int k,ifBroken[200],vis[200]={0};
vector<int> v[200];
string s;
int main(){
    cin>>k>>s;
    //cout<<(int)'_'<<(int)'a'<<endl;
    for(int i=0;i<s.size();i++){
        int j=i;
        while(s[j+1]==s[i])j++;
        v[s[i]].push_back(j-i+1);
        i=j;
    }
    for(int i='0';i<='9';i++){
        int j=0;
        for(;j<v[i].size();j++){
            if(v[i][j]%k!=0)break;
        }
        if(j==v[i].size()&&v[i].size()!=0)ifBroken[i]=1;
    }
    for(int i='a'-2;i<='z';i++){
        int j=0;
        for(;j<v[i].size();j++){
            //cout<<v[i][j]<<(char)i<<endl;
            if(v[i][j]%k!=0)break;
        }
        if(j==v[i].size()&&v[i].size()!=0)ifBroken[i]=1;
    }
    for(int i=0;i<s.size();i++){
        if(ifBroken[s[i]]&&!vis[s[i]]){
            cout<<s[i];
            vis[s[i]]=1;
        }
    }
    cout<<endl;
    for(int i=0;i<s.size();i++){
        cout<<s[i];
        if(ifBroken[s[i]])i+=k-1;
    }
    return 0;
}
```

