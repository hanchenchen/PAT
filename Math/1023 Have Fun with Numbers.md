# 1023 Have Fun with Numbers

```c++
#include<iostream>
#include<math.h>
using namespace std;
int arr[10]={0};
int main(){
    string n;
    cin>>n;
    int c=0,x=0;
    for(int i=n.size()-1;i>=0;i--){
        x=n[i]-'0';
        arr[x]++;
        x*=2;
        x+=c;
        arr[x%10]--;
        n[i]='0'+x%10;
        c=x/10;
    }
    for(int i=0;i<10;i++){
        if(arr[i]!=0){
            printf("No\n");
            if(c)printf("%d",c);
            for(int j=0;j<n.size();j++){
                printf("%d",n[j]-'0');
            }
            return 0;}
    }
    printf("Yes\n");
    if(c)printf("%d",c);
        for(int j=0;j<n.size();j++){
            printf("%d",n[j]-'0');
        }
    return 0;
}
```

