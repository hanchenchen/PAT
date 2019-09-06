# KNACK

1. `1000ms`大概能进行`200000000`即2*10^8^次计算

2. `256M`一般可是申请`10000000`即1e7个int

3. 大量输入输出使用`printf\scanf`能快很多

4. `Array`一般快于`vector`

5. 圆周率=acos(-1.0)
   自然对数=exp(1.0)

6. `a>>n` `a<<n`会快一些

7. 浮点数的比较

   ```c++
   #define eps 1e-6
   fabs(a-b)<eps
   ```

8. 字符串<->整形

   ```
   sscanf(s,"%d",&n);
   sprintf(s,"%d",n);
   ```

9. `String` `Map`的参数传递较慢，尽可能在函数传参中加入引用

10. `fill()` 、`memset()`

   <algorithm>

      1. `fill(memory[0],memory[0]+1000*1000,0);`
         - `memory[1000][1000]`首地址为`memory[0]`
      2. `memset(memory,0,sizeof(memory));`
         - 按字节赋值，只用于0、-1
         - sizeof(int)==4

11. `struct <`

   `const &a` 快

   ```
   bool operator <(const NODE &b) const{
   
   }
   ```

12. `#include<climits>`

   `INT_MAX` INT_MIN ` `LLONG_MAX` （以9开头的19位数字）

13. `unordered_map``unordered_set` 快`#include <unordered_map>`

14. `gcd`

   ```c++
   int gcd(int a,int b){
     return b==0?a:gcd(b,a%b);
   }
   ```

15. `#define lowbit(i) ((i)&(-i))`

   ```
   
   ```

   ```
   
   ```

16. `upper_bound` `lower_bound`

   ```c++
   int *x=lower_bound(arr,arr+n,val);//第一个大于等于
   int index=upper_bound(arr,arr+n,val)-arr;//第一个大于
   ```

17. `atoi` `stoi` 🧷区别🧷

   `string s`

   ##### `atoi`  

   1. `atoi()`不会做范围检查，如果超出范围的话，超出上界，则输出上界，超出下界，则输出下界；
   2. `atoi(s.c_str())` `s.c_str():#include<string>`
   3. `#include<cstdlib>`

   ##### `stoi`

   1.  stoi()会做范围检查，默认范围是在int的范围内的，如果超出范围的话则会runtime error！
   2.  `stoi(s)`
   3.  `#include<string>`

18. `next_permutation(a,a+3);`

19. ` is_permutation(v1.begin(), v1.end(), v2.begin());` 

   `is_sorted(begin(a), end(a));`// if non-decreased

20. `cout << *s.rbegin();`//`set<> s`

22. ```c++
   // sscanf() 从⼀一个字符串串中读进与指定格式相符的数据
   // sprintf() 字符串串格式化命令，主要功能是把格式化的数据写⼊入某个字符串串中 // 在头⽂文件 #include <string.h>，使⽤用⽅方法:
   char a[50], b[50];
   double temp;
   sscanf(a, "%lf", &temp);
   sprintf(b, "%.2lf",temp);
   ```

22. ```c++
   if(s.find('a', 5) != string::npos)
       int  index = s.find('a', 5);
   ```

23. ```c++
   const double eps = 1e-8;
   ```

24. 1

#### Reference

[ACM的小技巧](https://blog.csdn.net/power721/article/details/4503056)

<u>experience_by_liuchuo_v2.5.pdf</u>