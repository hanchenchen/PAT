# 1153 Decode Registration

```c++
#include <iostream>
#include <string>
#include <vector>
#include <unordered_map>
#include <algorithm>
using namespace std;
const int maxN=1e4+5;
int n,m;
int getNum(string s){
    int x=0;
    for(int i=0;i<s.size();i++){
        x*=10;
        x+=s[i]-'0';
    }
    return x;
}
struct NODE{
    string id,level;
    int site=0,date=0,testee=0,score=0;
    NODE(){
        site=date=testee=0;
    };
    NODE(string s,int x){
        this->id=s;
        this->level=s.substr(0,1);
        this->site=getNum(s.substr(1,3));
        this->date=getNum(s.substr(4,6));
        this->testee=getNum(s.substr(10,3));
        this->score=x;
    }
}node[maxN];

int y;
int main() {
    scanf("%d %d",&n,&m);
    int x;string s;
    for(int i=0;i<n;i++){
        cin>>s>>x;
        node[i]=NODE(s,x);
    }
    sort(node,node+n,[](const NODE &a,const NODE &b){
        if(a.score!=b.score)return a.score>b.score;
        return a.id<b.id;
    });
    for(int i=1;i<=m;i++){
        cin>>x;
        if(x==1){
            cin>>s;int flag=0;
            printf("Case %d: %d ",i,x);
            cout<<s<<endl;
            for(int i=0;i<n;i++){
                if(node[i].level==s){cout<<node[i].id<<" "<<node[i].score<<endl;flag=1;}
            }
            if(flag==0)cout<<"NA"<<endl;
        }else if(x==2){
            cin>>y;int siteNum=0,siteScore=0;
            printf("Case %d: %d %03d\n",i,x,y);
            for(int i=0;i<n;i++){
                if(node[i].site==y){
                    siteNum++;
                    siteScore+=node[i].score;
                }
            }
            if(siteNum==0){
                cout<<"NA"<<endl;
                continue;
            }
            printf("%d %d\n",siteNum,siteScore);
        }else if(x==3){
            cin>>y;
            printf("Case %d: %d %06d\n",i,x,y);
            struct site_num{int site=0;int num=0;};
            vector<site_num> ans;unordered_map<int,int> m;
            for(int j=0;j<n;j++){
                if(node[j].date==y)m[node[j].site]++;
            }
            if(m.size()==0){
                cout<<"NA"<<endl;
                continue;
            }
            for(auto it :m){
                ans.push_back({it.first,it.second});
            }
            sort(ans.begin(),ans.end(),[](const site_num &a,const site_num &b){
                if(a.num!=b.num)return a.num>b.num;
                return a.site<b.site;
            });
            for(int i=0;i<ans.size();i++){
                printf("%03d %d\n",ans[i].site,ans[i].num);
            }
        }
    }
    return 0;
}
```

