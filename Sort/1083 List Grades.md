# 1083 List Grades

```c++
#include<iostream>
#include<queue>
#include<vector>
#include<string.h>
#include<set>
#include<algorithm>
using namespace std;
const int maxN=100005;
//const int maxK=10;
//const int maxM=1e5+5;
//const int maxInt=2147483647;
struct STU{
    char name[15];
    char id[15];
    int score =0;
}stu[maxN];
int n;//k,m;
int l,h;
int main(){
    cin>>n;//student num
    for(int i=0;i<n;i++){
        scanf("%s %s %d",stu[i].name,stu[i].id,&stu[i].score);
    }
    int x,y;
    cin>>x>>y;
    l=min(x,y);
    h=max(x,y);
    sort(stu,stu+n,[](const STU a,const STU b){
        if(a.score>=l&&a.score<=h){
            if(b.score>=l&&b.score<=h){
                return a.score>b.score;
            }else{
                return true;
            }
        }else{
            if(b.score>=l&&b.score<=h){
                return false;
            }else{
                return a.score<b.score;
            }
        }
    });
    int num=0;
    for(int i=0;i<n;i++){
        if(stu[i].score>=l&&stu[i].score<=h)num++;
        else break;
    }
    if(num==0){
        cout<<"NONE"<<endl;return 0;
    }
    //cout<<num<<endl;
    for(int i=0;i<num;i++){
        printf("%s %s\n",stu[i].name,stu[i].id);
    }

    return 0;
}

```

