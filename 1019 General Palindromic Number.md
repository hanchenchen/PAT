# **1019** General Palindromic Number

| Submit Time         | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
| ------------------- | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
| 7/12/2019, 12:17:20 | Accepted | 20    | [1019](https://pintia.cn/problem-sets/994805342720868352/problems/994805487143337984) | C++ (g++) | 2 ms     | cc   |

| Case | Result   | Run Time | Memory |
| ---- | -------- | -------- | ------ |
| 0    | Accepted | 2 ms     | 352 KB |
| 1    | Accepted | 2 ms     | 512 KB |
| 2    | Accepted | 2 ms     | 384 KB |
| 3    | Accepted | 2 ms     | 424 KB |
| 4    | Accepted | 2 ms     | 384 KB |
| 5    | Accepted | 2 ms     | 384 KB |
| 6    | Accepted | 2 ms     | 384 KB |
| 7    | Accepted | 2 ms     | 384 KB |

```c++
//
//  main.cpp
//  dome
//
//  Created by cc on 2019/7/12.
//  Copyright © 2019 cc. All rights reserved.
//

#include <iostream>
#include <vector>
using namespace std;
#define INT_MAX 2147483647
int main() {
    int n,b;
    cin>>n;
    cin>>b;
    if(n==0){
        cout<<"Yes"<<endl<<"0";
        return 0;
    }
    int i=b;
    if(i<=INT_MAX/b){
        while(i<=n){
            i*=b;
            if(i>n)break;
        }
        i/=b;
    }else{
        if(i>n)i=1;
        else i=b;
    }
    int x;
    vector<int> v;
    while(i>0){
        x=n/i;
        v.push_back(x);
        n=n-x*i;
        i/=b;
    }
    int len=(int)v.size();
    for(int j=0;j<len/2;j++){
        if(v[j]!=v[len-1-j]){
            cout<<"No"<<endl;
            cout<<v[0];
            for(int a=1;a<len;a++){
                cout<<" "<<v[a];
            }
            return 0;
            
        }
    }
    cout<<"Yes"<<endl;
    cout<<v[0];
    for(int j=1;j<len;j++){
        cout<<" "<<v[j];
    }
    //cout<<INT_MAX<<endl;
    return 0;
}

```

