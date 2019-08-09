# 1032 Sharing

| Submit Time        | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
| ------------------ | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
| 8/9/2019, 20:20:34 | Accepted | 25    | [1032](https://pintia.cn/problem-sets/994805342720868352/problems/994805460652113920) | C++ (g++) | 24 ms    | cc   |

| Case | Result   | Run Time | Memory  |
| ---- | -------- | -------- | ------- |
| 0    | Accepted | 2 ms     | 356 KB  |
| 1    | Accepted | 2 ms     | 512 KB  |
| 2    | Accepted | 2 ms     | 484 KB  |
| 3    | Accepted | 3 ms     | 512 KB  |
| 4    | Accepted | 2 ms     | 416 KB  |
| 5    | Accepted | 24 ms    | 1056 KB |

```c++
#include<iostream>
using namespace std;
int arr[99999]={0};
int if1[99999]={0};
int main(){
    int l1=0,l2=0,n=0;
    scanf("%d %d %d",&l1,&l2,&n);
    int left=0;
    char c;
    for(int i=0;i<n;i++){
        scanf("%d %c",&left,&c);
        scanf("%d",&arr[left]);
    }
    left=l1;
    while(left!=-1){
        if1[left]=1;
        left=arr[left];
    }
    left=l2;
    while(left!=-1){
        if(if1[left]==1){
            printf("%05d",left);//cout<<left<<endl;
            return 0;
        }
        left=arr[left];
    }
    cout<<"-1"<<endl;
    return 0;
}
```

