c++

1

由于嵌套包含文件的原因 一个头文件可能会被多次包含在一个源文件中 条件指示符可防止这种头文件的重复处理

~~~c++
#ifndef BOOKSTORE_H
#define BOOKSTORE_H
/* Bookstore.h 的内容 */
#endif
~~~

编译程序时可以使用-D 选项 并且在后面写上预处理器常量的名字 这样就能在命令行中定义预处理器常量

>  $ CC -DDEBUG main.C 

2

编译 C++程序时 编译器自动定义了一个预处理器名字__cplusplus

另外两个比较有用的预定义名字是 __LINE__和__FILE__

另外两个预定义名字分别包含当前被编译文件的编译时间 __TIME__ 和日期__DATE__ 

3

assert()是 C 语台标准库中提供的一个通用预处理器宏 在代码中常利用 assert()来判断一个必需的前提条件 以便程序能够正确执行  

4

cerr   cout

5

指针的主要用处是管理和操纵动态分配的内存 

~~~c++
int *p = new int(100);
int a = *p;
int *c = &a;
delete p;
delete c;
~~~

6

指针

~~~c++
	char *ch[3] = {
	"asdasd",
	"wewe",
	"wew"
	};
//char *ch[3]  指针类型char *[3]  指针所指向的类型char [3]
~~~

~~~c++
	int m[3] = { 1,2,3 };
	int (*p)[3] = &m;//数组指针   指向整个数组 int()[3]     m=>*p
	int *mm = m;

	int **pp=&mm;//二位指针，指向 这个数组的第一个元素的指针

	int qqq = sizeof(p);//指针就是一个数  size都是4
	int www = sizeof(pp);


	char *ch[3] = {//指针数组 char *(ch[3])
	"asdasd",
	"wewe",
	"wew"
	};
~~~

7

类定义中被定义的成员函数 如 size() 会被自动当作是内联函数

8

缺省构造函数声明中出现的关键字 explicit 

9

泛型

~~~c++
template<class tyep>
class Myclass
{
public:
	tyep number;
};

int main()
{
	Myclass<char> a;
	a.number = 'a';
	return 0;
}

~~~

10

命名空间

~~~c++
namespace MyNameSpace {
	template<class tyep>
	class Myclass
	{
	public:
		tyep number;
	};
}

int main()
{
	MyNameSpace::Myclass<char> a;
	a.number = 'a';
	return 0;
}
~~~

11

向量 and 算法

~~~c++
#include <vector>
#include <algorithm>
#include <iostream>
int ia[ 10 ] = {
51, 23, 7, 88, 41, 98, 12, 103, 37, 6 };
int main()
{
vector< int > vec( ia, ia+10 );
// 排序数组
sort( vec.begin(), vec.end() );
// 获取值
int search_value;
cin >> search_value;
// 搜索元素
vector<int>::iterator found;
found = find( vec.begin(), vec.end(), search_value );
if ( found != vec.end() )
cout << "search_value found!\n";
else cout << "search_value not found!\n";
// 反转数组
reverse( vec.begin(), vec.end() );
// ...
}
~~~

12、

宽字符

wchar_t ch = L'周';

13

int *pi = 0; 

// pi 被初始化为 "没有指向任何对象" 

~~~c++
	int a = 10;
	int *p = 0;
	int *pp = &a;

	bool pb = p;//false
	bool ppb = pp;//true
~~~

14

~~~c++
	char *a = "asdasd";
	while (true)
	{
		char b = *a;
		a++;
		if (b == '\0') {
			break;
		}
		
	}
~~~

结束符'\0'

15

~~~c++
int* const p = &a;
const int *pp = &a;

*p = 12;
	
pp = &b;
~~~

p是常量， *pp是常量

16

在实际的程序中 指向 const 的指针常被用作函数的形式参数 它作为一个约定来保证被传递给函数的实际对象在函数中不会被修改 