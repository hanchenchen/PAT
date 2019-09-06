# 1132 **Cut Integer** 

Float Point Exception：➗0

```c++
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;
void divide(string s,long long &a,long long &b,long long &c){
    a=b=c=0;
    int n=(int)s.size()/2,i=0;
    for(;i<n;i++){
        a*=10;c*=10;
        a+=s[i]-'0';c+=s[i]-'0';
    }
    for(;i<s.size();i++){
        b*=10;c*=10;
        b+=s[i]-'0';c+=s[i]-'0';
    }
}
int main() {
    long long n,x,y,z;string s;
    cin>>n;
    for(int i=0;i<n;i++){
        cin>>s;
        divide(s,x,y,z);
        if(x!=0&&y!=0&&z%(x*y)==0){
            printf("Yes\n");
        }else{
            printf("No\n");
        }
    }
}
```

