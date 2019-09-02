# 1050 **String Subtraction**

```c++
#include<iostream>
#include<map>
#include<vector>
#include<string.h>
#include<set>
#include<algorithm>
using namespace std;
int main(){
    string str1,str2;
    getline(cin,str2);
    getline(cin,str1);
    int arr1[300]={0};
    for(int i=0;i<str1.size();i++){
        arr1[str1[i]]++;
    }
    for(int i=0;i<str2.size();i++){
        if(!arr1[str2[i]])cout<<str2[i];
    }
    return 0;
}
```

