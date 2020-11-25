# SDKD 2019 Spring Training Series C3 1st Round

**End:** 2019-03-06 21:30 CST

## [B - 石子合并问题--直线版](https://vjudge.net/problem/HRBUST-1818)

 [HRBUST - 1818](https://vjudge.net/problem/HRBUST-1818/origin)

区间dp，看 某学长的代码的。

dp[i] [j] 表示把i和j之间的堆成一堆花费的最小数额。

```
#include "cstdio"
#include "cstring"
#include "algorithm"
using namespace std;
#define INF 0x3f3f3f3f
const int maxn=109;
int big[maxn][maxn],small[maxn][maxn];
int n,num[maxn],sum[maxn];
int main()
{
//    freopen("in.text","r",stdin);
    while (scanf("%d",&n)!=EOF)
    {
        memset(small,INF, sizeof(small));
        memset(big,0, sizeof(big));
        sum[0]=0;
        for(int i=1;i<=n;++i)
        {
            scanf("%d",&num[i]);
            sum[i]=sum[i-1]+num[i];
            small[i][i]=0;
        }
        for(int len=1;len<=n;++len)
            for(int i=1;i+len<=n+1;++i)
                for(int k=i,j=i+len-1;k<j;++k)
                {
                    small[i][j]=min(small[i][j],small[i][k]+small[k+1][j]+sum[j]-sum[i-1]);
                    big[i][j]=max(big[i][j],big[i][k]+big[k+1][j]+sum[j]-sum[i-1]);
                }
        printf("%d %d\n",small[1][n],big[1][n]);
    }
    return 0;
}
```

### 学长的题解

```
七个题
难度顺序： 1.hdu 1283 模拟
2.HRBUST 1818 区间dp
3.hdu 1506 单调栈/笛卡尔树
4.uva11624 多源bfs
5.poj 1269 叉积
6.hdu 4544 优先队列
7.hdu 1426 搜索



题解： 本套题我是尽量按照我对难度的理解从A到G排的顺序。基本上每道题都是可以直接看出算法的。

A：c语言难度的模拟题 

B：最简单的区间dp，只不过要维护一个最大值一个最小值 

C：这个题我们如果知道了每个点以他为最矮的最长区间，那么枚举每个乘它的最长区间就可以了。那么给出一个数列，维护每个值最小的最大区间显然可以用单调队列或者单调栈直接做。

 D：训练指南上的原题，多源BFS。我的做法是先用多源bfs跑以火为起点的，然后记录出火到每个格子的最短时间。然后在用普通bfs跑人，当目标格子在当前时间还没有火到达的时候可以转移。我当时验题的时候没有考虑到人一开始就能直接逃出去然后wa了一发。

E：用叉积就可以解决。

F：优先队列 将兔子按照血量从大到小排序，把剑按照伤害大小从大到小排序。然后枚举每只兔子，维护一个指针来表示能杀死当前兔子的最小伤害的弓箭的下标，然后在所有能杀死这个兔子的弓箭里面找到花费最少的。那么移动指针的时候把这些弓箭放进有限队列就可以了。

G：这个搜就完事了。
```





* hhlllo
* kkk
* jjjj