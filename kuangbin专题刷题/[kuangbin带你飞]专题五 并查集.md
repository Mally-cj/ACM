# [kuangbin带你飞]专题五 并查集                

##### 写作风格

:star:表示我觉得有些难，还没怎么透

:heart:表示这是好题呀。可能是贴近实际生活的背景，可能是解法真是妙。​

[学习带权并查集原理](https://blog.csdn.net/yjr3426619/article/details/82315133)

### A. poj-2236

Wireless Network

**题意:**

有N台坏电脑的坐标，O x表示修复第x台电脑，S p q询问p和q这两台电脑能不能交流，交流的条件是，首先2台电脑得已经都被修复了，其次是p和q覆盖的网之间的距离不能超过d。

**题解：**

每次修好一台电脑就扫描所有点，以加入所有距离小于1的集合圈子内。不能只加一个，因为它可能是2个集合的连接点。



### B.poj-1611 并查集模板题

## The Suspects

**题意：**

有n个学生，m个聚会，给出每场聚会参加的人的号码，0号学生得了传染病SARS，问有几个人被传染得了SARS。



**题解：**

把每次聚会的人都做成一个并查集，最后对每个人看一遍是否和0号同学的祖宗相同。 

### C.hdu-1213 并查集裸题

```c++
#include "cstdio"
using namespace std;
int n,m;
const int maxn=3e4+10;
int fa[maxn],sure[maxn];
int anc(int a)
{
    if(fa[a]==a)return  a;
    return  fa[a]=anc(fa[a]);
}
void connect(int a,int b)
{
    int faa=anc(fa[a]);
    int fab=anc(fa[b]);
    fa[faa]=fab;
}
void  init(int n)
{
    for(int i=0;i<=n;++i)
    {
        fa[i]=i;
    }
}
int have[maxn];
int main(void)
{
   //freopen("in.text","r",stdin);
     int cas;
     scanf("%d",&cas);
     while (cas--)
     {
         scanf("%d %d",&n,&m);
         init(n);
         for(int i=1;i<=m;++i)
         {
             int a,b;
             scanf("%d %d",&a,&b);
             connect(a,b);
         }
         int ans=0,suc;
         for(int d=1;d<=n;++d)
         {
             suc=0;
            for(int i=1;i<=ans;++i)
                if(have[i]==anc(d))
                {   suc=1;
                    break;}
            if(!suc)have[++ans]=anc(d);

         }
        printf("%d\n",ans);
     }
    return  0;
}
```



###  E. poj-1182  :star:

### **题解：** 带权并查集好题

### F.  poj-1417 :heart:   并查集01模型+背包dp

​		*True Liars*

**题意：**

有n次对话，p1个好人，p2个坏人，问x2是一个好人吗，x1会回答yes或者no，如果x1是一个坏人他会说谎话，如果它是好人，他会说真话。

如果没有确切的证据找出这p1和p2个人，那么就写no。否则就按大小顺序输出。

**题解：**
$$
x1是天使\begin{cases}
x2是天使&说yes\\
x2是恶魔&说no\\
\end{cases}
$$

$$
x1是恶魔\begin{cases}
x2是恶魔&说yes\\
x2是天使&说no\\
\end{cases}
$$

由上分析知道说yes时两个人同属性，说no时不同属性。

故而做成并查集，有相关性的人会被放到同个集合内，而集合内有2种属性，即是否和根节点相同属性。

这时候就转化成另一个问题了，有（p1+p2)个数，其中有p1个A和p2个B，每组数里面有2种属性的人，各知道人数，但不知道是A还是B。



### G.poj-1456

**题意：**

超市里有N个商品. 第i个商品必须在保质期(第di天)之前卖掉, 若卖掉可让超市获得pi的利润.  每天只能卖一个商品. 现在你要让超市获得最大的利润. 

**题解**

[dp+并查集替链表||优先队列](https://blog.csdn.net/qq_43235540/article/details/104136285)

### H.poj-1733 :heart: 并查集妙用

**题意：**

有n个位置，有m句话说（a,b)范围内1的个数是奇数还是偶数。问第几句话开始出错。

**题解：**

[题解见此](https://blog.csdn.net/qq_43235540/article/details/104144262)

**wa点：**

  :angry: 把答案i-1写在break前面会wa，写在结尾不会wa！！！ :anger::anger::anger:



### poj-1984 :heart:

题解：

如果不是有限制在第几个条件之后才问这个问题，就可以用最短路算法了。

注意对问的问题要根据在第几个条件得到后去排序。