# 1097 **Deduplication on a Linked List**

| Submit Time         | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
| ------------------- | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
| 8/10/2019, 16:07:12 | Accepted | 25    | [1097](https://pintia.cn/problem-sets/994805342720868352/problems/994805369774129152) | C++ (g++) | 133 ms   | cc   |

| Case | Result   | Run Time | Memory  |
| ---- | -------- | -------- | ------- |
| 0    | Accepted | 10 ms    | 2432 KB |
| 1    | Accepted | 9 ms     | 2272 KB |
| 2    | Accepted | 10 ms    | 2344 KB |
| 3    | Accepted | 109 ms   | 4520 KB |
| 4    | Accepted | 133 ms   | 4480 KB |

```c++
#include<iostream>
#include<algorithm>
#include<set>
using namespace std;
const int maxnum=100005;
int head=0,n=0,k=0;    int m=0;
struct NODE{
    int adr=-1;
    int next=-1;
    int val=0;
    int if_duplicated=-1;
    int pos=-1;
}node[maxnum];
set<int> times;
int main(){
    
    scanf("%d %d",&head,&n);
    int ad=0;
    for(int i=0;i<n;i++){
        scanf("%d",&ad);
        scanf("%d %d",&node[ad].val,&node[ad].next);
        node[ad].adr=ad;
    }
    int ans=0;
    set<int>::iterator iter;
    while(head!=-1&&node[head].adr!=-1){
        iter=times.find(abs(node[head].val));
        if(iter==times.end()){
            times.insert(abs(node[head].val));
            node[head].if_duplicated=1;
            ans++;
        }else{
            node[head].if_duplicated=0;
        }
        m++;
        node[head].pos=m;
        //cout<<node[head].adr<<endl;
        head=node[head].next;
    }
    sort(node,node+maxnum,[](NODE &a,NODE &b){
        if(a.if_duplicated!=b.if_duplicated)return a.if_duplicated>b.if_duplicated;
        return a.pos<b.pos;
    });
    if(m==0){printf("0 -1\n");return 0;}
    for(int i=0;i<m-1;i++){
        if(i!=ans-1)printf("%05d %d %05d\n",node[i].adr,node[i].val,node[i+1].adr);
        else printf("%05d %d -1\n",node[i].adr,node[i].val);
    }
    printf("%05d %d -1\n",node[m-1].adr,node[m-1].val);
    return 0;
}
```

