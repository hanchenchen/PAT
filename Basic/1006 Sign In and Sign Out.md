# 1006 **Sign In and Sign Out**

```c++
#include<stdio.h>
#include "string.h"
#include<iostream>
using namespace std;
int main(){
    int m;
    scanf("%d",&m);
    char first_person[20];
    char first_time[10];
    char last_person[20];
    char last_time[10];
    scanf("%s %s %s",first_person,first_time,last_time);
    strcpy(last_person,first_person);
    for(int i=1;i<m;i++){
        char x[20],y[20],z[20];
        scanf("%s %s %s",x,y,z);
        if(strcmp(first_time,y)>0){
            strcpy(first_time,y);
            strcpy(first_person,x);
        }
        if(strcmp(z,last_time)>0){
            strcpy(last_time,z);
            strcpy(last_person,x);
        }
    }
    printf("%s %s\n",first_person,last_person);
}

```

