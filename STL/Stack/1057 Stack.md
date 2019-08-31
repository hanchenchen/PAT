# 1057 Stack

1. 分块

   ```c++
   					int len=(int)st.size();
               if(len%2==1)len++;
               len/=2;
               int num=0;int j=0;
               while(num+arr_100[j]<len){
                   num+=arr_100[j];
                   j++;
               }
               j=j*100;
               while(num+arr[j]<len){
                   num+=arr[j++];
               }
               cout<<j<<endl;
   ```

2. ac

   ```c++
   #include<iostream>
   #include<vector>
   #include<stack>
   #include<algorithm>
   using namespace std;
   const int maxN=100100;
   int arr_100[maxN/100]={0};
   int arr[maxN]={0};
   stack<int> st;
   int main(){
       int n,x;
       cin>>n;
       string s;
       for(int i=0;i<n;i++){
           cin>>s;
           if(s=="Pop"){
               if(st.empty()){
                   cout<<"Invalid"<<endl;
               }else{
                   cout<<st.top()<<endl;
                   arr_100[st.top()/100]--;
                   arr[st.top()]--;
                   st.pop();
               }
           }else if(s=="PeekMedian"){
               if(st.empty()){
                   cout<<"Invalid"<<endl;
                   continue;
               }
               int len=(int)st.size();
               if(len%2==1)len++;
               len/=2;
               int num=0;int j=0;
               while(num+arr_100[j]<len){
                   num+=arr_100[j];
                   j++;
               }
               j=j*100;
               while(num+arr[j]<len){
                   num+=arr[j++];
               }
               cout<<j<<endl;
           }else{
               cin>>x;
               st.push(x);
               arr_100[st.top()/100]++;
               arr[st.top()]++;
           }
       }
       return 0;
   }
   ```

3. `lowbit`

   ```c++
   #include<iostream>
   #include<vector>
   #include<stack>
   #include<algorithm>
   #define lowbit(m) ((m)&-(m))
   using namespace std;
   const int maxN=100100;
   int arr[maxN]={0};
   stack<int> st;
   void update(int index,int x){
       for(int i=index;i<maxN;i+=lowbit(i)){
           arr[i]+=x;
       }
   }
   int sum(int index){
       int re=0;
       for(int j=index;j>0;j-=lowbit(j)){
           re+=arr[j];
       }
       return re;
   }
   int main(){
       int n,x;
       cin>>n;
       string s;
       for(int i=0;i<n;i++){
           cin>>s;
           if(s=="Pop"){
               if(st.empty()){
                   cout<<"Invalid"<<endl;
               }else{
                   cout<<st.top()<<endl;
                   update(st.top(), -1);
                   st.pop();
               }
           }else if(s=="PeekMedian"){
               if(st.empty()){
                   cout<<"Invalid"<<endl;
                   continue;
               }
               int len=(int)st.size();
               if(len%2==1)len++;
               len/=2;
               int i=1,j=maxN;
               while(i<j){
                   int mid=(i+j)/2;
                   int t=sum(mid);
                   if(t<len){
                       i=mid+1;
                   }else if(t>=len){
                       j=mid;
                   }
               }
               cout<<i<<endl;
           }else{
               cin>>x;
               st.push(x);
               update(st.top(), 1);
           }
       }
       return 0;
   }
   ```

   