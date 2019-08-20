# 1060 Are They Equal

1. 易错：

   `0.0000*10^0`

2. AC

   | Submit Time         | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
   | ------------------- | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
   | 8/20/2019, 16:11:34 | Accepted | 25    | [1060](https://pintia.cn/problem-sets/994805342720868352/problems/994805413520719872) | C++ (g++) | 3 ms     | cc   |

   | Case | Result   | Run Time | Memory |
   | ---- | -------- | -------- | ------ |
   | 0    | Accepted | 3 ms     | 300 KB |
   | 1    | Accepted | 2 ms     | 296 KB |
   | 2    | Accepted | 2 ms     | 356 KB |
   | 3    | Accepted | 2 ms     | 384 KB |
   | 4    | Accepted | 2 ms     | 384 KB |
   | 5    | Accepted | 3 ms     | 288 KB |
   | 6    | Accepted | 2 ms     | 384 KB |

3. ```c++
   #include<iostream>
   #include<algorithm>
   #include<set>
   #include<string.h>
   using namespace std;
   int main(){
       int n;
       string a,b;
       scanf("%d",&n);
       cin>>a>>b;
       int point=-1,digit=-1;
       for(int i=0;i<a.size();i++){
           if(a[i]=='.')point=i;
           else if(a[i]!='0'&&digit==-1)digit=i;
       }
       string ad="";int ap=0;
       if(digit!=-1){
           if(point!=-1){
               int x=point-digit;
               if(point>digit){
                   ap=x;
               }else{
                   ap=x+1;
               }
           }else{
               ap=(int)a.size()-digit;
           }
           for(int i=0;i<n;i++){
               if(a[digit+i]=='.')digit++;
               if(digit+i<a.size())ad+=(a[digit+i]);
               else ad+="0";
           }
       }else
           for(int i=0;i<n;i++){ad+="0";}
       point=-1;digit=-1;
       for(int i=0;i<b.size();i++){
           if(b[i]=='.')point=i;
           else if(b[i]!='0'&&digit==-1)digit=i;
       }
       string bd="";int bp=0;
       if(digit!=-1){
           if(point!=-1){
               int x=point-digit;
               if(point>digit){
                   bp=x;
               }else{
                   bp=x+1;
               }
           }else{
               bp=(int)b.size()-digit;
           }
           for(int i=0;i<n;i++){
               if(b[digit+i]=='.')digit++;
               if(digit+i<b.size())bd+=(b[digit+i]);
               else bd+="0";
           }
       }else
           for(int i=0;i<n;i++){bd+="0";}
       if(ad==bd&&ap==bp){
           printf("YES 0.");
           cout<<ad;
           printf("*10^%d",ap);
       }else {
           printf("NO 0.");
           cout<<ad;
           printf("*10^%d",ap);
           printf(" 0.");
           cout<<bd;
           printf("*10^%d",bp);
       }
       return 0;
   }
   ```

4. 

5. 1