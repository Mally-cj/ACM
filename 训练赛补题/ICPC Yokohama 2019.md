前言：
交题链接：[A题](https://vjudge.net/problem/Aizu-1400)    [B题](https://vjudge.net/problem/Aizu-1401)  

### A-FastForwarding

题意：初始a为1，对于下一秒的a有3种选择，一种是a=a*3，一种是a=a/3, 还有一种就是a不变，a最小只能为1， 每一秒sum会加上a，现在问最短需要多少时间可以使得sum=n，且最终a=1.

解法：

<一> 贪心

想要用最大的速度走，同时要保证最终能把速度退到1.

如果当前sum+a*3<n, 那么就可以a=a\*3，   







B 题