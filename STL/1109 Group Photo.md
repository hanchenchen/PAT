# 1109 **Group Photo**

```c++
#include<iostream>
#include<algorithm>
#include<vector>
#include<map>
#include<math.h>
using namespace std;
const int maxN=1e4+5;
const int maxK=15;
struct NODE{
    int height=0;
    string name;
}node[maxN];
int n,row[maxK]={0};
vector<int> formation;
int main(){
    int n=0,k;
    cin>>n>>k;
    fill(row,row+maxK,n/k);
    row[k-1]+=(n%k);
    for(int i=0;i<n;i++){
        cin>>node[i].name>>node[i].height;
    }
    sort(node,node+n,[](NODE a,NODE b){
        if(a.height!=b.height)return a.height>b.height;
        return a.name<b.name;
    });
    int j=k-1,left=1;
    for(int i=0;i<=n;i++){
        if(formation.size()>=row[j]){
            cout<<node[formation[0]].name;
            for(int k=1;k<formation.size();k++){
                cout<<" "<<node[formation[k]].name;
            }
            formation.clear();
            left=1;
            j--;cout<<endl;
            if(j<0)break;
            
        }
        if(left){
            formation.push_back(i);
            left=0;
        }else{
            formation.insert(formation.begin(), i);
            left=1;
        }  
    }
    return 0;
}

```

