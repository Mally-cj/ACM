# 北京理工大学ACM冬季培训课程笔记

视频地址：https://www.bilibili.com/video/BV1pE411E7RV?from=search&seid=5720876971363950839



小记：

2020.5.3到 第一节 53分钟处

## lesson 1 C++ STL

断点调试



endl和"\n"有区别，endl可以清除缓冲区。



cin.getline 用于读一行，但是要加读入的字符数上限

```
cin.getline(cString,10000);
getline(cin,cString);
```

cin的速度比scanf慢不少（哪怕是关闭了同步）



C++语法特性 ——bool

* 动态开辟内存

  与c中的malloc类似，C++中用new来动态开辟内存，new写起来更简明

  ```
  int *a=new int[100];
  ```

  c++不支持变长数组

* 引用

  用&来创建引用

  