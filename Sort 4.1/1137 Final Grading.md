# **1137** **Final Grading** 

```c++
#include <iostream>
#include <string.h>
#include <vector>
#include <math.h>
#include <algorithm>
#include <unordered_map>
#include <climits>
using namespace std;
//const int maxN=1e4+5;
struct NODE {
    string name;
    double programming=-1.0,midTerm=-1.0,finalTerm=-1.0;
    int g=-1;
    NODE(){}
    NODE(const string &s,const double &x,const double &y,const double &z,const int &g){
        this->name=s;
        this->programming=x;
        this->midTerm=y;
        this->finalTerm=z;
        this->g=g;
    }
};int p,m,n;
int main() {
    unordered_map<string,NODE> um;
    cin>>p>>m>>n;
    string s;int x;
    for(int i=0;i<p;i++){
        cin>>s>>x;
        um[s].programming=x;
    }
    for(int i=0;i<m;i++){
        cin>>s>>x;
        um[s].midTerm=x;
    }
    for(int i=0;i<n;i++){
        cin>>s>>x;
        um[s].finalTerm=x;
    }
    vector<NODE> ans;
    for(auto it:um){
        double g=0.0;
        if(it.second.midTerm>it.second.finalTerm){
            g=0.4*it.second.midTerm+0.6*it.second.finalTerm+0.5;
        }else{
            g=it.second.finalTerm;
        }
        if(g>=60&&it.second.programming>=200)
            ans.push_back(NODE(it.first,it.second.programming,it.second.midTerm,it.second.finalTerm,(int)g));
    }
    sort(ans.begin(),ans.end(),[](const NODE &a,const NODE &b){
        if(a.g!=b.g)return a.g>b.g;
        return a.name<b.name;
    });
    for(int i=0;i<ans.size();i++){
        cout<<ans[i].name;
        printf(" %.0f %.0f %.0f %d\n",ans[i].programming,ans[i].midTerm,ans[i].finalTerm,ans[i].g);
    }
    return 0;
}
```

