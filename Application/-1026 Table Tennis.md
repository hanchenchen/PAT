# **-1026** **Table Tennis**

#### 28/30

| Submit Time         | Status             | Score | Problem                                                      | Compiler  | Run Time | User |
| ------------------- | ------------------ | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
| 8/31/2019, 23:10:12 | Partially Accepted | 28    | [1026](https://pintia.cn/problem-sets/994805342720868352/problems/994805472333250560) | C++ (g++) | 9 ms     | cc   |

| Case | Result       | Run Time | Memory |
| ---- | ------------ | -------- | ------ |
| 0    | Accepted     | 3 ms     | 416 KB |
| 1    | Accepted     | 3 ms     | 424 KB |
| 2    | Accepted     | 3 ms     | 424 KB |
| 3    | Wrong Answer | 3 ms     | 424 KB |
| 4    | Accepted     | 2 ms     | 512 KB |
| 5    | Accepted     | 4 ms     | 384 KB |
| 6    | Accepted     | 3 ms     | 384 KB |
| 7    | Accepted     | 3 ms     | 356 KB |
| 8    | Accepted     | 9 ms     | 680 KB |

```
#include<iostream>
#include<queue>
#include<vector>
#include<algorithm>
using namespace std;
const int maxN=10005;
const int maxINT=2147483647;
const int maxK=105;
int getSecond(int hh,int mm,int ss){
    return hh*60*60+mm*60+ss;
}
int stTime=getSecond(8,0,0);
int edTime=getSecond(21,0,0);
struct PLAYER{
    int vip=0;
    int usingTime=0;
    int comeTime=0;
    int endTime=0;
}player[maxN];
struct TABLE{
    int vip=0;
    int endTime=stTime;
}table[maxK];
queue<PLAYER> pt;
queue<PLAYER> vip;
void output(int t1,int t2){
    if(t1>=t2){
        printf("%02d:%02d:%02d %02d:%02d:%02d 0\n",
               t1/3600,(t1%3600)/60,t1%60,
               t1/3600,(t1%3600)/60,t1%60);
        return;
    }
    int x=t2-t1;
    printf("%02d:%02d:%02d %02d:%02d:%02d %d\n",
           t1/3600,(t1%3600)/60,t1%60,
           t2/3600,(t2%3600)/60,t2%60,
           (x+30)/60);
}
int times[maxK]={0};
int main(){
    int n,m,k;
    cin>>n;
    int hh,mm,ss;
    for(int i=0;i<n;i++){
        scanf("%d:%d:%d ",&hh,&mm,&ss);
        player[i].comeTime=getSecond(hh,mm,ss);
        cin>>player[i].usingTime;
        if(player[i].usingTime>120)player[i].usingTime=120;
        player[i].usingTime*=60;
        cin>>player[i].vip;
    }
    sort(player,player+n,[](PLAYER a,PLAYER b)
         {return a.comeTime<b.comeTime;});
    cin>>k>>m;
    int x;
    for(int i=0;i<m;i++){
        cin>>x;
        table[x].vip=1;
    }
    for(int i=0;i<n;i++){
        if(player[i].vip)vip.push(player[i]);
        else pt.push(player[i]);
    }
    for(int j=0;j<n;j++){
        int tableNum=-1,tableTime=maxINT;
        int viptableNum=-1,viptableTime=maxINT;
        for(int i=1;i<=k;i++){
            if(tableTime>table[i].endTime){
                tableTime=table[i].endTime;
                tableNum=i;
            }
            if(viptableTime>table[i].endTime&&table[i].vip){
                viptableTime=table[i].endTime;
                viptableNum=i;
            }
        }
        PLAYER p;p.comeTime=maxINT;
        
        if(tableTime>=edTime)break;
        if(viptableTime==tableTime){
            if(!vip.empty()){//vip等候
                if(tableTime>=vip.front().comeTime){//vip 早于桌子
                    //cout<<" 1"<<viptableTime<<endl;
                    output(vip.front().comeTime, tableTime);times[viptableNum]++;
                    table[viptableNum].endTime=tableTime+vip.front().usingTime;
                    vip.pop();
                    continue;
                }else{
                    p=vip.front();
                }
            }
            if(!pt.empty()){//普通等候
                if(tableTime>=pt.front().comeTime){//pt 早于桌子
                    //cout<<" 2"<<tableNum<<endl;
                    output(pt.front().comeTime, tableTime);times[tableNum]++;
                    table[tableNum].endTime=tableTime+pt.front().usingTime;
                    pt.pop();
                    continue;
                }else{//都晚于桌子
                    if(pt.front().comeTime<p.comeTime){//pt早于vip
                        p=pt.front();
                    }else{//vip 早于pt
                    }
                }
            }else{//vip 且无pt等候

            }
            if(p.vip){
                //cout<<" 3.1 "<<viptableTime<<endl;
                output(vip.front().comeTime, vip.front().comeTime);times[viptableNum]++;
                table[viptableNum].endTime=vip.front().comeTime+vip.front().usingTime;
                vip.pop();
                continue;
            }else{
                //cout<<" 3.2 "<<tableNum<<endl;
                output(p.comeTime, p.comeTime);times[tableNum]++;
                table[tableNum].endTime=p.comeTime+p.usingTime;
                pt.pop();
            }

        }else{
            if(!vip.empty()){//vip等候
                p=vip.front();
            }
            if(!pt.empty()){//普通等候
                if(p.comeTime>pt.front().comeTime){//普通先于 vip
                    p=pt.front();
                }
            }
            if(p.comeTime==maxINT)continue;
            if(p.comeTime<tableTime){
                //cout<<" 4"<<tableNum<<endl;
                output(p.comeTime, tableTime);times[tableNum]++;
                table[tableNum].endTime=tableTime+p.usingTime;
                if(p.vip)vip.pop();
                else pt.pop();
            }else{
                if(p.vip&&viptableTime<=vip.front().comeTime){
                    //cout<<"! "<<viptableNum<<endl;
                    output(vip.front().comeTime, vip.front().comeTime);times[viptableNum]++;
                    table[viptableNum].endTime=vip.front().comeTime+vip.front().usingTime;
                    vip.pop();
                    continue;
                }
                //cout<<" 5"<<tableNum<<endl;
                output(p.comeTime, p.comeTime);times[tableNum]++;
                table[tableNum].endTime=p.comeTime+p.usingTime;
                if(p.vip)vip.pop();
                else pt.pop();
            }
            
        }
    }
    cout<<times[1];
    for(int i=2;i<=k;i++){
        cout<<" "<<times[i];
    }
    return 0;
}
```

##### WA

```c++
#include<iostream>
#include<queue>
#include<vector>
#include<map>
#include<algorithm>
using namespace std;
const int maxN=10005;
const int maxINT=2147483647;
const int maxK=105;
int getSecond(int hh,int mm,int ss){
    return hh*60*60+mm*60+ss;
}
int stTime=getSecond(8,0,0);
int edTime=getSecond(21,0,0);
struct PLAYER{
    int vip=0;
    int usingTime=0;
    int comeTime=0;
    int serveTime=0;
}player[maxN];
struct TABLE{
    int vip=0;
    int endTime=stTime;
}table[maxK];
queue<int> pt;
queue<int> vip;
void output(int t1,int t2){
    if(t1>=t2){
        printf("%02d:%02d:%02d %02d:%02d:%02d 0\n",
               t1/3600,(t1%3600)/60,t1%60,
               t1/3600,(t1%3600)/60,t1%60);
        return;
    }
    int x=t2-t1;
    printf("%02d:%02d:%02d %02d:%02d:%02d %d\n",
           t1/3600,(t1%3600)/60,t1%60,
           t2/3600,(t2%3600)/60,t2%60,
           (x+30)/60);
}
int times[maxK]={0};
int main(){
    int n,m,k;
    cin>>n;
    int hh,mm,ss;
    for(int i=0;i<n;i++){
        scanf("%d:%d:%d ",&hh,&mm,&ss);
        player[i].comeTime=getSecond(hh,mm,ss);
        cin>>player[i].usingTime;
        if(player[i].usingTime>120)player[i].usingTime=120;
        player[i].usingTime*=60;
        cin>>player[i].vip;
    }
    sort(player,player+n,[](PLAYER a,PLAYER b)
         {return a.comeTime<b.comeTime;});
    cin>>k>>m;
    int x;
    for(int i=0;i<m;i++){
        cin>>x;
        table[x].vip=1;
    }
    for(int i=0;i<n;i++){
        if(player[i].vip)vip.push(i);
        else pt.push(i);
    }
    for(int j=0;j<n;j++){
        int tableNum=-1,tableTime=maxINT;
        int viptableNum=-1,viptableTime=maxINT;
        for(int i=1;i<=k;i++){
            if(tableTime>table[i].endTime){
                tableTime=table[i].endTime;
                tableNum=i;
            }
            if(viptableTime>table[i].endTime&&table[i].vip){
                viptableTime=table[i].endTime;
                viptableNum=i;
            }
        }
        PLAYER p;p.comeTime=maxINT;
        
        if(tableTime>=edTime)break;
        if(viptableTime==tableTime){
            if(!vip.empty()){//vip等候
                if(tableTime>=player[vip.front()].comeTime){//vip 早于桌子
                    //cout<<" 1"<<viptableTime<<endl;
                    player[vip.front()].serveTime=tableTime;
                    times[viptableNum]++;
                    table[viptableNum].endTime=tableTime+player[vip.front()].usingTime;
                    vip.pop();
                    continue;
                }else{
                    p=player[vip.front()];
                }
            }
            if(!pt.empty()){//普通等候
                if(tableTime>=player[pt.front()].comeTime){//pt 早于桌子
                    //cout<<" 2"<<tableNum<<endl;
                    player[pt.front()].serveTime=tableTime;
                    times[tableNum]++;
                    table[tableNum].endTime=tableTime+player[pt.front()].usingTime;
                    pt.pop();
                    continue;
                }else{//都晚于桌子
                    if(player[pt.front()].comeTime<p.comeTime){//pt早于vip
                        p=player[pt.front()];
                    }else{//vip 早于pt
                    }
                }
            }else{//vip 且无pt等候

            }
            if(p.vip){
                //cout<<" 3.1 "<<viptableTime<<endl;
                player[vip.front()].serveTime=player[vip.front()].comeTime;
                times[viptableNum]++;
                table[viptableNum].endTime=player[vip.front()].comeTime+player[vip.front()].usingTime;
                vip.pop();
                continue;
            }else{
                //cout<<" 3.2 "<<tableNum<<endl;
                player[pt.front()].serveTime=player[pt.front()].comeTime;
                times[tableNum]++;
                table[tableNum].endTime=p.comeTime+p.usingTime;
                pt.pop();
            }

        }else{
            if(!vip.empty()){//vip等候
                p=player[vip.front()];
            }
            if(!pt.empty()){//普通等候
                if(p.comeTime>player[pt.front()].comeTime){//普通先于 vip
                    p=player[pt.front()];
                }
            }
            if(p.comeTime==maxINT)continue;
            if(p.comeTime<tableTime){
                //cout<<" 4"<<tableNum<<endl;
                times[tableNum]++;
                table[tableNum].endTime=tableTime+p.usingTime;
                if(p.vip){
                    player[vip.front()].serveTime=tableTime;
                    vip.pop();
                }
                else {
                    player[pt.front()].serveTime=tableTime;
                    pt.pop();
                }
            }else{
                if(p.vip&&viptableTime<=player[vip.front()].comeTime){
                    //cout<<"! "<<viptableNum<<endl;
                    player[vip.front()].serveTime=player[vip.front()].comeTime;
                    times[viptableNum]++;
                table[viptableNum].endTime=player[vip.front()].comeTime
                    +player[vip.front()].usingTime;
                    vip.pop();
                    continue;
                }
                //cout<<" 5"<<tableNum<<endl;
                times[tableNum]++;
                table[tableNum].endTime=p.comeTime+p.usingTime;
                if(p.vip)vip.pop();
                else pt.pop();
                if(p.vip){
                    player[vip.front()].serveTime=player[vip.front()].comeTime;
                    vip.pop();
                }
                else {
                    player[pt.front()].serveTime=player[pt.front()].comeTime;
                    pt.pop();
                }
            }
            
        }
    }
    sort(player,player+n,[](PLAYER a,PLAYER b)
         {return a.serveTime<b.serveTime;});
    for(int i=0;i<n;i++){
        output(player[i].comeTime,player[i].serveTime);
    }
    cout<<times[1];
    for(int i=2;i<=k;i++){
        cout<<" "<<times[i];
    }
    return 0;
}

```

```c++
#include<iostream>
#include<queue>
#include<vector>
#include<set>
#include<algorithm>
using namespace std;
const int maxN=10005;
const int maxINT=2147483647;
const int maxK=105;
int getSecond(int hh,int mm,int ss){
    return hh*60*60+mm*60+ss;
}
int stTime=getSecond(8,0,0);
int edTime=getSecond(21,0,0);
struct PLAYER{
    int vip=0;
    int usingTime=0;
    int comeTime=0;
    int endTime=0;
}player[maxN];
struct TABLE{
    int endTime=stTime;
    int num=0;
    int vip=0;
}table[maxK];
queue<int> pt;
queue<int> vip;
set<TABLE> pTable;
set<TABLE> vipTable;
void output(int t1,int t2){
    if(t1>=t2){
        printf("%02d:%02d:%02d %02d:%02d:%02d 0\n",
               t1/3600,(t1%3600)/60,t1%60,
               t1/3600,(t1%3600)/60,t1%60);
        return;
    }
    int x=t2-t1;
    printf("%02d:%02d:%02d %02d:%02d:%02d %d\n",
           t1/3600,(t1%3600)/60,t1%60,
           t2/3600,(t2%3600)/60,t2%60,
           (x+30)/60);
}
int times[maxK]={0};
int main(){
    int n,m,k=0;
    cin>>n;
    int hh,mm,ss;
    for(int i=1;i<=n;i++){
        scanf("%d:%d:%d ",&hh,&mm,&ss);
        player[i].comeTime=getSecond(hh,mm,ss);
        cin>>player[i].usingTime;
        if(player[i].usingTime>120)player[i].usingTime=120;
        player[i].usingTime*=60;
        cin>>player[i].vip;
    }
    sort(player,player+n,[](PLAYER a,PLAYER b)
         {return a.comeTime<b.comeTime;});
    cin>>k>>m;
    int x;
    for(int i=0;i<m;i++){
        cin>>x;
        table[x].vip=1;
    }
    for(int i=0;i<k;i++){
        table[i].num=i+1;//1-k
        if(table[i].vip)vipTable.insert(table[i]);
        else pTable.insert(table[i]);
    }
    for(int i=0;i<n;i++){
        if(player[i].vip)vip.push(i);
        else pt.push(i);
    }
    //queue<PLAYER> pt;
    //queue<PLAYER> vip;
    //set<TABLE> pTable;
    //set<TABLE> vipTable;
    set<TABLE> availTable;
    set<TABLE> vipAvailTable;
    queue<int> waiting;
    queue<int> VIPwaiting;
    for(int i=getSecond(8,0,0);i<=getSecond(21,0,0);i++){
        if(i>=pTable.begin()->endTime){
            availTable.insert(*pTable.begin());
            pTable.erase(pTable.begin());
        }
        if(i>=vipTable.begin()->endTime){
            vipAvailTable.insert(*vipTable.begin());
            vipTable.erase(vipTable.begin());
        }
        if(i>=player[pt.front()].comeTime){
            waiting.push(pt.front());
            pt.pop();
        }
        if(i>=player[vip.front()].comeTime){
            VIPwaiting.push(vip.front());
            vip.pop();
        }
        if(!VIPwaiting.empty()&&!vipAvailTable.empty()){
            output(player[ VIPwaiting.front()].comeTime, i);
            VIPwaiting.pop();vipTable.erase(vipTable.begin());
            times[vipAvailTable.begin()->num]++;
            continue;
        }
        if(player[VIPwaiting.front()].comeTime<=player[waiting.front()].comeTime){
            if(!vipAvailTable.empty()){
                
            }else if(!availTable.empty()){
                
            }
        }

    }
    for(int j=0;j<n;j++){
        int tableNum=-1,tableTime=maxINT;
        int viptableNum=-1,viptableTime=maxINT;
        for(int i=1;i<=k;i++){
            if(tableTime>table[i].endTime){
                tableTime=table[i].endTime;
                tableNum=i;
            }
            if(viptableTime>table[i].endTime&&table[i].vip){
                viptableTime=table[i].endTime;
                viptableNum=i;
            }
        }
        PLAYER p;p.comeTime=maxINT;
        
        if(tableTime>=edTime)break;
        if(viptableTime==tableTime){
            if(!vip.empty()){//vip等候
                if(tableTime>=vip.front().comeTime){//vip 早于桌子
                    //cout<<" 1"<<viptableTime<<endl;
                    output(vip.front().comeTime, tableTime);times[viptableNum]++;
                    table[viptableNum].endTime=tableTime+vip.front().usingTime;
                    vip.pop();
                    continue;
                }else{
                    p=vip.front();
                }
            }
            if(!pt.empty()){//普通等候
                if(tableTime>=pt.front().comeTime){//pt 早于桌子
                    //cout<<" 2"<<tableNum<<endl;
                    output(pt.front().comeTime, tableTime);times[tableNum]++;
                    table[tableNum].endTime=tableTime+pt.front().usingTime;
                    pt.pop();
                    continue;
                }else{//都晚于桌子
                    if(pt.front().comeTime<p.comeTime){//pt早于vip
                        p=pt.front();
                    }else{//vip 早于pt
                    }
                }
            }else{//vip 且无pt等候
                
            }
            if(p.vip){
                //cout<<" 3.1 "<<viptableTime<<endl;
                output(vip.front().comeTime, vip.front().comeTime);times[viptableNum]++;
                table[viptableNum].endTime=vip.front().comeTime+vip.front().usingTime;
                vip.pop();
                continue;
            }else{
                //cout<<" 3.2 "<<tableNum<<endl;
                output(p.comeTime, p.comeTime);times[tableNum]++;
                table[tableNum].endTime=p.comeTime+p.usingTime;
                pt.pop();
            }
            
        }else{
            if(!vip.empty()){//vip等候
                p=vip.front();
            }
            if(!pt.empty()){//普通等候
                if(p.comeTime>pt.front().comeTime){//普通先于 vip
                    p=pt.front();
                }
            }
            if(p.comeTime==maxINT)continue;
            if(p.comeTime<tableTime){
                //cout<<" 4"<<tableNum<<endl;
                output(p.comeTime, tableTime);times[tableNum]++;
                table[tableNum].endTime=tableTime+p.usingTime;
                if(p.vip)vip.pop();
                else pt.pop();
            }else{
                if(p.vip&&viptableTime<=vip.front().comeTime){
                    //cout<<"! "<<viptableNum<<endl;
                    output(vip.front().comeTime, vip.front().comeTime);times[viptableNum]++;
                    table[viptableNum].endTime=vip.front().comeTime+vip.front().usingTime;
                    vip.pop();
                    continue;
                }
                //cout<<" 5"<<tableNum<<endl;
                output(p.comeTime, p.comeTime);times[tableNum]++;
                table[tableNum].endTime=p.comeTime+p.usingTime;
                if(p.vip)vip.pop();
                else pt.pop();
            }
            
        }
    }
    cout<<times[1];
    for(int i=2;i<=k;i++){
        cout<<" "<<times[i];
    }
    return 0;
}

```





#### 使用class

```c++

#include"all.h"//#include<bits/stdc++.h>
using namespace std;
int getSecond(string time);
string getTime(int second);

class Player{
private:
    int arriveTime;
    int playTime;
public:
    Player(string arriveTime_ = "",int playTime_ = 0);
    int getArriveTime() const;
    int getPlayTime() const;
    bool operator<(const Player& p2) const;
};
Player::Player(string arriveTime_ ,int playTime_ ){
    arriveTime=getSecond(arriveTime_);
    playTime=playTime_;
}
int Player::getArriveTime() const{
    return arriveTime;
}
int Player::getPlayTime() const{
    return playTime;
}
bool Player::operator<(const Player& p2) const{
    return getArriveTime()<p2.getArriveTime();
}

const int maxN=10000+5;
class PlayerList{
private:
    int playerNum;
    Player* list;
public:
    PlayerList();
    void sortList();
    bool pushBack(Player p);
    Player* getFront();
}ordinaryPlayer,VIPplayer;
PlayerList::PlayerList(){
    playerNum=0;
    list=new Player[maxN];
}
void PlayerList::sortList(){
    sort(list,list+playerNum);
}
bool PlayerList::pushBack(Player p){
    if(playerNum>=maxN)return false;
    list[playerNum++]=p;
    return true;
}
Player* PlayerList::getFront(){
    if(!playerNum--)return NULL;
    Player* p=list;
    list++;
    return p;
}

class Table{
private:
    int remainTime;
    int ifVIP;
public:
    Table();
    void setTime(int time);
    void setVIP();
    int getTime();
};
Table::Table(){
    remainTime=0;
    ifVIP=0;
}
void Table::setTime(int time){
    remainTime=time;
}
void Table::setVIP(){
    ifVIP=1;
}
int Table::getTime(){
    return remainTime;
}

const int maxK=100+5;
class TableList{
private:
    int tableNum;
    Table* list;
public:
    TableList();
    void setTableNum(int tableNum_);
    void setVIP(int index);
    vector<int> findTable();
    vector<int> getTable(int& currentTime);
}table;
TableList::TableList(){
    tableNum=0;
    list=new Table[maxK];
}
void TableList::setTableNum(int tableNum_){
    tableNum=tableNum_;
}
void TableList::setVIP(int index){
    list[index].setVIP();
}
vector<int> TableList::findTable(){
    vector<int> tl;
    for(int i=1;i<=tableNum;i++){
        if(!list[i].getTime())tl.push_back(i);
    }
    return tl;
}
vector<int> TableList::getTable(int& currentTime){
    int minTime=2*60+5;
    for(int i=1;i<=tableNum;i++){
        minTime=min(minTime,list[i].getTime());
    }
    currentTime+=minTime;
    for(int i=1;i<=tableNum;i++){
        list[i].setTime(list[i].getTime()-minTime);
    }
    return TableList::findTable();
}

int main(){
    int n,k,m;
    string arriveTime;
    int playTime,vip;
    cin>>n;
    for(int i=0;i<n;i++){
        cin>>arriveTime>>playTime>>vip;
        if(vip){
            VIPplayer.pushBack(Player(arriveTimae,playTime));
        }else{
            ordinaryPlayer.pushBack(Player(arriveTime,playTime));
        }
    }
    cin>>k>>m;
    for(int i=0;i<m;i++){
        cin>>vip;
        table.setVIP(vip);
    }
    int currentTime=getSecond("08:00:00");
    
    return 0;
}





int getSecond(string time){
    int h=(time[0]-'0')*10+time[1]-'0';
    int m=h*60+(time[3]-'0')*10+time[4]-'0';
    int s=m*60+(time[6]-'0')*10+time[7]-'0';
    return s;
}
string getTime(int second){
    int s=second%60;
    int m=second/60;
    int h=m/60;
    m=m%60;
    string time="00:00:00";
    time[0]=h/10+'0';time[1]=h%10+'0';
    time[3]=m/10+'0';time[4]=m%10+'0';
    time[6]=s/10+'0';time[7]=s%10+'0';
    return time;
}

```

