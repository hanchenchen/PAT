# 1012 The Best Rank

```c++
#include<iostream>
#include<map>
#include<vector>
#include<algorithm>
using namespace std;
const int maxN=20005;
struct PEOPLE{
    string id;
    int average=100;
    int programming=0;
    int mathematics=0;
    int english=0;
}people[maxN];
map<string,int> name;
vector<int> C,M,E,A;
int n,m;
int main(){
    
    cin>>n>>m;
    for(int i=0;i<n;i++){
        cin>>people[i].id>>people[i].programming>>people[i].mathematics;
        cin>>people[i].english;
        people[i].average=people[i].mathematics+people[i].programming+people[i].english;
        people[i].average++;
        people[i].average/=3;
        C.push_back(people[i].programming);
        M.push_back(people[i].mathematics);
        E.push_back(people[i].english);
        A.push_back(people[i].average);
        name[people[i].id]=i;
    }
    sort(C.begin(),C.end(),[](int a,int b){return a>b;});
    sort(M.begin(),M.end(),[](int a,int b){return a>b;});
    sort(E.begin(),E.end(),[](int a,int b){return a>b;});
    sort(A.begin(),A.end(),[](int a,int b){return a>b;});
    string s;
    for(int j=0;j<m;j++){
        cin>>s;
        if(name.find(s)==name.end()){
            cout<<"N/A"<<endl;
            continue;
        }
        int i=name[s];
        int a=0,b=0,c=0,d=0;
        while(C[a]>people[i].programming)a++;
        while(M[b]>people[i].mathematics)b++;
        while(E[c]>people[i].english)c++;
        while(A[d]>people[i].average)d++;
        int mini=min(min(a,b),min(c,d));
        cout<<mini+1<<" ";
        if(d==mini){
            cout<<"A"<<endl;
        }else if(a==mini){
            cout<<"C"<<endl;
        }else if(b==mini){
            cout<<"M"<<endl;
        }else if(c==mini){
            cout<<"E"<<endl;
        }
    }
    return 0;
}

```

