# 1133 **Splitting A Linked List**

`sort`函数有矛盾会报错，`return true` 会导致 `a>b` `b>c` `c>a`

```c++
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
using namespace std;
const int maxN=1e5+5;
int first,n,k;
struct NODE{
    int adr,next,val,order=0;
    bool ifin=false;
    NODE(){
        this->adr=this->next=-1;
    }
    NODE(int x,int y,int z){
        this->adr=x;
        this->val=y;
        this->next=z;
    }
}node[maxN];
int main() {
    scanf("%d %d %d",&first,&n,&k);
    int x,y,z;
    for(int i=0;i<n;i++){
        scanf("%d %d %d",&x,&y,&z);
        node[x]=NODE(x,y,z);
    }
    x=first;int num=0;
    while(x!=-1){
        node[x].ifin=true;
        num++;
        node[x].order=num;
        x=node[x].next;
    }
    sort(node,node+maxN,[](NODE a,NODE b){
        if(a.ifin!=b.ifin)return a.ifin;
        if(a.val<0){
            if(b.val<0)return a.order<b.order;
            else return true;
        }else if(a.val>=0&&a.val<=k){
            if(b.val<0)return false;
            else if(b.val>=0&&b.val<=k)return a.order<b.order;
            else return true;
        }else {
            if(b.val<0)return false;
            else if(b.val>=0&&b.val<=k)return false;
            else return a.order<b.order;
        }
    });
    for(int i=0;i<num-1;i++){
        printf("%05d %d %05d\n",node[i].adr,node[i].val,node[i+1].adr);
    }
    printf("%05d %d -1\n",node[num-1].adr,node[num-1].val);
}
```

