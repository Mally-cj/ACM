# CodeForces - 1151B 思维

## 题意

有一个n行m列的矩阵，问能否从每行里取出一个数，使得n个数字异或后不为0

## 记录

4个月前做是用纯粹的暴力去做，没有过，原因是那时在赛场上没有很潜下心去相通。

今天再看这个题目，之前的暴力没有对重复数字进行优化,试着对这个点优化暴力过了。

虽然从异或角度，没有发现可用的，但是发现4个连续的数字异或后为0。（从0开始算起）

再看网上题解，真的很妙，这就是一道思维题。

## 正解

<一>思维

如果第一列的值异或和>1,就直接全输入1即可，如果等于0，我们只要在任意一行中找到一个不等于这一行的第一个元素就行，因为其他数异或这行第一个数为0，那其他数异或这个不等于第一个的数肯定大于1。

网上这种解法的代码很多，就不贴了。

<二>暴力

去重之后，直接搜索。

```c++
#include "cstdio"
#include "iostream"
using namespace std;
const int N=509;
const int M=509;
int use[N][N];
int have[N][M];
int num[N];
int ans[N];

int dfs(int ceng,int val)
{
    if(ceng==0)return val;
    for(int i=1;i<=num[ceng];++i)
    {
        if( dfs(ceng-1,val^have[ceng][i]))
        {
           ans[ceng]=have[ceng][i];
            return 1;
        }
    }
    return 0;
}
int main()
{
//    freopen("in.text","r",stdin);
    int n,m;
    scanf("%d %d",&n,&m);
    for(int i=1;i<=n;++i)
        for(int d=1,a;d<=m;++d)
        {
            scanf("%d",&a);
            if(use[i][a]==0)
            {
                use[i][a]=d;
                have[i][++num[i]]=a;
            }
        }
    int suc=0;

    if(dfs(n,0)) {
        printf("TAK\n");
        for (int i = 1; i <= n; ++i) {
            printf("%d ", use[i][ans[i]]);
//            printf("%d\n",ans[i]);
        }
    }
    else printf("NIE\n");
    return 0;
}
```

