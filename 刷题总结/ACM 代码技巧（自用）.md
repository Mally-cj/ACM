# ACM 代码技巧（自用）



[查区域赛样例数据](https://blog.csdn.net/iwts_24/article/details/79240987)

#### 队列清空

```c++
inline void clearPQ (priority_queue<int> &q) {priority_queue<int> tmp; swap(tmp, q);}
```

#### 队列的自定义顺序

<一>

```c++
bool operator < (A a1, A a2){
	return a1.r < a2.r;
}
 
bool operator > (A a1, A a2){
	return a1.l > a2.l;
}
 
priority_queue<A, vector<A>, greater<A> > que1;		// 递增 - 对应>
priority_queue<A, vector<A>, less<A> > que2;		// 递减 - 对应<

```

<二>

```c++
struct cmp {
    bool operator() (const re &a, const re &b) const {
        return a.p < b.p;
    }
};
priority_queue<re,vector<re>,cmp > have;
```

表示a+1

```
a=a|1
```

去重

```
sort(a+1,a+n+1);
n=unique(a+1,a+n+1)-a-1;
```

a,b交换

```c++
a,b=b,a
```



#### 查找

```
sort(num,num+6,cmd);                      //按从大到小排序
int pos3=lower_bound(num,num+6,7,greater<int>())-num;  //返回数组中第一个小于或等于被查数的值 
int pos4=upper_bound(num,num+6,7,greater<int>())-num;  //返回数组中第一个小于被查数的值 
```

