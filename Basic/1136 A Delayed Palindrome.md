# **1136** **A Delayed Palindrome**

```c++
#include <iostream>
#include <string.h>
#include <vector>
#include <math.h>
#include <algorithm>
#include <unordered_map>
#include <climits>
using namespace std;
//const int maxN=1e4+5;
string add(string s1,string s2){
    int i=(int)s1.size()-1,j=(int)s2.size()-1,c=0;
    string s;int x;
    for(;i>=0&&j>=0;i--,j--){
        x=c+s1[i]+s2[j]-'0'-'0';
        s=(char)('0'+x%10)+s;
        c=x/10;
    }
    if(c)s=(char)('0'+c)+s;
    return s;
}
int main() {
    string s,pre;
    cin>>s;
    for(int i=0;i<10;i++){
        pre=s;
        reverse(s.begin(),s.end());
        if(pre==s){
            cout<<s<<" is a palindromic number."<<endl;
            return 0;
        }
        cout<<pre<<" + ";
        cout<<s<<" = ";
        s=add(pre,s);
        cout<<s<<endl;
    }
    cout<<"Not found in 10 iterations."<<endl;
    return 0;
}
```

