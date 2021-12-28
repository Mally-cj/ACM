#### 1.购物单

解：手输数据



#### 2.等差素数列

解：2

不会，盲猜

代码

```c++
#include"bits/stdc++.h"
using namespace std;
const int MAXN=1E6+20;
bool noprime[MAXN];
int prime[MAXN],cnt;
typedef  long long ll;
void makeprime()
{
    for(int i=2;i<MAXN;++i)
     {
         if(noprime[i])continue;
         prime[++cnt]=i;
         for(int d=i*2;d<MAXN;d+=i)noprime[d]=1;
     }
}
int judge(int a)
{
    for(int i=1;i<=cnt&&(ll)prime[i]*prime[i]<=a;++i)
    {
        if(a%prime[i]==0)return 0;
    }
    return 1;
}
int main()
{
    makeprime();
    printf("cnt=%d\n",cnt);
    int suc=0;
    for(int cha=2;suc!=1;++cha)
    {
        for(int i=1;i<=cnt;++i)
        {
            int now=1;
            int fau=0;
            while(now<=10)
            {
                if(prime[i]+now*cha<MAXN&&noprime[ prime[i]+now*cha ]==1)
                {
                    fau=1;
                    break;
                }
                else if(prime[i]+now*cha>MAXN)
                {
                    if(judge(prime[i]+now*cha)==0)
                    {
                        fau=0;
                        break;
                    }
                }
                ++now;
            }
            if(fau==0){
                    suc=1;
                    for(int d=0;d<10;++d)
                        printf("%d ",prime[i]+cha*d);
                    printf("\n");
                    break;
            }

        }
        if(suc)
        {

            printf("cha=%d\n",cha);
            break;
        }
    }
    return 0;
}

```



#### 3.承压计算

没思路



#### 4.方格分割

有一些思路，麻烦先跳过



#### 5.取整位

```
#include"bits/stdc++.h"
using namespace std;
int len(int x)
{
    if(x<10)return 1;
    return len(x/10)+1;
}
int f(int x,int k)
{
    if(len(x)-k==0)return x%10;
    return  (int)(x/pow(10,len(x)-k))%10;
}
int main()
{
    int x=2398;
    printf("%d\n",f(x,3));

}

```



#### 6.最大公共子串

解：

```c++
 a[i][j]=a[i-1][j-1]+1;
```



```
#include<stdio.h>
#include<string.h>
#define N 256
int f(const char* s1,const char* s2)
{
    int a[N][N];
    int len1=strlen(s1);
    int len2=strlen(s2);
    int i,j;

    memset(a,0,sizeof(int)*N*N);
    int max=0;
    for(i=1;i<=len1;++i){
        for(j=1;j<=len2;++j){
            if(s1[i-1]==s2[j-1]){
                a[i][j]=a[i-1][j-1]+1;
                if(a[i][j]>max)max=a[i][j];
            }
        }
    }
    return max;
}
int main()
{
    printf("%d\n",f("abcdkkk","baabcdadabc"));
    return 0;
}

```



#### 7.日期问题

```
#include<stdio.h>
#include<string.h>
#include<vector>
#include<cstdio>
#include<algorithm>
using namespace std;
struct re
{
    int y,m,d;
    re(int a,int b,int c)
    {
        y=a;m=b;d=c;
    }
    bool operator <(const re &it)const{
    if(y!=it.y)return y<it.y;
    if(m!=it.m)return m<it.m;
    return d<it.d;
    }
};
vector<re>have;
int main()
{
    int a,b,c;
    scanf("%d/%d/%d",&a,&b,&c);

    if(a>=60)have.push_back(re(a+1900,b,c));
    if(c>=60)
    {
        have.push_back(re(c+1900,a,b));
        have.push_back(re(c+1900,b,a));
    }

    if(a<60)have.push_back(re(a+2000,b,c));
    if(c<60)
    {
        have.push_back(re(c+2000,a,b));
        have.push_back(re(c+2000,b,a));
    }

    sort(have.begin(),have.end());

    for(int i=0;i<3;++i)
        printf("%4d-%02d-%02d\n",have[i].y,have[i].m,have[i].d);
    return 0;
}

```



#### 8.包子凑数





#### 9.分巧克力

```
#include<cstdio>
#include<algorithm>
using namespace std;
const int MAXN=1E5+10;
int h[MAXN],w[MAXN],n,k;
bool ok(int a)
{
    int now=0;
    for(int i=1;i<=n;++i)
    {
        now+=(h[i]/a)*(w[i]/a);
    }
    if(now>=k)return 1;
    return 0;
}
int main()
{
   // freopen("C:/Users/29066/Desktop/in.txt","r",stdin);

    scanf("%d %d",&n,&k);


    int lef=1,rig=0,mid,ans=0;
    for(int i=1;i<=n;++i)
    {
        scanf("%d %d",&h[i],&w[i]);
        rig=max(h[i],rig);
        rig=max(w[i],rig);
    }


    while(lef<=rig)
    {
        mid=(lef+rig)/2;
        if(ok(mid))
        {
            ans=mid;
            lef=mid+1;
        }
        else
        {

            rig=mid-1;
        }
        //printf("lef=%d  rig=%d mid=%d\n",lef,rig,mid);
    }
    printf("%d\n",ans);
    return 0;
}

```







#### 10.k倍区间

```
#include<cstdio>
#include<algorithm>
using namespace std;
const int MAXN=1E5+10;
int all[MAXN],n,k;
int tree[MAXN*4+10];
bool is_node[MAXN*4+10];
void push_up(int id)
{
    tree[id]=tree[id*2]+tree[id*2+1];
}

void build(int lef,int rig,int id)
{
    if(lef==rig)
    {
        tree[id]=all[lef];
        is_node[id]=1;
        return;
    }
    if(lef>rig)return;
    int mid=(lef+rig)/2;

    build(lef,  mid,id*2);
    build(mid+1,rig,id*2+1);
    push_up(id);
     printf("%d :%d  %d   %d\n",id,lef,rig,tree[id]);
}
int get_ans(int id)
{
    if(is_node[id])
    {
        if(tree[id]%k==0)return 1;
        return 0;
    }

    int ans=0;

    ans+=get_ans(id*2)+get_ans(id*2+1);
    if(tree[id]%k==0 && tree[id]>=k)ans+=1;

    printf("id=%d ans=%d\n",id,ans);

  //  printf("id=%d  ans=%d       %d--%d  \n",id,ans,tree[id*2],tree[id*2+1]);
    return ans;
}
int main()
{
    freopen("C:/Users/29066/Desktop/in.txt","r",stdin);
    scanf("%d %d",&n,&k);
    for(int i=1;i<=n;++i)scanf("%d",&all[i]);
    build(1,n,1);

    //for(int i=1;i<=5;++i)printf("tree[%d]=%d\n",i,tree[i]);

    int ans=0;

    ans+=get_ans(1);

    printf("%d\n",ans);
    return 0;
}

```

