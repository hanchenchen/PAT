# 1153 Decode Registration

1. `测试点3 TLE`

   用空间不一定换得到时间...

   200ms大约可以循环4*10^7^，所以每次循环一遍是够的

   ```c++
   #include <iostream>
   #include <string>
   #include <string.h>
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
   unordered_map<string,vector<NODE>> q1;
   unordered_map<int,vector<int>> date_site;
   int siteNum[1000]={0},siteScore[1000]={0};
   int y;int vis[1000]={0};
   int main() {
       scanf("%d %d",&n,&m);
       int x;string s;
       for(int i=0;i<n;i++){
           cin>>s>>x;
           node[i]=NODE(s,x);
           siteNum[node[i].site]++;
           siteScore[node[i].site]+=node[i].score;
           q1[node[i].level].push_back(node[i]);
           date_site[node[i].date].push_back(node[i].site);
       }
       sort(q1["A"].begin(),q1["A"].end(),[](const NODE &a,const NODE &b){
           if(a.score!=b.score)return a.score>b.score;
           return a.id<b.id;
       });
       sort(q1["B"].begin(),q1["B"].end(),[](const NODE &a,const NODE &b){
           if(a.score!=b.score)return a.score>b.score;
           return a.id<b.id;
       });
       sort(q1["T"].begin(),q1["T"].end(),[](const NODE &a,const NODE &b){
           if(a.score!=b.score)return a.score>b.score;
           return a.id<b.id;
       });
       
       for(int i=1;i<=m;i++){
           cin>>x;
           if(x==1){
               cin>>s;
               printf("Case %d: %d ",i,x);
               cout<<s<<endl;
               for(int i=0;i<q1[s].size();i++){
                   cout<<q1[s][i].id<<" "<<q1[s][i].score<<endl;
               }
               if(q1[s].size()==0)cout<<"NA"<<endl;
           }else if(x==2){
               cin>>y;
               printf("Case %d: %d %03d\n",i,x,y);
               if(siteNum[y]==0){
                   cout<<"NA"<<endl;
                   continue;
               }
               printf("%d %d\n",siteNum[y],siteScore[y]);
           }else if(x==3){
               cin>>y;
               printf("Case %d: %d %06d\n",i,x,y);
               vector<int> ans;
               if(date_site.find(y)==date_site.end()){
                   cout<<"NA"<<endl;
                   continue;
               }
               memset(vis,0,sizeof(vis));
               for(int j=0;j<date_site[y].size();j++){
                   if(vis[date_site[y][j]]){
                   }else{
                       ans.push_back(date_site[y][j]);
                   }
                   vis[date_site[y][j]]++;
               }
               sort(ans.begin(),ans.end(),[](const int &a,const int &b){
                   if(vis[a]!=vis[b])
                       return vis[a]>vis[b];
                   return a<b;
               });
               for(int i=0;i<ans.size();i++){
                   printf("%03d ",ans[i]);
                   cout<<vis[ans[i]]<<endl;
               }
           }
       }
       return 0;
   }
   
   ```

2. ==AC==

   | Submit Time        | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
   | ------------------ | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
   | 9/6/2019, 19:13:02 | Accepted | 25    | [1153](https://pintia.cn/problem-sets/994805342720868352/problems/1071785190929788928) | C++ (g++) | 197 ms   | cc   |

   | Case | Result   | Run Time | Memory  |
   | ---- | -------- | -------- | ------- |
   | 0    | Accepted | 4 ms     | 1124 KB |
   | 1    | Accepted | 5 ms     | 1192 KB |
   | 2    | Accepted | 45 ms    | 2524 KB |
   | 3    | Accepted | 92 ms    | 2772 KB |
   | 4    | Accepted | 197 ms   | 3416 KB |

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
   unordered_map<string,vector<NODE>> q1;
   
   int siteNum[1000]={0},siteScore[1000]={0};
   int y;
   int main() {
       scanf("%d %d",&n,&m);
       int x;string s;
       for(int i=0;i<n;i++){
           cin>>s>>x;
           node[i]=NODE(s,x);
           siteNum[node[i].site]++;
           siteScore[node[i].site]+=node[i].score;
           q1[node[i].level].push_back(node[i]);
       }
       sort(q1["A"].begin(),q1["A"].end(),[](const NODE &a,const NODE &b){
           if(a.score!=b.score)return a.score>b.score;
           return a.id<b.id;
       });
       sort(q1["B"].begin(),q1["B"].end(),[](const NODE &a,const NODE &b){
           if(a.score!=b.score)return a.score>b.score;
           return a.id<b.id;
       });
       sort(q1["T"].begin(),q1["T"].end(),[](const NODE &a,const NODE &b){
           if(a.score!=b.score)return a.score>b.score;
           return a.id<b.id;
       });
       
       for(int i=1;i<=m;i++){
           cin>>x;
           if(x==1){
               cin>>s;
               printf("Case %d: %d ",i,x);
               cout<<s<<endl;
               for(int i=0;i<q1[s].size();i++){
                   cout<<q1[s][i].id<<" "<<q1[s][i].score<<endl;
               }
               if(q1[s].size()==0)cout<<"NA"<<endl;
           }else if(x==2){
               cin>>y;
               printf("Case %d: %d %03d\n",i,x,y);
               if(siteNum[y]==0){
                   cout<<"NA"<<endl;
                   continue;
               }
               printf("%d %d\n",siteNum[y],siteScore[y]);
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

   