# 1022 Digital Library

1. `getline`会读入`回车`,要用`getchar()`把多余的`回车`吸收掉

2. 输入的ID并不是顺序的（测试点1、4）

3. `%07d`

4. `String` `Map`的参数传递较慢，尽可能在函数传参中加入引用

5. 代码略长

   | Submit Time         | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
   | ------------------- | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
   | 8/29/2019, 13:45:37 | Accepted | 30    | [1022](https://pintia.cn/problem-sets/994805342720868352/problems/994805480801550336) | C++ (g++) | 136 ms   | cc   |

   | Case | Result   | Run Time | Memory  |
   | ---- | -------- | -------- | ------- |
   | 0    | Accepted | 4 ms     | 424 KB  |
   | 1    | Accepted | 4 ms     | 424 KB  |
   | 2    | Accepted | 4 ms     | 384 KB  |
   | 3    | Accepted | 4 ms     | 356 KB  |
   | 4    | Accepted | 136 ms   | 7680 KB |

   ```c++
   #include<iostream>
   #include<map>
   #include<set>
   using namespace std;
   map<string,set<int> > title;
   map<string,set<int> > author;
   map<string,set<int> > keyWords;
   map<string,set<int> > publisher;
   map<string,set<int> > year;
   int main(){
       int n,id;cin>>n;getchar();
       string s;
       map<string,set<int> >::iterator iter;
       for(int i=0;i<n;i++){
           cin>>id;getchar();
           getline(cin,s);
           title[s].insert(id);
           
           getline(cin,s);
           author[s].insert(id);
           
           while(cin>>s){
               char c=getchar();
               keyWords[s].insert(id);
               if(c=='\n')break;
           }
           
           getline(cin,s);
           publisher[s].insert(id);
           
           getline(cin,s);
           year[s].insert(id);
       }
       
       int m,num;cin>>m;
       set<int>::iterator j;
       for(int i=0;i<m;i++){
           scanf("%d: ",&num);//cout<<num<<endl;
           switch(num){
               case 1:
                   getline(cin,s);
                   cout<<num<<": "<<s<<endl;
                   iter=title.find(s);
                   if(iter==title.end()){
                       cout<<"Not Found"<<endl;
                       break;
                   }
                   j=iter->second.begin();
                   while(j!=iter->second.end())printf("%07d\n",*j++);
                   break;
               case 2:
                   getline(cin,s);
                   cout<<num<<": "<<s<<endl;
                   iter=author.find(s);
                   if(iter==author.end()){
                       cout<<"Not Found"<<endl;
                       break;
                   }
                   j=iter->second.begin();
                   while(j!=iter->second.end())printf("%07d\n",*j++);
                   break;
               case 3:
                   getline(cin,s);
                   cout<<num<<": "<<s<<endl;
                   iter=keyWords.find(s);
                   if(iter==keyWords.end()){
                       cout<<"Not Found"<<endl;
                       break;
                   }
                   j=iter->second.begin();
                   while(j!=iter->second.end())printf("%07d\n",*j++);
                   break;
               case 4:
                   getline(cin,s);
                   cout<<num<<": "<<s<<endl;
                   iter=publisher.find(s);
                   if(iter==publisher.end()){
                       cout<<"Not Found"<<endl;
                       break;
                   }
                   j=iter->second.begin();
                   while(j!=iter->second.end())printf("%07d\n",*j++);
                   break;
               case 5:
                   getline(cin,s);
                   cout<<num<<": "<<s<<endl;
                   iter=year.find(s);
                   if(iter==year.end()){
                       cout<<"Not Found"<<endl;
                       break;
                   }
                   j=iter->second.begin();
                   while(j!=iter->second.end())printf("%07d\n",*j++);
                   break;
               default:
                   cout<<"Not Found"<<endl;;
           }
       }
       return 0;
   }
   ```

6. 加了`Queue`函数

   | Submit Time         | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
   | ------------------- | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
   | 8/29/2019, 13:45:01 | Accepted | 30    | [1022](https://pintia.cn/problem-sets/994805342720868352/problems/994805480801550336) | C++ (g++) | 147 ms   | cc   |

   | Case | Result   | Run Time | Memory  |
   | ---- | -------- | -------- | ------- |
   | 0    | Accepted | 4 ms     | 384 KB  |
   | 1    | Accepted | 4 ms     | 352 KB  |
   | 2    | Accepted | 4 ms     | 368 KB  |
   | 3    | Accepted | 4 ms     | 352 KB  |
   | 4    | Accepted | 147 ms   | 7552 KB |

   ```c++
   #include<iostream>
   #include<map>
   #include<set>
   using namespace std;
   map<string,set<int> > title;
   map<string,set<int> > author;
   map<string,set<int> > keyWords;
   map<string,set<int> > publisher;
   map<string,set<int> > year;
   map<string,set<int> >::iterator iter;
   set<int>::iterator j;
   void query(map<string,set<int> > &m,string s){
       iter=m.find(s);
       if(iter==m.end()){
           cout<<"Not Found"<<endl;
           return;
       }
       j=iter->second.begin();
       while(j!=iter->second.end())printf("%07d\n",*j++);
   }
   int main(){
       int n,id;cin>>n;getchar();
       string s;
       
       for(int i=0;i<n;i++){
           cin>>id;getchar();
           getline(cin,s);
           title[s].insert(id);
           
           getline(cin,s);
           author[s].insert(id);
           
           while(cin>>s){
               char c=getchar();
               keyWords[s].insert(id);
               if(c=='\n')break;
           }
           
           getline(cin,s);
           publisher[s].insert(id);
           
           getline(cin,s);
           year[s].insert(id);
       }
       
       int m,num;cin>>m;
       
       for(int i=0;i<m;i++){
           scanf("%d: ",&num);//cout<<num<<endl;
           getline(cin,s);
           cout<<num<<": "<<s<<endl;
           switch(num){
               case 1:
                   query(title, s);
                   break;
               case 2:
                   query(author, s);
                   break;
               case 3:
                   query(keyWords, s);
                   break;
               case 4:
                   query(publisher, s);
                   break;
               case 5:
                   query(year, s);
                   break;
               default:
                   cout<<"Not Found"<<endl;;
           }
       }
       return 0;
   }
   ```

   