# **1014** **Waiting in Line** 

```c++
#include<iostream>
#include<queue>
#include<vector>
using namespace std;
const int maxN=25;
const int maxINT=2147483647;
const int maxK=1005;
int getminute(int hh,int mm){
    return hh*60+mm;
}
int stTime=getminute(8,0);
int edTime=getminute(17,0);
struct CUS{
    int order=0;
    int serviceTime=0;
    int endTime=0;
}cus[maxK];
struct WIN{
    queue<int> qe;
    int endTime=stTime;
}win[maxN];
int main(){
    int n,m,k,q;
    cin>>n>>m>>k>>q;
    for(int i=0;i<k;i++){
        cin>>cus[i].serviceTime;
    }
    cus[k].order=-1;
    cus[k].endTime=stTime;
    for(int j=0;j<n;j++){
        win[j].qe.push(k);
    }
    int firstoutLine=0;
    for(int i=0;i<n*m;i++){
        int goWin=-1,shortestLine=maxINT;
        for(int j=0;j<n;j++){
            if(win[j].qe.size()<shortestLine){
                goWin=j;
                shortestLine=(int)win[j].qe.size();
            }
        }
        if(win[goWin].qe.size()==m){firstoutLine=i;break;}
        win[goWin].qe.push(i);
    }
    
    while(firstoutLine<k){
        int endWin=-1,EndTime=maxINT;
        for(int j=0;j<n;j++){
            //cout<<win[j].endTime<<" ";
            if(EndTime>win[j].endTime){
                EndTime=win[j].endTime;
                endWin=j;
            }
        }
        //cout<<endl;
        //cout<<endl<<i<<" "<<minEndTime<<" "<<minWin<<endl;
        if(!win[endWin].qe.empty()){
            cus[win[endWin].qe.front()].endTime=EndTime;
            //cout<<win[endWin].qe.front()<<" ";
            //printf("%02d:%02d\n",EndTime/60,EndTime%60);
            win[endWin].qe.pop();
            win[endWin].endTime=EndTime+cus[win[endWin].qe.front()].serviceTime;
        }else break;
        int goWin=-1,shortestLine=maxINT;
        for(int j=0;j<n;j++){
            if(win[j].qe.size()<shortestLine){
                goWin=j;
                shortestLine=(int)win[j].qe.size();
            }
        }
        if(firstoutLine<k&&shortestLine<m)win[goWin].qe.push(firstoutLine++);
    }
    for(int j=0;j<n;j++){
        while(!win[j].qe.empty()){
            cus[win[j].qe.front()].endTime=win[j].endTime;
            win[j].qe.pop();
            win[j].endTime+=cus[win[j].qe.front()].serviceTime;
        }
    }
    int ask;
    for(int i=0;i<q;i++){
        cin>>ask;
        if(cus[ask-1].endTime==0||cus[ask-1].endTime-edTime>=cus[ask-1].serviceTime)
            cout<<"Sorry"<<endl;
        else
            printf("%02d:%02d\n",cus[ask-1].endTime/60,cus[ask-1].endTime%60);
    }
    for(int i=0;i<k;i++){
        ask=i;
        //printf("%02d:%02d\n",cus[ask+1].endTime/60,cus[ask+1].endTime%60);
    }
    return 0;
}
```

