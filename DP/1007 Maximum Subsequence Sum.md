# **1007** **Maximum Subsequence Sum** 

```c++
#include<stdio.h>
int main(){
    int k;
    scanf("%d",&k);
    int sum=0;
    int right=0,left=0;
    scanf("%d",&sum);
    int first,last;
    first=last=sum;
    right=left=sum;
    int x;
    int y=0;
    int max_sum=sum;
    for(int i=1;i<k;i++){
        scanf("%d",&x);
        last=x;
        if(sum>=0){
            sum+=x;
        }else{
            y=x;
            sum=x;
        }
        if(max_sum<sum){
            max_sum=sum;
            right=x;
            left=y;
        }
    }
    if(max_sum>=0)printf("%d %d %d",max_sum,left,right);
    else printf("0 %d %d",first,last);
    return 0;
}

```

