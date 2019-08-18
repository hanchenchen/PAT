# 1088 Rational Arithmetic

```c++
#include<iostream>
#include<algorithm>
#include<math.h>
using namespace std;
struct rational{
    long long numerator=0;
    long long denominator=1;
}r[2],one,ans[4];
long long gcd(long long a,long long b){
    return b==0?a:gcd(b,a%b);
}
rational func(rational a,rational b){
    rational re;int sign=1;
    long long up=a.numerator*b.denominator+b.numerator*a.denominator;
    long long down=b.denominator*a.denominator;
    if(up<0){sign=-sign;up=-up;}
    if(down<0){sign=-sign;down=-down;}
    long long d=1;
    if(up!=0&&down!=0)d=gcd(up,down);
    else if(up==0&&down!=0)down=1;
    else if(up!=0&&down==0)up=1;
    re.numerator=up/d*sign;
    re.denominator=down/d;
    return re;
}
rational func2(rational a,rational b){
    rational re;int sign=1;
    long long up=a.numerator*b.numerator;
    long long down=b.denominator*a.denominator;
    if(up<0){sign=-sign;up=-up;}
    if(down<0){sign=-sign;down=-down;}
    long long d=1;
    if(up!=0&&down!=0)d=gcd(up,down);
    else if(up==0&&down!=0)down=1;
    else if(up!=0&&down==0)up=1;
    re.numerator=up/d*sign;
    re.denominator=down/d;
    return re;
}
rational func3(rational a,rational b){
    rational re;int sign=1;
    long long up=b.denominator*a.numerator;
    long long down=a.denominator*b.numerator;
    if(up<0){sign=-sign;up=-up;}
    if(down<0){sign=-sign;down=-down;}
    long long d=1;
    if(up!=0&&down!=0)d=gcd(up,down);
    else if(up==0&&down!=0)down=1;
    else if(up!=0&&down==0)up=1;
    re.numerator=up/d*sign;
    re.denominator=down/d;
    return re;
}
void print(rational sum){
    if(sum.denominator==0)
    {printf("Inf");return;}
    int flag=0;
    if(sum.numerator<0)flag=1;
    if(flag)printf("(");
    long long integer=sum.numerator/sum.denominator;
    if(integer!=0)sum.numerator=abs(sum.numerator%sum.denominator);
    if(integer!=0&&sum.numerator!=0)
        printf("%lld %lld/%lld",integer,sum.numerator,sum.denominator);
    else if(integer==0&&sum.numerator!=0)
        printf("%lld/%lld",sum.numerator,sum.denominator);
    else if(integer==0&&sum.numerator==0)
        printf("0");
    else if(sum.numerator==0)
        printf("%lld",integer);
    if(flag)printf(")");
}
int main(){
    for(int i=0;i<2;i++){
        scanf("%lld/%lld",&r[i].numerator,&r[i].denominator);
        r[i]=func(one,r[i]);
    }
    ans[0]=func(r[0],r[1]);
    print(r[0]);printf(" + ");print(r[1]);printf(" = ");print(ans[0]);printf("\n");
    
    r[1].numerator=-r[1].numerator;
    ans[1]=func(r[0],r[1]);
    r[1].numerator=-r[1].numerator;
    print(r[0]);printf(" - ");print(r[1]);printf(" = ");print(ans[1]);printf("\n");
    
    ans[2]=func2(r[0],r[1]);
    print(r[0]);printf(" * ");print(r[1]);printf(" = ");print(ans[2]);printf("\n");
    
    ans[3]=func3(r[0],r[1]);
    print(r[0]);printf(" / ");print(r[1]);printf(" = ");print(ans[3]);printf("\n");
    return 0;
}
```

