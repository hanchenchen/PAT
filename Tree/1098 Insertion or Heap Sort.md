# 1098 Insertion or Heap Sort

1. ⚠️

2. ```c++
   4
   3 4 2 1
   3 4 2 1
     
   Insertion Sort
   2 3 4 1
   ```

```c++
#include<iostream>
#include<vector>
#include<algorithm>
using namespace std;
vector<int> initial;
vector<int> ordered;
bool ifHeap(vector<int> mid){
    int i=(int)initial.size()-1;
    while(i>0&&mid[i]==ordered[i])i--;
    int index=i;
    int temp=mid[index];
    mid[index]=mid[1];
    mid[1]=temp;
    i=1;int j=2;
    while(j<index){
        if(j+1<index&&mid[j+1]>mid[j]){
            j=j+1;
        }
        if(mid[j]>temp){
            mid[i]=mid[j];
            i=j;j=2*i;
        }else
            break;
    }
    mid[i]=temp;
    cout<<"Heap Sort"<<endl<<mid[1];
    for(i=2;i<mid.size();i++){
        cout<<" "<<mid[i];
    }
    return true;
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
    if(!ifInsert(mid))ifHeap(mid);
    return 0;
}

```

