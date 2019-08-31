# 1033 To Fill or Not to Fill

1. 把路程划分成一个一个的价格相等区间，每个价格相等区间的价格等于该区间前可以买到的最便宜的汽油的价格

```c++
#include<iostream>
#include<map>
#include<set>
#include<queue>
#include<algorithm>
using namespace std;
const double MAX=2147483647;
map<double,double> Pos_Price;
int main(){
    double cmax,d,davg;
    int n;
    cin>>cmax>>d>>davg>>n;
    if(n*davg==0){
        cout<<"The maximum travel distance = 0.00";
        return 0;
    }
    double x,y;
    for(int i=0;i<n;i++){
        cin>>y>>x;
        Pos_Price[x]=y;
        if(Pos_Price.find(x+cmax*davg)==Pos_Price.end())
            Pos_Price[x+cmax*davg]=MAX;
    }
    Pos_Price[d]=MAX;
    map<double,double>::iterator pre=Pos_Price.begin();
    map<double,double>::iterator iter=Pos_Price.begin();
    if(iter->first!=0){
        cout<<"The maximum travel distance = 0.00";
        return 0;
    }
    iter++;
    double ans=0.0;
    while(iter!=Pos_Price.end()){
        map<double,double>::iterator jter=iter;
        double minPrice=MAX;
        while(jter!=Pos_Price.begin()){
            jter--;
            if(jter->first<iter->first-cmax*davg)break;
            if(jter->second<minPrice){
                minPrice=jter->second;
            }
        }
        if(minPrice==MAX){
            cout<<"The maximum travel distance = ";
            printf("%.2f",pre->first);
            return 0;
        }
        ans+=(iter->first-pre->first)/davg*minPrice;
        pre=iter;
        if(iter->first==d)break;
        iter++;
    }
    printf("%.2f",ans);
    return 0;
}

```

