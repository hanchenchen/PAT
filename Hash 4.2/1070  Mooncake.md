# 1070  **Mooncake**

1. 不一定能达到`maximum total demand of the marke`

```c++
#include<iostream>
#include<map>
#include<vector>
#include<string.h>
#include<set>
#include<algorithm>
using namespace std;

const int maxN=1005;
const int maxD=505;
//const int maxInt=2147483647;
struct STU{
    double price=0.0,amount=0.0;
}stu[maxN];
int n;
double d;
int main(){
    cin>>n>>d;
    for(int i=0;i<n;i++){
        scanf("%lf",&stu[i].amount);
    }
    for(int i=0;i<n;i++){
        scanf("%lf",&stu[i].price);
    }
    sort(stu,stu+n,[](STU a,STU b){return a.price/a.amount>b.price/b.amount;});
    double totalAmount=0.0,totalPrice=0.0;
    for(int i=0;i<n;i++){
        if(totalAmount+stu[i].amount<=d){
            totalAmount+=stu[i].amount;
            totalPrice+=stu[i].price;
        }else{
            totalPrice+=stu[i].price/stu[i].amount*(d-totalAmount);
            printf("%.2f",totalPrice);
            return 0;
        }
    }
    printf("%.2f",totalPrice);//测试点3
    return 0;
}
```

