# 1016 Phone Bills

⚠️没有通话记录的用户不用输出

```c++
#include<iostream>
#include<map>
#include<vector>
#include<algorithm>
using namespace std;
const int maxN=1005;
/*struct USER{
    string name;
     calls;
}user[maxN];*/
map<string,map<int,int>> calls;
void outputTime(int x){
    printf("%02d:",(x/60/24)%60+1);
    x%=(60*24);
    printf("%02d:",(x/60)%60);
    printf("%02d",x%60);
}
int toNumber(int a,int b,int c){
    return c+60*(b+24*(a-1));
}
int n,m,dayPrice;
int priceHour[24]={0};
int price(int x){
    int day=x/60/24;
    x=x%(60*24);
    int i,sum=0;
    for(i=0;i<x/60;i++){
        sum+=priceHour[i]*60;//cout<<sum<<endl;
    }
    sum+=priceHour[i]*(x%60)+day*dayPrice;
    return sum;
}

int main(){
    //cout<<price(toNumber(28, 15, 41))<<endl;
    //outputTime(toNumber(10, 0, 0));
    for(int i=0;i<24;i++){
        cin>>priceHour[i];
        dayPrice+=60*priceHour[i];
        
    }
    cin>>n;
    int m=0;
    string s1,s3;
    int a,b,c;
    for(int i=0;i<n;i++){
        cin>>s1;
        scanf("%d:%d:%d:%d",&m,&a,&b,&c);
        cin>>s3;
        if(s3=="on-line")calls[s1][toNumber(a,b,c)]=1;
        else calls[s1][toNumber(a,b,c)]=-1;
    }
    map<string,map<int,int>>::iterator iter=calls.begin();
    for(;iter!=calls.end();iter++){
        int total=0,x;
        int flag=1;
        map<int,int>::iterator j=iter->second.begin();
        for(;j!=iter->second.end();j++){
            if(j->second<0)continue;
            map<int,int>::iterator k=j;k++;
            if(k==iter->second.end()||k->second>0)continue;
            if(flag){
                cout<<iter->first<<" ";
                printf("%02d\n",m);
                flag=0;
            }
            outputTime(j->first);
            cout<<" ";
            outputTime(k->first);
            cout<<" "<<k->first-j->first<<" $";
            x=price(k->first)-price(j->first);
            printf("%.2f\n",(double)x/100.0);
            total+=x;
        }
        if(flag==0){
            cout<<"Total amount: $";
            printf("%.2f\n",(double)total/100.0);
        }

    }
    return 0;
}
```

