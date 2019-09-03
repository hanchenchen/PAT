# 1010 Radix

1. ##### `Overflow`

   如果进制取得过大，会导致进制转换函数结果溢出为负，此时返回一个很大的值，使向左区间查找

2. `long long`

3. ```c++
   #include<iostream>
   #include<vector>
   #include<algorithm>
   using namespace std;
   long long n1=0,tag,radix;
   string s1,s2;
   int tonum(char c){
       if(c>='0'&&c<='9'){
           return c-'0';
       }
       return c-'a'+10;
   }
   long long shift(string s,long long r){
       long long x=0,mid;
       for(int i=0;i<s.size();i++){
           x*=r;
           mid=tonum(s[i]);
           if(mid>=r)return -1;
           if(x<0)return -2;
           x+=mid;
       }
       return x;
   }
   int main(){
       cin>>s1>>s2>>tag>>radix;
       if(tag==2){
           swap(s1,s2);
       }
       n1=shift(s1,radix);
       long long left=2,right=2147483647;
       while(left<right){
           long long mid=(left+right)/2;
           if(shift(s2,mid)==-2){
               right=mid;
           }else if(shift(s2,mid)<n1){
               left=mid+1;
           }else{
               right=mid;
           }
       }
       if(shift(s2,left)==n1&&n1!=-1){
           cout<<left<<endl;
           return 0;
       }
       cout<<"Impossible"<<endl;
       return 0;
   }
   ```

4. 

5. 1