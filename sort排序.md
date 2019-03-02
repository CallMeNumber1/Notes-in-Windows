## 使用sort排序

```cpp
#include <algorithm>
sort(arr, arr + 5);				// 从arr开始到第五个元素按从小到大的顺序排列
sort(arr + i, arr + j) 			// 被排序的是arr[i]到arr[j - 1]
```

#### 从大到小排序

```cpp
sort(arr, arr + 5, greater<int>());
第三个参数为排序方法
<int>代表待排序的数组中的元素类型为int
```

#### 二级排序

```cpp
typedef struct Node{
    int grade;
    int num;
}Node;
//比较函数写法，按成绩从高到低排序，当成绩相同时按编号从低到高排序
bool cmp(Node a,Node b)
{
    if(a.grade == b.grade)
        return a.num<b.num;
    return a.grade>b.grade;
}
```

#### 注意事项：

**`sort排序如何变为稳定排序`**

sort是不稳定排序，若想实现稳定排序

可在待排序的结构体内增加一个字段num，记录输入的次序

当两个结构体变量的排序字段相等时，按照num升序，即实现了稳定排序

## 结构体的构造函数

1. C++中结构体内不仅可以定义变量成员，也可以定义函数成员

2. 在同一个结构体中，不能出现两个默认构造函数

3. 如果在结构体中自定义了一个构造函数（任意形式），编译器就不会为我们定义默认构造函数了，这个时候如果需要，自己再定义它

4. 初始化列表：在构造函数的括号后面加一个冒号，然后按照`成员变量（参数）`的形式，依次对每一个变量进行初始化

   在初始化变量之后，还要别的事情要做，可以把代码写在大括号里

   就算什么都不做，大括号也不能省略



## 四舍五入

```cpp
floor(), ceil(), round() 均为取整函数

四舍五入保留整数：
int a = b + 0.5
四舍五入保留一位小数：
int a = (b + 0.05) * 10;
double c = a / 10;
四舍五入保留二位小数:
int a = (b + 0.005) * 100;
double c = a / 100;
注意：上面的三个方法仅适用于正数
```

## 注意事项

- 对于new出来的数组，使用memset会出错！
- 传递指针的引用

```cpp
void func(int *&p) {
    p = new int;
    return ;
}
```



