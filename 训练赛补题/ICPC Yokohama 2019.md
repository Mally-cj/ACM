前言：
交题链接：[A题](https://vjudge.net/problem/Aizu-1400)    [B题](dge.net/problem/Aizu-1401)  

### A-FastForwarding

题意：初始a为1，对于下一秒的a有3种选择，一种是a=a*3，一种是a=a/3, 还有一种就是a不变，a最小只能为1， 每一秒sum会加上a，现在问最短需要多少时间可以使得sum=n，且最终a=1.

解法：

<一> 贪心

想要用最大的速度走，同时要保证最终能把速度退到1.

如果当前sum+a*3<n, 那么就可以a=a\*3，   







B 题

**题意**： 给出w*d的方阵，给出n块方块的海拔高度，每块相邻方块之间的高度差为0或者1，问这个方针的最小海拔高度为多少？

**解法**：

<一>

对于每一个给定海拔的台阶，它周围的海拔范围是（z-d，z+d），这个d可以用 欧几里得距离算出来。
对于高海拔台阶来说，要使得总体海拔最小，则尽可能按最大差距进行递减，对于低海拔台阶来说，要使得和台阶最大海拔差距小于等于1，按最大差距进行递增，对于每个给定的台阶，都可承担两个角色，高海拔/低海拔，然后对未知海拔台阶按照两种角色进行推测，若出现某台阶的从已知低海拔上升的最高海拔比从已知高海拔下降到最低海拔还要低，则出现矛盾。

如果没有出现矛盾，则说明必然存在，那么就选择最小方案。

```c++
#include<iostream>
#include<algorithm>
#include<cstdio>
#include<string>
#include<cstring>
#include<cmath>
#include<sstream>
#include<queue>
#include<vector>
#include<map>
#include<set>
#define ll long long
#define INF 0x3f3f3f3f
using namespace std;
int mp[100][100];
int vis[100][100];
int mp_max[100][100];
int mp_min[100][100];
int main() {
//    freopen("in.text","r",stdin);

    int w, d, n;
    memset(vis, 0, sizeof(vis));
    cin >> w >> d >> n;
    for (int i = 1; i <= w; i++) {
        for (int j = 1; j <= d; j++) {
            mp_max[i][j] = 1005;
            mp_min[i][j] = -1005;
        }
    }

    for (int i = 0; i < n; i++) {
        int x, y, z;
        cin >> x >> y >> z;
        mp[x][y] = z;
        vis[x][y] = 1;
        for (int i = 1; i <= w; i++) {
            for (int j = 1; j <= d; j++) {
                int dis = abs(x - i) + abs(y - j);
                int dis_max = z + dis;
                mp_max[i][j] = min(mp_max[i][j], dis_max);
                int dis_min = z - dis;
                mp_min[i][j] = max(mp_min[i][j], dis_min);
            }
        }
    }
    int sum = 0;
    int flag = 1;
    for (int i = 1; i <= w; i++) {
        for (int j = 1; j <= d; j++) {
            if (mp_max[i][j] < mp_min[i][j]) {
                flag = 0;
                break;
            }
            if (vis[i][j] == 0) {
                sum += mp_min[i][j];
            } else {
                sum += mp[i][j];
            }
        }
        if (flag == 0) break;
    }
    if (flag) {
        cout << sum << endl;
    } else {
        cout << "No" << endl;
    }
}
```

<二> 

既然是要使得总海拔最低，也已经给了最高海拔，那么每次就从队列里取出当前最高海拔的位置，让这个位置周围的四个海拔降低1（如果该方块未被定义）。如果该方块已经被定义过了，而不能保证与当前位置的水平差距为1，那么就说明会出现矛盾，不成立。

```
#include "bits/stdc++.h"
#define inf 0x3f3f3f3f
using namespace  std;
struct re{
    int x,y,v;
    re(int a,int b,int c){x=a;y=b;v=c;}
    bool operator<(const re &it)const {
        if(v!=it.v)return v<it.v;
        else if(x!=it.x)return x<it.x;
        else return y<it.y;
    }
};

priority_queue<re>have;
int stepx[]={-1,1,0,0};
int stepy[]={0,0,1,-1};
int mp[200][200];
int main()
{
//    freopen("in.text","r",stdin);
    int W,D,n;
    int suc=1,ans=0;

    scanf("%d %d %d",&W,&D,&n);
    memset(mp,inf,sizeof(mp));
    for(int a,b,c,i=1;i<=n;++i)
    {
        scanf("%d %d %d",&a,&b,&c);
        have.push(re(a,b,c));
        mp[a][b]=c;
        ans+=c;
    }
    while (suc&&!have.empty())
    {
        re tem=have.top();have.pop();
        for(int i=0;i<4;++i)
        {
            int nx=tem.x+stepx[i];
            int ny=tem.y+stepy[i];
            if(nx<=0||ny<=0||nx>W||ny>D)continue;

            if(mp[nx][ny]!=inf)continue;
            else {
                mp[nx][ny]=tem.v-1;
                if(mp[nx][ny]>100)suc=0;
                for(int k=0;k<4;++k){
                    if(nx+stepx[k]<1 ||ny+stepy[k]<1 ||nx+stepx[k] >W ||ny+stepy[k] >D)continue;

                    int ff=mp[nx+stepx[k] ][ny+stepy[k]];

                    if(ff!=inf&&abs(ff-mp[nx][ny] )>1){ suc=0;break;}
                }
                ans+=mp[nx][ny];
                have.push(re(nx,ny,mp[nx][ny]));
            }
        }
    }
    if(suc)printf("%d\n",ans);
    else puts("No");
    return 0;
}
```

