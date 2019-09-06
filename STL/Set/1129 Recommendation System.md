# **1129** **Recommendation System**

1. `Vector`+`Sort`

   TLE*3

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<vector>
   #include<map>
   #include<queue>
   #include<math.h>
   using namespace std;
   struct NODE{
       int id=0,frequent=0;
   };
   const int maxN=50000+5;
   int n,k,x;
   vector<NODE> v,temp;
   int main(){
       scanf("%d %d",&n,&k);
       NODE node;
       v.push_back(node);
       for(int i=1;i<=n;i++){
           node.id++;
           v.push_back(node);
       }
       for(int i=0;i<n;i++){
           temp=v;
           sort(temp.begin(),temp.end(),[](NODE a,NODE b){
               if(a.frequent!=b.frequent)return a.frequent>b.frequent;
               return a.id<b.id;
           });
           scanf("%d",&x);
           if(i!=0)printf("%d:",x);
           for(int i=0;i<temp.size()&&i<k;i++){
               if(temp[i].frequent==0)break;
               printf(" %d",temp[i].id);
           }
           if(i!=0)cout<<endl;
           v[x].frequent++;
       }
       return 0;
   }
   ```

2. `Set`+`struct`==AC==

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<vector>
   #include<map>
   #include<set>
   #include<math.h>
   using namespace std;
   struct NODE{
       int id=0,frequent=0;
       NODE(int x,int y){
           this->id=x;
           this->frequent=y;
       }
       bool operator<(const NODE b) const{
           if(this->frequent!=b.frequent)return this->frequent>b.frequent;
           return this->id<b.id;
       }
   };
   const int maxN=50000+5;
   int n,k,x,book[maxN]={0};
   set<NODE> v;
   int main(){
       scanf("%d %d",&n,&k);
       for(int i=0;i<n;i++){
           scanf("%d",&x);
           if(i!=0)printf("%d:",x);
           set<NODE>::iterator iter=v.begin();
           for(int i=0;i<k&&iter!=v.end();i++){
               printf(" %d",iter++->id);
           }
           if(i!=0)cout<<endl;
           iter=v.find(NODE(x,book[x]));
           if(iter!=v.end())v.erase(iter);
           book[x]++;
           v.insert(NODE(x,book[x]));
       }
       return 0;
   }
   ```

   

