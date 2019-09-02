# **1025** **PAT Ranking**

```c++
#include<iostream>
#include<map>
#include<vector>
#include<algorithm>
using namespace std;
const int maxN=105;
const int maxNK=105*300;
struct STU{
    string name;
    int grade=0;
    int pos=0;
}stu[maxNK];
vector<int> local[maxN];
vector<int> final;
int n,k;int x=0;
int main(){
    cin>>n;string s;
    for(int i=0;i<n;i++){
        cin>>k;
        for(int j=0;j<k;j++){
            cin>>stu[x].name;
            cin>>stu[x].grade;
            stu[x].pos=i;
            local[i].push_back(stu[x].grade);
            final.push_back(stu[x++].grade);
        }
        sort(local[i].begin(),local[i].end(),[](int a,int b){return a>b;});
    }
    sort(final.begin(),final.end(),[](int a,int b){return a>b;});
    map<int,int> f;
    
    sort(stu,stu+x,[](STU a,STU b){
        if(a.grade==b.grade)return a.name<b.name;
        return a.grade>b.grade;
        
    });
    cout<<x<<endl;int r=1;
    for(int i=0;i<x;i++){
        cout<<stu[i].name<<" ";
        if(i>0&&stu[i].grade!=stu[i-1].grade)r=i+1;
        cout<<r<<" "<<stu[i].pos+1<<" ";
        int v=0;
        while(v<local[stu[i].pos].size()&&local[stu[i].pos][v]>stu[i].grade)v++;
        cout<<v+1<<endl;
    }
    return 0;
}
```

