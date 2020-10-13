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

##### 去重

```
sort(a+1,a+n+1);
n=unique(a+1,a+n+1)-a-1;
```

a,b交换

```c++
a,b=b,a
```



清空数组

```c++
memset(apple,0,sizeof(apple[0])*(n+1)); // apple 的每个元素初始化为 0，需要多少清楚多少
```



#### 查找

```
sort(num,num+6,cmd);                      //按从大到小排序
int pos3=lower_bound(num,num+6,7,greater<int>())-num;  //返回数组中第一个小于或等于被查数的值 
int pos4=upper_bound(num,num+6,7,greater<int>())-num;  //返回数组中第一个小于被查数的值 
```



#### 常用数学函数

1. ```c++
   __gcd(a,b);
   ```

   

2. 查找一个数的二进制形式中有多少个1，  

```
__builtin_popcount(i)
```

#### cin加速

cin加速

```
	ios_base::sync_with_stdio(0), cin.tie(0);
```



#### 极大值

```
    const int MAX = numeric_limits<int>::max();

```



printf转义字符

```
    printf("%Lf",longdoublevalue);\\打印long double 类型
      if(hh<12)printf("%02d:%02d",hh,mm); \\不足两位用0补前导

```



#### STL

##### set

```c++
 // lower_bound()找到大于或等于某值的第一个元素的迭代器
  set<int>aa;
  aa.insert(3);
  aa.insert(10);
  printf("%d",*aa.lower_bound(4)); //打印10
```

**value_comp**()    来自[博客1](https://zhidao.baidu.com/question/281009061.html)

C++中的map::value_comp()原型是:
value_compare value_comp ( ) const;
其返回值是一个bai比较类的对du象，这个类是map::value_compare，并且是map的一个内部类zhi。
返回的这dao个对象可以用来通过比较两个元素的value来判决它们对应的key在map的位置谁在前面谁在后面。

```c++
map<char,int> mymap;
map<char,int>::iterator it;
pair<char,int> highest;

mymap['x']=1001;
mymap['y']=2002;
mymap['z']=3003;

cout << "mymap contains:\n";

highest=*mymap.rbegin(); // last element

it=mymap.begin();
do {
cout << (*it).first << " => " << (*it).second << endl;
} while ( mymap.value_comp()(*it++, highest) );


```

输出结果为

```
mymap contains:
x => 1001
y => 2002
z => 3003
```

