# **1074** Reversing Linked List 

| Submit Time         | Status   | Score | Problem                                                      | Compiler  | Run Time | User |
| ------------------- | -------- | ----- | ------------------------------------------------------------ | --------- | -------- | ---- |
| 8/10/2019, 15:28:37 | Accepted | 25    | [1074](https://pintia.cn/problem-sets/994805342720868352/problems/994805394512134144) | C++ (g++) | 74 ms    | cc   |

| Case | Result   | Run Time | Memory  |
| ---- | -------- | -------- | ------- |
| 0    | Accepted | 10 ms    | 2344 KB |
| 1    | Accepted | 7 ms     | 2344 KB |
| 2    | Accepted | 9 ms     | 2304 KB |
| 3    | Accepted | 8 ms     | 2344 KB |
| 4    | Accepted | 6 ms     | 2304 KB |
| 5    | Accepted | 74 ms    | 4096 KB |
| 6    | Accepted | 7 ms     | 2176 KB |

```c++
#include<iostream>
#include<algorithm>
using namespace std;
const int maxnum=100005;
    int head=0,n=0,k=0;    int m=0;
struct NODE{
    int adr=-1;
    int next=-1;
    int val=0;
    int ifuesd=0;
    int pos=-1;
}node[maxnum];
int main(){

    scanf("%d %d %d",&head,&n,&k);
    int ad=0;
    for(int i=0;i<n;i++){
        scanf("%d",&ad);
        scanf("%d %d",&node[ad].val,&node[ad].next);
        node[ad].adr=ad;
    }

    while(head!=-1){
        if(node[head].adr==-1)break;
        node[head].pos=m;
        m++;
        node[head].ifuesd=1;
        //cout<<node[head].adr<<endl;
        head=node[head].next;
    }
    sort(node,node+maxnum,[](NODE &a,NODE &b){
        if(a.ifuesd*b.ifuesd==0)return a.ifuesd>b.ifuesd;
        if(m%k!=0&&a.pos/k==(m-1)/k&&a.pos/k==b.pos/k){
            return a.pos<b.pos;
        }
        if(a.pos/k==b.pos/k){
            return a.pos%k>b.pos%k;
        }
        return a.pos/k<b.pos/k;
    });
    if(m==0){printf("0 -1\n");return 0;}
    for(int i=0;i<m-1;i++){
        printf("%05d %d %05d\n",node[i].adr,node[i].val,node[i+1].adr);
    }
    printf("%05d %d -1\n",node[m-1].adr,node[m-1].val);
    return 0;
}
```

