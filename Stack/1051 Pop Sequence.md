# **1051** Pop Sequence

| Submit Time        | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
| ------------------ | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
| 8/9/2019, 21:42:29 | Accepted | 25    | [1051](https://pintia.cn/problem-sets/994805342720868352/problems/994805427332562944) | C++ (g++) | 4 ms     | cc   |

| Case | Result   | Run Time | Memory |
| ---- | -------- | -------- | ------ |
| 0    | Accepted | 3 ms     | 412 KB |
| 1    | Accepted | 2 ms     | 412 KB |
| 2    | Accepted | 4 ms     | 384 KB |
| 3    | Accepted | 3 ms     | 384 KB |
| 4    | Accepted | 2 ms     | 384 KB |
| 5    | Accepted | 2 ms     | 416 KB |

```c++
#include<iostream>
#include<algorithm>
#include<stack>
using namespace std;
int m,n,k;
bool func(int arr[]){
    stack<int> st;
    int j=0,i=1;
    for(;i<=n;i++){
        st.push(i);
        if(st.size()>m)return false;
        while(!st.empty()&&arr[j]==st.top()){
            st.pop();
            j++;
        }
    }
    if(st.empty())return true;
    return false;
}
int main(){
    scanf("%d %d %d",&m,&n,&k);
    int arr[n];
    for(int i=0;i<k;i++){
        for(int j=0;j<n;j++){
            scanf("%d",&arr[j]);
        }
        if(func(arr)){
            printf("YES\n");
        }else{
            printf("NO\n");
        }
    }
    return 0;
}
```

