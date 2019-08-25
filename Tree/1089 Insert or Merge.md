# 1089 Insert or Merge

1. `Merge sort`最后会剩余不是`2`的倍数长度的数组需要`sort`

```c++
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;
vector<int> initial;
vector<int> ordered;
bool ifMerge(vector<int> mid){
    int flag=0,i,j;
    for(i=2;i<initial.size();i*=2){
        for(j=1;j+i<=initial.size();j+=i){
            sort(initial.begin()+j,initial.begin()+j+i);
        }
        if(j<initial.size())sort(initial.begin()+j,initial.end());
        if(flag){
            cout<<"Merge Sort"<<endl<<initial[1];
            for(i=2;i<initial.size();i++){
                cout<<" "<<initial[i];
            }
            return true;
        }
        if(initial==mid)flag=1;
    }
    return false;
    
}
bool ifInsert(vector<int> mid){
    int i=0;
    for(i=1;i<(int)mid.size();i++){
        if(mid[i]<mid[i-1])break;
    }
    int index=i;
    for(;i<(int)mid.size();i++)if(mid[i]!=initial[i])return false;
    sort(mid.begin()+1,mid.begin()+index+1);
    cout<<"Insertion Sort"<<endl<<mid[1];
    for(i=2;i<mid.size();i++){
        cout<<" "<<mid[i];
    }
    return true;
}
int main(){
    int n,x;
    cin>>n;
    initial.push_back(0);
    vector<int> mid;
    mid.push_back(0);
    for(int i=0;i<n;i++){
        cin>>x;
        initial.push_back(x);
    }
    for(int i=0;i<n;i++){
        cin>>x;
        mid.push_back(x);
    }
    ordered=initial;
    sort(ordered.begin()+1,ordered.end());
    if(!ifInsert(mid))ifMerge(mid);
    return 0;
}
```

