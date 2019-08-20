# 1100 Mars Numbers

1. 打表

2. 特殊测试用例 `13` `tam`，而非`tam tret`

3. | Submit Time         | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
   | ------------------- | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
   | 8/20/2019, 19:19:12 | Accepted | 20    | [1100](https://pintia.cn/problem-sets/994805342720868352/problems/994805367156883456) | C++ (g++) | 4 ms     | cc   |

   | Case | Result   | Run Time | Memory |
   | ---- | -------- | -------- | ------ |
   | 0    | Accepted | 3 ms     | 384 KB |
   | 1    | Accepted | 3 ms     | 416 KB |
   | 2    | Accepted | 4 ms     | 384 KB |
   | 3    | Accepted | 4 ms     | 416 KB |
   | 4    | Accepted | 3 ms     | 384 KB |

4. ```c++
   #include<iostream>
   #include<algorithm>
   #include<map>
   #include<string.h>
   using namespace std;
   string digit[13]={"tret","jan", "feb", "mar", "apr",
       "may", "jun", "jly", "aug", "sep", "oct", "nov", "dec"};
   string higher[13]={"",
       "tam", "hel", "maa", "huh", "tou", "kes", "hei", "elo",
       "syy", "lok", "mer", "jou"
   };
   map<string,int> m;
   string arr[200];
   int main(){
       arr[0]="tret";
       m.insert(pair<string,int>(arr[0],0));
       for(int i=1;i<13;i++){
           arr[i]=digit[i];
           m.insert(pair<string,int>(arr[i],i));
           arr[13*i]=higher[i];
           m.insert(pair<string,int>(arr[13*i],13*i));
       }
       for(int i=1;i<13;i++){
           for(int j=1;j<13;j++){
               arr[i*13+j]=higher[i]+" "+digit[j];
               m.insert(pair<string,int>(arr[i*13+j],i*13+j));
           }
       }
       int n;
       string s;
       scanf("%d\n",&n);// \n! 否则会被输入getline
       for(int i=0;i<n;i++){
           getline(cin,s);
           if(s[0]<='9'&&s[0]>='0'){
               int x=0;
               for(int i=0;s[i]!='\0';i++){
                   x*=10;
                   x+=s[i]-'0';
               }
               cout<<arr[x]<<endl;
           }else {
               cout<<m[s]<<endl;
           }
       }
       return 0;
   }
   ```

5. 