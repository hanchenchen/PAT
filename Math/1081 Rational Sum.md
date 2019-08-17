# 1081 Rational Sum

```c++
#include<iostream>
#include<algorithm>
#include<math.h>
using namespace std;
struct rational{
    long long numerator=0;
    long long denominator=1;
}r,sum;
long long gcd(long long a,long long b){
    return b==0?a:gcd(b,a%b);
}
rational func(rational a,rational b){
    rational re;int sign=1;
    long long up=a.numerator*b.denominator+b.numerator*a.denominator;
    long long down=b.denominator*a.denominator;
    if(up<0){sign=-1;up=-up;}
    int d=gcd(up,down);
    re.numerator=up/d*sign;
    re.denominator=down/d;
    return re;
}
int main(){
    int n;
    cin>>n;
    for(int i=0;i<n;i++){
        scanf("%lld/%lld",&r.numerator,&r.denominator);
        sum=func(sum,r);
    }
    long long integer=sum.numerator/sum.denominator;
    sum.numerator=abs(sum.numerator%sum.denominator);
    if(integer!=0&&sum.numerator!=0)
        printf("%lld %lld/%lld",integer,sum.numerator,sum.denominator);
    else if(integer==0&&sum.numerator!=0)
        printf("%lld/%lld",sum.numerator,sum.denominator);
    else if(integer==0&&sum.numerator==0)
        printf("0");
    else if(sum.numerator==0)
        printf("%lld",integer);
    return 0;
}

```

