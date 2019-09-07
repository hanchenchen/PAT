# 1140 **Look-and-say Sequence**

```
#include <iostream>
#include <string.h>
#include <vector>
#include <math.h>
#include <algorithm>
#include <unordered_map>
#include <climits>
using namespace std;
//const int maxN=1e4+5;
string func(string s){
    string ans;
    for(int i=0;i<s.size();i++){
        int j=i;
        while(s[j+1]==s[i])j++;
        ans+=s[i];
        ans+=to_string(j-i+1);
        i=j;
    }
    return ans;
}
int main() {
    string s;int n;
    cin>>s>>n;
    for(int i=1;i<n;i++){
        s=func(s);
    }
    cout<<s<<endl;
    return 0;
}

```

