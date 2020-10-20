## uva 1650 数位dp

参考博客：[传送门1](https://blog.csdn.net/zju2016/article/details/78571087?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522160254600019724848301777%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=160254600019724848301777&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v3~pc_rank_v2-3-78571087.first_rank_ecpm_v3_pc_rank_v2&utm_term=UVA1650&spm=1018.2118.3001.4187)，[传送门2](https://blog.csdn.net/bluebayou/article/details/103837223)， [传送门3](https://www.cnblogs.com/TheRoadToTheGold/p/7465734.html)

> 紫书习题10-28 ，P347
>
> 20201013 没有想明白；非原创，只是急于准备比赛

**题意：**

每个排列都可以算出一个特征，即从第二个数开始每个数和前面一个数相比是增加(I)还 

是减少(D)。例如，{3,1,2,7,4,6,5}的特征是DIIDID。输入一个长度为*n*-1（2≤*n*≤1001）的字符 

串（包含字符*I*, D*和?），统计1～*n*有多少个排列的特征和它匹配（其中?表示I和D都符 

合）。输出答案除以1000000007的余数。



##### 会tle但是思路清晰的写法

```c++
#include<cstdio>
#include<cstring>
#define mod 1000000007
#define N 1000
using namespace std;
char s[N+5];
int dp[N+5][N+5];
int main()
{
    while(scanf("%s",s)!=EOF)
    {
        int len=strlen(s);
        memset(dp,0,sizeof(dp));
        for(int i=0;i<=len;i++) dp[0][i]=1;
        for(int i=1;i<=len;i++)
            for(int j=0;j<=i;j++)
            {
                if(s[i-1]=='D' || s[i-1]=='?') 
                    for(int k=j;k<i;k++) dp[i][j]+=dp[i-1][k],dp[i][j]%=mod;
                if(s[i-1]=='I' || s[i-1]=='?')
                    for(int k=0;k<j;k++) dp[i][j]+=dp[i-1][k],dp[i][j]%=mod;
            }
        int ans=0;
        for(int i=0;i<=len;i++) ans+=dp[len][i],ans%=mod;
        printf("%d\n",ans);
    }
}
```

##### 可以ac的代码

```c++
#include <iostream>
#include <cstring>
#include <cmath>
using namespace std;
const int mod=1000000007;
int dp[1005][1005],sum[1005][1005],n;
char s[1005];
int main(){
  while(cin>>s){n=strlen(s);
    memset(dp,0,sizeof(dp));
    memset(sum,0,sizeof(sum));
    for(int j=0;j<=n;j++)dp[0][j]=1,sum[0][j]=j+1;;
    for(int i=1;i<=n;i++){
      if(s[i-1]!='I')dp[i][0]=sum[i-1][i-1],sum[i][0]=dp[i][0];
      for(int j=1;j<=i;j++){
	if(s[i-1]!='I')dp[i][j]=(sum[i-1][i-1]-sum[i-1][j-1]+mod)%mod;
	if(s[i-1]!='D')dp[i][j]=(dp[i][j]+sum[i-1][j-1])%mod;
	sum[i][j]=(sum[i][j-1]+dp[i][j])%mod;
      }
    }
    cout<<sum[n][n]<<endl;
  }
  return 0;
}

```

