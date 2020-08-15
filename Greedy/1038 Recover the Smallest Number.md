# **1038** **Recover the Smallest Number**

1. `sscanf``sprinf`看起来很好用，但总是有莫名其妙的错误🙅

2. `string`

   ==AC==

   ```c++
   #include<iostream>
   #include<queue>
   #include<vector>
   #include<string.h>
   #include<set>
   #include<stdio.h>
   #include<algorithm>
   using namespace std;
   const int maxN=10005;
   //const int maxInt=2147483647;
   int n,x;
   string arr[maxN];
   int main(){
       cin>>n;
       for(int i=0;i<n;i++){
           cin>>arr[i];
       }
       sort(arr,arr+n,[](string a,string b){
           return a+b<b+a;
       });
       string ans;
       for(int i=0;i<n;i++){
           ans+=arr[i];
       }
       while(ans.size()>1&&ans[0]=='0')ans.erase(ans.begin());
       cout<<ans;
       return 0;
   }
   ```

#### Python

```python
def cmp(a, b):
    if a + b < b + a:
        return -1
    elif a + b > b + a:
        return 1
    else:
        return 0


from functools import cmp_to_key

n = input()
arr = n.split()[1:]
n = int(n[0])
if not n:
    exit(0)
# arr.sort()
arr.sort(key=cmp_to_key(cmp), reverse=False)
# arr.sort()
ans = ''
for i in arr:
    ans+=i
for i in range(len(ans)):
    if ans[i]=='0':
        pass
    else:
        ans = ans[i:]
        print(ans)
        exit()
print('0')
```

