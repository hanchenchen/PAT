# **1052** Linked List Sorting

| Submit Time        | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
| ------------------ | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
| 8/9/2019, 21:18:46 | Accepted | 25    | [1052](https://pintia.cn/problem-sets/994805342720868352/problems/994805425780670464) | C++ (g++) | 101 ms   | cc   |

| Case | Result   | Run Time | Memory  |
| ---- | -------- | -------- | ------- |
| 0    | Accepted | 9 ms     | 1792 KB |
| 1    | Accepted | 9 ms     | 1952 KB |
| 2    | Accepted | 8 ms     | 1920 KB |
| 3    | Accepted | 101 ms   | 3752 KB |
| 4    | Accepted | 8 ms     | 1888 KB |

谁能想到有无效节点？

```c++
#include<iostream>
#include<algorithm>
using namespace std;
const int maxnum=100005;
struct NODE{
    int adr;
    int next=-1;
    int val=0;
    int ifuesd=0;
}node[maxnum];
int main(){
    int head=0,n=0;
    scanf("%d %d",&n,&head);
    int ad=0;
    for(int i=0;i<n;i++){
        scanf("%d",&ad);
        scanf("%d %d",&node[ad].val,&node[ad].next);
        node[ad].adr=ad;
    }
    int m=0;
    while(head!=-1){
        if(node[head].adr)
        m++;
        node[head].ifuesd=1;
        head=node[head].next;
    }
    sort(node,node+maxnum,[](NODE &a,NODE &b){
        if(a.ifuesd*b.ifuesd==0)return a.ifuesd>b.ifuesd;
        return a.val<b.val;
    });
    if(m==0){printf("0 -1\n");return 0;}
    printf("%d %05d\n",m,node[0].adr);
    for(int i=0;i<m-1;i++){
        printf("%05d %d %05d\n",node[i].adr,node[i].val,node[i+1].adr);
    }
    printf("%05d %d -1\n",node[m-1].adr,node[m-1].val);
    return 0;
}

```

