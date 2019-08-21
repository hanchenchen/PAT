# 1071 Speech Patterns

1. `"a"` 

2. | Submit Time         | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
   | ------------------- | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
   | 8/21/2019, 13:14:05 | Accepted | 25    | [1071](https://pintia.cn/problem-sets/994805342720868352/problems/994805398257647616) | C++ (g++) | 158 ms   | cc   |

   | Case | Result   | Run Time | Memory  |
   | ---- | -------- | -------- | ------- |
   | 0    | Accepted | 3 ms     | 424 KB  |
   | 1    | Accepted | 3 ms     | 512 KB  |
   | 2    | Accepted | 158 ms   | 2400 KB |
   | 3    | Accepted | 101 ms   | 2328 KB |
   | 4    | Accepted | 3 ms     | 424 KB  |

3. ```c++
   #include<iostream>
   #include<algorithm>
   #include<map>
   #include<string.h>
   using namespace std;
   map<string,int> m;
   bool if_alphanumerical(char &c){
       if(c<='9'&&c>='0')return true;
       if(c<='z'&&c>='a')return true;
       if(c<='Z'&&c>='A'){c=c-'A'+'a';return true;}
       return false;
   }
   int main(){
       string s;
       getline(cin,s);
       string word="";
       map<string,int>::iterator iter;
       for(int i=0;i<s.size();i++){
           if(if_alphanumerical(s[i])){
               word+=s[i];
           }else if(word!=" "&&word!=""){
               iter=m.find(word);
               if(iter!=m.end()){
                   m[word]++;
               }else{
                   m.insert(pair<string,int>(word,1));
               }
               word="";
           }
       }
       if(word!=" "&&word!=""){
           iter=m.find(word);
           if(iter!=m.end()){
               m[word]++;
           }else{
               m.insert(pair<string,int>(word,1));
           }
       }
       int num=0;string ans;
       for(iter=m.begin();iter!=m.end();iter++){
           //cout<<iter->first<<" "<<iter->second<<endl;
           if(num<iter->second){
               num=iter->second;
               ans=iter->first;
           }
       }
       cout<<ans<<" "<<num<<endl;
       return 0;
   }
   ```

4. 

5. 1