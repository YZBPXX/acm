####  二分图匹配
> 概念
> 二分图：点可以被分为x,y组，两组相连接，并且组内不能连接（等价于不存在含奇数条边的环）
> 匹配：边的集合，其中任意两条边没有公共顶点
> 饱和点：如果点v在匹配中，则称v为饱和点（相对匹配来说）
> 交错路：匹配边和非匹配边交替出现
> 增广路：起点和终点都是非饱和点的交错路
> 最大匹配：边数最大
> Berge定理: 如果不存在增广路，那么该匹配是最大匹配
> 完美匹配：所有的点都能匹配
> 相等子图：边两端顶点标号相加大于等于边权的边构成的图

- 最大匹配：匈牙利算法O(VE) (每个点都需要遍历它的全部边）
```
for 每次找一个非饱和点，深度搜索是否存在一个以非饱和点为节点的路径
    if 存在
        将此次的路径作为匹配
    else 
        说明此时已经是最大匹配了(不包括后面的点）
````
- 例题[hdu2063](https://acm.hdu.edu.cn/showproblem.php?pid=2063)
模版
```c++
#include<iostream>
#include<cstring>
#include<vector>
using namespace std;
int visit[510],  gf[510];
vector<int>  cp[510];
int k,n,m;
bool dfs(int x){
   for(int i=0,n=cp[x].size();i<n;i++){
         int y=cp[x][i];
         if(visit[y]==0){
             visit[y]=1;
             if(gf[y]==0||dfs(gf[y])){
                 gf[y]=x;
                 return 1;
             }
         }      
   } 
   return 0;
}
int main(){

    while(scanf("%d %d %d",&k,&n,&m),k!=0){
        memset(gf,0,sizeof(gf));
        for(int i=0;i<=509;i++)cp[i].clear();
        for(int i=0;i<k;i++){
            int x,y;
            cin>>x>>y;
            cp[x].push_back(y);
        }
        int sum=0;
        for(int i=1;i<=n;i++){
            memset(visit,0,sizeof(visit));
            if(dfs(i))sum++;
        }
        cout<<sum<<endl;
    }
}
```
- 最大权完美匹配: KM算法
- 问题描述：某一个party里有n个男生，n个女生。两两间的好感度为$a_{ij}$，问如何匹配使得他们的好感度最高;如图
```
for 每一次非饱和点判断是否能在不改变期望值的情况下找个合适的匹配（最大匹配）
    如果能皆大欢喜
    如果不能找到好感度最高的匹配，那么此时好感度必然需要下降才能满足要求，但是考虑是哪一个下降，解决的办法就是，两个都下降，但是互相争夺的匹配点上升，这样两个肯定会有一个与匹配点匹配（从而保持总和不变），另外一个则下降, 与一个非饱和点匹配（总和下降）, 然后重新匹配一次, 
    如果每次下降一点幸福感，收敛太慢。可以通过记录每个非饱和男生(当前尝试过的）要成功匹配最少还差多少辛福感，使得每次减少都有一个非饱和男生成功匹配（松弛操作），时间复杂度：遍历n个点，每个点找一次增广路要n, 如果不能匹配则要修改顶标n，总共O(n^3)
```

```c++
#include<iostream>
#include<cstring>
#include<cstdio>
#include<cmath>
using namespace std;
const int MAX=305;
const int INF=0x4f4f4f4f;
int N;
int vis_girl[MAX];
int vis_boy[MAX];
int ex_girl[MAX];
int ex_boy[MAX];
int love[MAX][MAX];
int match[MAX];
int slack[MAX];
int dfs(int girl){
    vis_girl[girl]=true;
    for(int boy=0;boy<N;++boy){
        if(vis_boy[boy])continue;
        int gap=ex_girl[girl]+ex_boy[boy]-love[girl][boy];\\ 注意这里必须是正的
        if(gap==0){//下一个匹配点未标记, 所以总和期望下降
            vis_boy[boy]=true;
            if(match[boy]==-1||dfs(match[boy])){
               match[boy]=girl;
                return true;
            }
        } else {
            slack[boy]=min(slack[boy],gap);
        }
    }
    return false; }
int KM(){
    memset(match,-1,sizeof(match));
    memset(ex_boy,0,sizeof(ex_boy));
    for(int i=0;i<N;i++){
        ex_girl[i]=love[i][0];
        for(int j=1;j<N;j++){
           ex_girl[i]=max(ex_girl[i],love[i][j]);
        }
    }
    for(int i=0;i<N;i++){
        fill(slack,slack+N,INF);
        memset(vis_girl,0,sizeof(vis_girl));
        memset(vis_boy,0,sizeof(vis_boy));
        while(1){
            memset(vis_girl,0,sizeof(vis_girl));
            memset(vis_boy,0,sizeof(vis_boy));
            if(dfs(i)) break;
           int d = INF;
           for(int j=0;j<N;j++){
              if(!vis_boy[j]) d=min(d,slack[j]); 
           }
           for(int j=0;j<N;j++){
               if(vis_girl[j])ex_girl[j]-=d;
               if(vis_boy[j])ex_boy[j]+=d;
           }
        }
    }
   int res=0;
   for(int i=0;i<N;i++){
       res+=ex_boy[i]+ex_girl[match[i]];
   }
   return res;
}
int main(){
    ios::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    while (cin>>N) {
        for (int i = 0; i < N; ++i)
            for (int j = 0; j < N; ++j)
                cin>>love[i][j];
        cout<<KM()<<endl;
   } 
    return 0;
}
```
