# 1027  **Colors in Mars**

```c++
#include<iostream>
#include<algorithm>
#include<vector>
using namespace std;
const int maxN =100006;
int a,b,c;
string toMars(int x){
    string s;
    if(x<=9){
        s+=(x+'0');
        return s;
    }
    if(x<=12){
        s+=(x-10+'A');
        return s;
    }
    return s;
}
int main(){
    cin>>a>>b>>c;
    cout<<"#"<<toMars(a/13)+toMars(a%13);
    cout<<toMars(b/13)+toMars(b%13);
    cout<<toMars(c/13)+toMars(c%13);
    return 0;
}
```

