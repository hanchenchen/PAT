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
vector<int> initial;
vector<int> ordered;
bool ifHeap(vector<int> init){

}
bool ifInsert(vector<int> init){
    int i=0;
    while(i<initial.size()&&init[i]==ordered[i])i++;
    while(i<initial.size()&&init[i]==initial[i])i++;
    if(i==initial.size())
    for(int i=0;i<;i++){
        if(&&init[i]!=)
    }
}
int main(){
    int n,x;
    cin>>n;
    for(int i=0;i<n;i++){
        cin>>x;
        initial.push(x);
        }
        ordered=initial;
        sort(ordered.begin(),ordered.end());
}
```

