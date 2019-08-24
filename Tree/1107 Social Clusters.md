# 1107 Social Clusters

1. 并查集

2. AC

3. ```c++
   #include<iostream>
   #include<set>
   #include<algorithm>
   using namespace std;
   
   int hobby[1001]={0};
   int stu[1001]={0};
   int getroot(int x){
       //cout<<x;
       int y=x;
       while(hobby[x]!=x)x=hobby[x];
       hobby[y]=x;
       return x;
   }
   int main(){
       int n,k,mini,input;
       set<int>::iterator iter;
       scanf("%d",&n);
       for(int i=1;i<=1001;i++)hobby[i]=i;
       
       for(int i=1;i<=n;i++){
           scanf("%d:",&k);
           set<int> s;
           for(int j=0;j<k;j++){
               scanf("%d:",&input);
               s.insert(getroot(input));
           }
           iter=s.begin();
           mini=*iter;
           stu[i]=mini;
           while(iter!=s.end()){
               hobby[*iter]=mini;
               iter++;
           }
           /*for(int i=1;i<=10;i++){
               cout<<hobby[i]<<" ";
           }cout<<endl;*/
       }
       int ans[1001]={0};
       for(int i=1;i<=n;i++){
           ans[getroot(stu[i])]++;
       }
       sort(ans,ans+1001,[](int a,int b){return a>b;});
       int count=0;
       for(int i=0;i<=1000;i++){
           if(ans[i])count++;
           else break;
       }
       cout<<count<<endl<<ans[0];
       for(int i=1;i<=1000;i++){
           if(ans[i])printf(" %d",ans[i]);
           else break;
       }
   }
   
   ```

4. 