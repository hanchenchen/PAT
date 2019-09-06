# 1152 **Google Recruitment** 

```c++
#include <iostream>
#include <string>
#include <vector>
#include <math.h>
#include <algorithm>
using namespace std;
const int maxN=1e3+5;
int l,k;
bool ifPrime(string s){
    int x=stoi(s);
    int sqr=sqrt(x);
    for(int i=2;i<=sqr;i++){
        if(x%i==0)return false;
    }
    return true;
}
int main() {
    string s;
    cin>>l>>k;
    cin>>s;
    for(int i=0;i<=l-k;i++){
        if(ifPrime(s.substr(i,k))){
            cout<<s.substr(i,k)<<endl;
            return 0;
        }
    }
    cout<<"404"<<endl;
    return 0;
}
```

