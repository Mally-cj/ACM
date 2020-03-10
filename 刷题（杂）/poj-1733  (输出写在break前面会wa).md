# poj-1733  (输出写在break前面会wa)

###  :heart: 并查集妙用

### 题意：

有n个位置，有m句话说（a,b)范围内1的个数是奇数还是偶数。问第几句话开始出错。

题解：

如果用最普通的方法就是（sum[b]-sum[a-1]）%2= ？。那样前提是知道每个sum，也就是sum[i]-sum[0],

而这题中我们假设sum[a-1]=0;可知（sum[b]-sum[a-1]),也就是说以a-1为父亲，b为儿子，表示的是知道这一段的数字是多少。这解释了a和b建立父子关系的含义。

如果知道sum[c],并且有sum[a]-sum[c]和sum[b]-sum[a]这两段关系，也就知道了sum[b]-sum[a]。这解释了当两个祖宗相同时，表示的含义。

由于使用了路径压缩，故要进行权值转移。

[带权并查集原理](https://blog.csdn.net/yjr3426619/article/details/82315133)

### wa点：

  :angry: 把答案i-1写在break前面会wa，写在结尾不会wa！！！ :anger::anger::anger:



```c++
#include "cstdio"
#include "algorithm"
using namespace std;
const int maxn=1e4+10;
int rak[maxn],fa[maxn];
struct  re
{
    int a,b,c;
};
re data[maxn];
int all[maxn],n,m;
void input()
{
    int a,b,c;
    char ch[10];
    for(int i=1;i<=m;++i)
    {
        scanf("%d %d %s",&data[i].a,&data[i].b,ch);
        if(ch[0]=='o')data[i].c=1; else data[i].c=0;
        data[i].a--;
        all[i*2-1]=data[i].a;
        all[i*2]=data[i].b;
    }
    sort(all+1,all+m*2+1);
    n=unique(all+1,all+m*2+1)-all-1;

    for(int i=0;i<=n;++i)
    {
        rak[i]=0;fa[i]=i;
    }
}
int anc(int a)
{
    if(fa[a]==a)return a;
    int k=anc(fa[a]);
    rak[a]=(rak[a]+rak[ fa[a]]+2)%2;
    return  fa[a]=k;
}
void connect(int a,int b,int c)
{
    int fa_a=anc(a);
    int fa_b=anc(b);
    fa[fa_b]=fa_a;
    rak[fa_b]=(rak[a]+c-rak[b]+2)%2;
}
int main()
{
//    freopen("in.text","r",stdin);
    while (scanf("%d %d",&n,&m)!=EOF) {
        input();
       int i;
        for ( i = 1; i <= m; ++i) {
            int x = lower_bound(all + 1, all + n+1, data[i].a) - all;
            int y = lower_bound(all + 1, all + n+1, data[i].b) - all;
            int fa_x = anc(x);
            int fa_y = anc(y);
            if (fa_x == fa_y) {
                if ((rak[y] +data[i].c + 2) % 2 != rak[x]) {
//                    printf("%d\n",i-1);            //写在这边会wa。
                    break;
                }
            }
            else  if(fa_y>fa_x)connect(x, y, data[i].c);
            else if(fa_x>fa_y)connect(y,x,data[i].c);
        }
        printf("%d\n",i-1);
    }
    return 0;
}
```

