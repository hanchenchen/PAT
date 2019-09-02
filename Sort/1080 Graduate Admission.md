# 1080 **Graduate Admission**

```c++
#include<iostream>
#include<queue>
#include<vector>
#include<string.h>
#include<set>
#include<algorithm>
using namespace std;
const int maxN=40005;//the total number of applicants
const int maxK=10;//the number of choices an applicant may have
const int maxM=105;//the total number of graduate schools
//const int maxInt=2147483647;
struct STU{
    int id,gE,gI,score,rank;
    int choices[maxK];
    //string name;
}stu[maxN];
int n,m,k;
int quota[maxM];

int main(){
    cin>>n>>m>>k;//applicants schools choices
    for(int i=0;i<m;i++){
        scanf("%d",&quota[i]);
    }
    for(int i=0;i<n;i++){
        stu[i].id=i;
        scanf("%d %d",&stu[i].gE,&stu[i].gI);
        stu[i].score=stu[i].gE+stu[i].gI;
        for(int j=0;j<k;j++){
            scanf("%d",&stu[i].choices[j]);
        }
    }
    sort(stu,stu+n,[](const STU a,const STU b){
        if(a.score!=b.score){
            return a.score>b.score;
        }
        return a.gE>b.gE;
    });
    int r=0;
    for(int i=0;i<n;i++){
        if(i>0&&stu[i].score==stu[i-1].score&&stu[i].gE==stu[i-1].gE){
            
        }else{
            r=i;
        }
        stu[i].rank=r+1;
        //cout<<r+1<<" "<<stu[i].id<<" "<<stu[i].score<<endl;
    }
    vector<int> admit[maxM];
    for(int i=0;i<n;i++){
        for(int j=0;j<k;j++){
            int shool=stu[i].choices[j];
            if(admit[shool].size()<quota[shool]){
                admit[shool].push_back(i);
                break;
            }
            if(stu[admit[shool].back()].rank==stu[i].rank){
                admit[shool].push_back(i);
                break;
            }
        }
    }
    for(int i=0;i<m;i++){
        for(int j=0;j<admit[i].size();j++){
            admit[i][j]=stu[admit[i][j]].id;
        }
    }
    for(int i=0;i<m;i++){
        sort(admit[i].begin(),admit[i].end());
        if(admit[i].size()){
            printf("%d",admit[i][0]);
            for(int j=1;j<admit[i].size();j++){
                printf(" %d",admit[i][j]);
            }
        }
        printf("\n");
    }
    return 0;
}
```

