# **1056** Mice and Rice

| Submit Time        | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
| ------------------ | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
| 8/9/2019, 23:18:23 | Accepted | 25    | [1056](https://pintia.cn/problem-sets/994805342720868352/problems/994805419468242944) | C++ (g++) | 4 ms     | cc   |

| Case | Result   | Run Time | Memory |
| ---- | -------- | -------- | ------ |
| 0    | Accepted | 3 ms     | 464 KB |
| 1    | Accepted | 3 ms     | 492 KB |
| 2    | Accepted | 3 ms     | 384 KB |
| 3    | Accepted | 3 ms     | 384 KB |
| 4    | Accepted | 4 ms     | 424 KB |
| 5    | Accepted | 4 ms     | 424 KB |

```c++
#include<iostream>
#include<algorithm>
#include<queue>
using namespace std;
int main(){
    int p,g;
    scanf("%d %d",&p,&g);
    int arr[p]={0};
    int ans[p]={0};
    for(int i=0;i<p;i++){
        cin>>arr[i];
    }
    queue<int> qu;
    int x;
    for(int i=0;i<p;i++){
        cin>>x;
        qu.push(x);
    }
    while(qu.size()>1){
        queue<int> mid;
        x=(int)qu.size()/g+((int)qu.size()%g>0)+1;
        while(!qu.empty()){
            int mice=-1;
            int programmer=-1;
            for(int k=0;k<g&&!qu.empty();k++){
                if(mice<arr[qu.front()]){
                    mice=arr[qu.front()];
                    programmer=qu.front();
                }
                ans[qu.front()]=x;
                qu.pop();                
            }
            mid.push(programmer);
        }
        qu=mid;
    }
    ans[qu.front()]=1;
    printf("%d",ans[0]);
    for(int i=1;i<p;i++){
        printf(" %d",ans[i]);
    }
    return 0;
}

```

