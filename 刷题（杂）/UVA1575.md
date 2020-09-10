## uva 1575 排列组合+dfs减枝

### 记

参考了这篇[博客](https://blog.csdn.net/qq_34416123/article/details/81234342)， 自己计算证明了为什么用那么些20多个素数就可以。

### 题意

给出n，对于f(k),求最小的k.

f(k) 的定义是 对k 质因数分解，问这些质因数的排列组合数。

### 思路

##### 主要思路

1. 对于k，$k=p_1^{a_1}*p_2^{a_2}...*p_m^{a_m}$,排列组合数就是 $\frac{(a_1+a_2+...a_m)!}{a_1!*a_2!*...a_m!}$ ,由此可见，其实与素数是什么没有关系的，主要是各个素数的数量是多少。

2.  
   $$
   x_0=\frac{(a_1+a_2+...a_m)!}{a_1!*a_2!*...a_m!}
   $$
   
   $$
   x_1=\frac{(a_1+a_2+...a_m+a_{m+1})!}{a_1!*a_2!*...a_m!*a_{m+1}!}
   $$
   
   $$
   \frac{x_1}{x_0}= \frac{(a_1+a_2+...a_m+a_{m+1})! }{(a_1+a_2+...a_m)!*a_{m+1}!}=\frac{sum1!}{sum2!*a_{m+1}!}=C_{sum2}^{a_{m+1}}
   $$
   

   由此发现在原来的基础上加上 $a_{m+1}$ 个新质数后的排列组合数，和旧的之间的关系。

   因此可以先打组合数表作为备用。

3. 那么这个sum最大会是多少呢，

   最糟糕的情况(在相同的n下) 是$\frac{sum!}{1!*2!*....i!}$,($sum=(1+i)*i/2$) , 因为这时候分子最大 

   而经过计算，在i到达20的时候，也就是sum到达80多的时候， $\frac{sum!}{1!*2!*....i!}$ 就会超过$2^{63}$

   因此制作素数表的时候，只要找到前30个就好；并且也可以确定组合数表的范围$C_b^a$ , b<90

   

   

##### 算法步骤

1. 打素数表找30个素数，打组合数表，找底数小于100的组合数
2. 为了让k尽可能小，那就是让前面的素数个数尽可能多。再利用dfs 减枝

### 代码

```c++
#include "bits/stdc++.h"
using namespace  std;
typedef unsigned long long ll;
const int N=100;
const int MAXN=1E6+10;
ll C[100][100];
int cnt=0,prime[N+10];
bool noprime[MAXN];
void Calumn()
{
    memset(C,0,sizeof(C));
    for(int i=1;i<=90;++i)   //通过估计，大概是80多就够用，所以取90
    {
        C[i][0] = 1;
        for (int j = 1; j <= i; ++j) {
            C[i][j] = C[i - 1][j - 1] + C[i - 1][j];
        }
    }
}
void make_prim()
{
    cnt=0;
    int i;
    for(i=2; cnt<=30 ;++i)  //通过估计，大概只会用到20个素数，所以取30
    {
        if(noprime[i])continue;
        prime[++cnt]=i;
        for(int d=i+i;d<=MAXN;d+=i)noprime[d]=1;
    }
}
ll target,ans;
void dfs(int last,ll value,int n,int dep,ll ans_tem)
{
    // last 表示上一种素数用了几个，以此限制当前素数个数
    // value 表示当前的组合数是多少了
    // n 表示截至上一个，已经有了几个因数了，因为在求组合数时要用到
    // dep是深度的意思，表示当前是第几种因数了
    // ans_tem 表示这些质因数的价值，因为题目说要求最小的，因此用此来减枝条。
    if(dep>23)return;  //超过了估计使用的素数种数
    if(ans_tem>=ans)return;
    if(value==target){ans=ans_tem;return;}

    ll tem=1;
    for(int i=1;i<=last;++i)
    {
        tem*=prime[dep];
        if(ans_tem>(ans/tem)||C[n+i][i]>target )continue;

        ll n_value=value*C[n+i][i];
        if(n_value>target)continue;
        dfs(i,n_value,n+i,dep+1,ans_tem*tem);
    }
}
int main()
{
//    freopen("in.text","r",stdin);
    Calumn();
    make_prim();
    while (cin>>target)
    {
        ans=numeric_limits<ll>::max();
        dfs(63,1,0,1,1);
        cout<<target<<" "<<ans<<endl;
    }

    return 0;
}

```

