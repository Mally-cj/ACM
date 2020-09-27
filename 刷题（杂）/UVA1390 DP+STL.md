UVA 1390 DP+STL

### 记

这道题目好好看过,但是没有好好想过,  网上的都是哈希,但是 看到一篇博客用vector和map写的是真好, [传送们](https://blog.csdn.net/bluebayou/article/details/104171326?utm_source=app)

但是我现在还存在疑惑不懂的就是 30个点,最多会出现多少种分组情况, 这个最大值会不会爆出数组,但是我也没有从网上找到答案.所以对于这一题,我不确认这个算法能否再限定的时间下跑完最糟糕的情况 .



### 题意

输入一个n个点，m条边的无向图G($n\leq 30，m\leq 1000$)。每次随机增加一条非自环的边（u，v）（加完后可以重边）。添加每条边的概率是相等的，求使G连通的期望操作次数。

分析

每个无向图看作一个状态，

当前状态先记作S,  dp[S]表示这个状态的期望值，这个状态下有a个连通体，这些联通体的边数分别是$k_i$

新连一条边，这条边重边的概率为
$$
p_0=\sum_{i=1}^{i=a}\frac{C_{k_i}^2}{C_n^2}=\frac{\sum_{i=1}^n k_i*(k_i-1)}{n(n-1)}
$$

那么不重边的概率就是$1-p_0$

那么算出不重边的情况数,除以不重边的概率就可以知道当前这个状态下有多少种情况,故得总公式
$$
dp[S]=\frac{\sum_{i=1}^{n}(dp[s_i]*p_i)+1}{1-p_0}
$$


### 代码

```c++
#include<bits/stdc++.h>
using namespace std;
const int MAXN=1E6;
int n,m;
int g[40][40],vis[40],group[40];
double dp[MAXN];        //每种情况的期望值是double类型
vector<vector<int> >vs;  //每一种情况dp【s】都是一个vector<int>
map<vector<int>,int>ids;

void dfs(int a,int id)
{
    vis[a]=1;
    ++group[id];
    for(int i=1;i<=n;++i)
    {
        if(vis[i]==0&&g[a][i]==1)dfs(i,id);
    }
}
int ID(vector<int> v)
{
    if(ids.count(v)==0){
        ids[v]=vs.size();
        vs.push_back(v);
    }
    return ids[v];
}
inline  double  C(int x){ return  (double)x*(x-1)/2;  }
double  DP(int id)
{
    if(dp[id] )return dp[id];

    vector<int>v=vs[id];

    if(v.size()==1)return 0;
    double ci=0,cn=C(n);
    for(int i=0;i<v.size();++i)ci+=C(v[i]);
    double p=ci/cn,seg=0;

    for(int i=0;i<v.size();++i)
        for(int j=i+1;j<v.size();++j){
            double  pi=(v[i]*v[j])/cn;
            vector<int> tmp=v;
            tmp.erase(tmp.begin()+i);
            tmp.erase(tmp.begin()+j-1);
            tmp.push_back(v[i]+v[j]);
            sort(tmp.begin(),tmp.end());
            int id=ID(tmp);
            seg+=DP(id)*pi;
        }
    return dp[id]=(seg+1)/(1-p);
}
int main()
{
//    freopen("in.text","r",stdin);
    while(cin>>n>>m){
        memset(g,0, sizeof(g));
        memset(vis,0, sizeof(vis));
        memset(dp,0, sizeof(dp));
        memset(group,0, sizeof(group));
        int cnt=0;  //有几个连通体

        for(int a,b,i=1;i<=m;++i){cin>>a>>b;g[a][b]=g[b][a]=1;}
        for(int i=1;i<=n;++i)if(vis[i]==0)dfs(i,++cnt);

        sort(group+1,group+1+cnt);

        vector<int>tem(group+1,group+1+cnt);
        printf("%.6lf\n",DP(ID(tem)));
    }
    return 0;
}
```

























