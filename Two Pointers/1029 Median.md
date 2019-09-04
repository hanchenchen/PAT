# 1029 Median

```c++
#include<iostream>
#include<algorithm>
#include<vector>
using namespace std;
const int maxN=400005;
int arr[maxN];
int main(){
    int n;
    cin>>n;
    for(int i=0;i<n;i++){
        cin>>arr[i];
    }
    int m;
    cin>>m;
    for(int i=n;i<m+n;i++){
        cin>>arr[i];
    }
    sort(arr,arr+n+m);
    cout<<arr[(n+m-1)/2];
    return 0;
}

```

