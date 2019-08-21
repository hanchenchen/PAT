# 1103 Integer Factorization

1. `测试点4`?

2. AC

   ```c++
   #include<iostream>
   #include<algorithm>
   #include<math.h>
   #include<string.h>
   using namespace std;
   int n,k,p,anslen=0;
   int arr[500]={0};
   int ans[500]={0};
   int power[500]={0};
   bool cmp(int arr[],int ans[]){
       for(int i=0;i<k;i++){
           if(arr[i]!=ans[i])return arr[i]>ans[i];
       }
       return false;
   }
   void func(int index,int sum,int len){
       if(index>k||sum>n)return;
       if(sum==n&&index==k&&len>=anslen&&cmp(arr,ans)){
           anslen=len;
           for(int i=0;i<k;i++){ans[i]=arr[i];}
           return;
       }
       int m=n;
       if(index!=0)m=power[arr[index-1]];
       m=min(n-sum,m);
       for(int i=1;i<=n&&power[i]<=m;i++){//测试点4 去掉i<=n 就过不了，搞不懂
           arr[index]=i;
           func(index+1,sum+power[i],len+i);
       }
   }
   int main(){
       cin>>n>>k>>p;
       for(int i=1;i<=n;i++){
           power[i]=pow(i,p);
           if(power[i]>n)break;
       }
       func(0,0,0);
       if(!ans[0]){
           cout<<"Impossible";
           return 0;
       }
       cout<<n<<" = ";
       for(int i=0;i<k;i++){
           if(i!=0)cout<<" + ";
           cout<<ans[i]<<"^"<<p;
       }
       return 0;
   }
   ```

3. 1