#  [kuangbin带你飞]专题六 最小生成树

### poj1679

次小生成树

解法<一> 简单枚举

时间复杂度是$O( (V log_2V+E) *E);$

1.kruscal建立最小生成树BST，时间复杂度是$O( V log_2V+E);$。

2.BST中只要有一条边没有被用到，就不是原来的树，基于这个原理，去

暴力枚举每条边。

[krscal建立](https://blog.csdn.net/Albert_Bolt/article/details/82253141)

<二> 

[prime和dijkstra区别](https://www.cnblogs.com/yuyixingkong/p/3464267.html)

a.prime是找距离出发区域最小的边，dijkstra是找距离起点最近的边。

1.dijkstra建立从1