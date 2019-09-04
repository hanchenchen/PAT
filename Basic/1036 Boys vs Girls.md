# 1036 **Boys vs Girls** 

```c++
#include<iostream>
#include<algorithm>
#include<vector>
using namespace std;
int boyGrade=101,girlGrade=-1;
string boyName,girlName,boyID,girlID;
int main(){
    int n,x;cin>>n;
    string a,b,c;
    for(int i=0;i<n;i++){
        cin>>a>>b>>c>>x;
        if(b=="M"){
            if(boyGrade>x){
                boyName=a;
                boyID=c;
                boyGrade=x;
            }
        }else{
            if(girlGrade<x){
                girlName=a;
                girlID=c;
                girlGrade=x;
            }
        }
    }
    if(girlGrade==-1){
        cout<<"Absent"<<endl;
    }else{
        cout<<girlName<<" "<<girlID<<endl;
    }
    if(boyGrade==101){
        cout<<"Absent"<<endl;
    }else{
        cout<<boyName<<" "<<boyID<<endl;
    }
    if(girlGrade==-1||boyGrade==101){
        cout<<"NA"<<endl;
    }else{
        cout<<girlGrade-boyGrade<<endl;
    }
    return 0;
}
```

