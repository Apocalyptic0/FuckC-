Fuck C++
1. <font color = pink>C++ Prime Plus</font>
2. 
3. 
4. 
5. 
6. 

## C++ Prime Plus
pages:678
date:2023/11/7
last update:2023/11/12 00:05 Full Combo!

*作为对前置基础的回顾，预计一周速通*

### 第一章 预备知识
* 与自顶向下的C相比，C++是自底向上的语言（p3）

<font color = red>Question:一个程序从创建到运行的全部过程 (this->p4)</font>

attention! 这是一个长期问题
编写
    - IDE 集成开发环境，现代IDE可以完成程序编写到运行的一切工作
    - 任何文本编辑器都可以完成程序的编写，then
        - 编译，链接    （GUN）
从文件到执行
    - 预处理：处理以#开头的编译指令
    - 编译：从高级语言到汇编语言，也就是《编译原理》里的内容
    - 汇编：从汇编语言到机器语言    这是一个容易逆转的过程，即为反汇编的原理
    - 链接：
    - 运行

总结为第一章经典废话

<font color = green>End of Chapter</font>

### 第二章 开始学习C++

头文件命名（p15）
C++新式风格 无扩展名
C的头文件   前缀c

iostream与iostream.h（p16）
后者没有引入命名空间，不用std，然而起码我的VS不能直接include<iostream.h>

\n与endl（p17）
endl会刷新缓冲区，过多的endl是影响程序效率低下的原因之一

C++程序的模块：函数（p30）

C++语句的6种类型（p30）
声明语句，赋值语句，消息语句，函数调用，函数原型，返回语句

<font color = green>End of Chapter</font>

### 第三章 处理数据

对变量名（p33）
以下划线开头的变量名被保留给实现，可能会与用户定义的变量名冲突

关于未初始化变量（p37）
如果不对函数内部定义的变量进行初始化，该变量的值是不确定的。这意味着该变量的值将是它被创建之前，相应内存单元保存的值

变量初始化方式（p37）
```C++
int a = 1;
int a(1);
int a = {1};
int a{1};
int a{};//0
```

cout输出hex，dec，oct（p40）
```C++
cout<<hex;//dont print anything, just change the mode of cout
```
tips:为什么dec表示10进制，oct表示8进制，与英文中月份的表示错开了2
英国历法本来只有十个月，后来在前面加了两个月，于是oct从8变成了今天的10月

总结为可以跳过的一章，重要的内容平时一直都在用

<font color = green>End of Chapter</font>

### 第四章 复合类型
```C++
struct Matrix4x4f {
	union {
		float data[4][4];
	};
};
//对这个structure的定义，哪一个是正确的
//A. 
Matrix4x4f identity = 	
			{ 1.0f, 0.0f, 0.0f, 0.0f },
			{ 0.0f, 1.0f, 0.0f, 0.0f },
			{ 0.0f, 0.0f, 1.0f, 0.0f },
			{ 0.0f, 0.0f, 0.0f, 1.0f }
			;
//B. 
Matrix4x4f identity = {
			{ 1.0f, 0.0f, 0.0f, 0.0f },
			{ 0.0f, 1.0f, 0.0f, 0.0f },
			{ 0.0f, 0.0f, 1.0f, 0.0f },
			{ 0.0f, 0.0f, 0.0f, 1.0f }
			};
//C. 
Matrix4x4f identity = { {
			{ 1.0f, 0.0f, 0.0f, 0.0f },
			{ 0.0f, 1.0f, 0.0f, 0.0f },
			{ 0.0f, 0.0f, 1.0f, 0.0f },
			{ 0.0f, 0.0f, 0.0f, 1.0f }
			} };
//D. 
Matrix4x4f identity = { { {
			{ 1.0f, 0.0f, 0.0f, 0.0f },
			{ 0.0f, 1.0f, 0.0f, 0.0f },
			{ 0.0f, 0.0f, 1.0f, 0.0f },
			{ 0.0f, 0.0f, 0.0f, 1.0f }
			} } };

```
数组的个数声明可以为常数，const常量或者常量表达式（sizeof），总的来说要求编译时确定，在有初始化时也可以为空，建议只在存储字符串时这样做，数组的初始化只能发生在声明的时候，也不能将一个数组赋值给另一个（p61），但可以将一个string赋值给另一个（p69）

数组列表初始化禁止缩窄变换，但允许一般的类型转换（p62）
```C++
char a[4]{'h', 'i', 1233456, 'b'}//not allowed
char a[4]{'h', 'i', 112}//allowed
```
sizeof与strlen（p64）
sizeof返回整个数组的长度，而strlen返回字符串长度且不包括\0
strlen == string.size() （p71）
```C++
char a[20] = "my length is 15";
strlen(a);//15
sizeof(a);//20

//attention: strlen与sizeof没有绝对的大小关系
char a[20];
//maybe strlen(a) > 20
//as for char c : a c!=\0
```
cout.getline(),cout.get()与cout拼接（p66）
getline与get都读取一行，参数为写入位置和size，区别在于getline会去掉输入流的\n而get不会
```C++
cin.getline(name, 20);
cin.getline(dessert, 20);

//等价
cin.get(name, 20);
cin.get();//无参数时表示读取一个字符，在这里是\n
cin.get(dessert, 20);
cin.get();

//拼接
cin.getline(name, 20).getline(dessert, 20);
//是的，这是理所当然的正确用法，但请注意执行顺序

//此外，name写入满也会导致函数返回，所以get更容易检查错误，通过get()可以确定函数返回原因，而getline在写入满时会设置失效位

//注意
//cin也不会读取\n
//solution:
cin>>year;
cin.get();
cin.getline(name, 20);

//读取string
getline(cin, str);
cin>>str;//also read a word;
```

字符串前缀（p72）
```C++
wchar_t title[] = L"csjalk cjsklaj";
char16_t name[] = u"sdjakldjklsa";
char32_t car[] = U"dsaklHdksjal";
//and raw string(原始字符串)
R"(jim, "kim", "\n")"//不执行转义
R"+*(now you can use ')' inside)+*"
```

位字段（p78）//可能一辈子用不到

匿名共用体（p78）//如果你对本章开头那个问题有疑问的话

枚举（p79）
1. 可以创建多个相同值的枚举量
2. 为枚举变量赋值只能是取值范围内的值
    - 事实是在我的VS上取值范围外也是可以的
3. 取值范围
    - 上限 max(2^n)-1                   101 -> 128-1
    - 下限 min > 0? 0: max(2^n)+1       -6 -> -8+1
    - just like 2^m|->---{min--0----enum------max}-----<-|2^n

tips：我在初学这个概念时，将枚举变量视为string，并且期望打印枚举变量的变量名，事实是变量名其实是服务编译器用户（程序员）的，在程序中根本没有所谓的变量名，所以打印变量名根本就是天方夜谭。枚举本质还是储存着整形变量的易于归类理解的一系列名称

空指针，野指针（p84）
空指针在C++是nullptr，值为0
何为野指针？
```C++
//what happened?
long *pos;
*pos = 223344;

//result: compile error: 使用了未初始化的变量pos
```
pos就是野指针，对于未初始的变量（参见第61行），值为该位置原来保存的值，也就是说此时的pos指向了一个未知的位置，有可能是虚拟内存的任何地方，如果对该位置赋值，程序会被破坏

new and delete（p84）
虽然这本书讲的不是很深，anyway，这是一个大坑，应该先熟悉这些基础知识

数组地址（p90）
```C++
int a[10];
a = &a[0]; //int ptr
&a; //int[10] ptr
//值相同但类型不同
```

数组和std::array都是栈静态分配，而std::vector是堆动态分配（p99）

一个小问题
```C++
char* p = "hhh";		//invalid
const char* p = "hhh";	//valid
char p[] = "hhh";		//valid
std::string p = "hhh";	//valid

//why?
//结合变量，常量在虚拟内存的表现进行思考
```

指针真是让人头晕的东西

<font color = green>End of Chapter</font>

### 第五章 循环和关系表达式

关于cin的返回值（p131）
cin总是在确保程序获取输入后尽可能返回cin，如果在返回的时候程序还没有获取到输入，就把输入返回

cin失败时发生了什么
```C++
int a = 0;
cin >> a;
cout << a;
cin >> a;
cout << a << " "<< bool(cin);

//input 5 a
//output 50 0
```
把0写入，cin变为false，设置失效位，后面的输入都无效

循环有什么难度，跳过跳过~

<font color = green>End of Chapter</font>

### 第六章 分支语句和逻辑运算符

呵呵

<font color = green>End of Chapter</font>

### 第七章 函数————C++的编程模块

为什么C++函数不能返回数组，但是可以返回结构体和对象（p168）
数组是C++的二等公民，无法通过值传递，而函数的返回就是值传递

void fun(int a[], int num);
void fun(int* a, int num);
这是唯一的int a[]和int* a有相同意义的地方，都表示&a[0]，sizeof(a) == sizeof(ptr)（p177）

二维数组的参数声明（p185）
```C++
int a[100][4];
sum(a, 100);
//a: a point to a array own 4 members, sizeof(a) = 16

int sum(int ar2[][4], int num);
int sum(int* ar2[4], int num);

```
<font color = green>End of Chapter</font>

### 第八章 函数探幽

指针和引用的区别（p211）
引用在声明时必须初始化
指针可以更换指向的变量，但引用不行

传递引用参数时不能传入表达式（p215）
但如果是const形参就可以
遇到不匹配的引用，函数会放弃引用而增加一个临时变量，这一举动会使对引用的更改无效，而const本就禁止这一行为

正确使用引用返回值（p220）
不要返回对已经消失变量的引用（函数中的临时变量），可以返回对引用参数的引用
如果不希望修改返回值的值，最好返回值声明为const

使用template<>来进行显示具体化（p234）
优先级：非模板函数>显示具体化>模板函数
显示实例化：template void Swap<int>(int &, int &);显示让程序自动生成定义

C++11关键字 decltype（p241）
对未知变量类型的定义 decltype(expression) var;
1. 和expression类型想同
2. 函数调用，var为返回值类型
在返回值使用
```C++
template<class T1, class T2>
auto gt(T1 x, T2 y) -> decltype(x + y)
{
	//...
	return x + y;
}
```
<font color = green>End of Chapter</font>

### 第九章 内存模型和名称空间

头文件常包含的内容（p247）
函数原型 符号常量 结构声明 类声明 模板声明 内联函数
不应该在头文件创建变量和定义函数，因为会导致多重定义

使用#ifdef管理头文件（p248）
当然现代IDE都有自己的方式使头文件只出现一次

关于static静态（p253）
C++中有三种变量存储方式，静态，动态和自动
静态：从声明开始一直在那里，如果没有初始化就会被赋值0，包括static和global，有内部链接性，外部链接性，无链接性三种
动态：通过new分配，delete删除，运行时在堆中动态分配删除的内存
自动：函数中的变量，在栈中分配，函数运行完后栈指针移动，但原位置的值不会被改变，这也是变量应该初始化后再使用的原因

作用域解析运算符(::)放在变量前面表示全局变量（p256）

volatile禁止优化修饰符的意义是为了适配外部硬件对内存的修改，防止被编译器优化掉
mutable表示类常量中可被修改的部分
const的链接性为局部的，这也是它可以被放到头文件的原因
（p260）

定位new函数（p266）
实质是在指定的内存位置写入，不是写入到堆中，因此delete无效

<font color = green>End of Chapter</font>

### 第十章 对象和类

C++的结构被提供和类相同的功能，唯一的区别是结构默认为public（p283）

在类中定义的函数会自动成为inline，当然也可以在类后面手动声明（p284）

为什么引用参数可以传入const char* 字符串（p289）
```C++
Stock::Stock(const string& company, long n, double pr);
Stock food = Stock("World, Cabbage", 250, 1.25);
```
-> row:292

在没有提供构造函数时，编译器会提供默认构造函数，但如果提供了构造函数，就要手动处理无参的情况（p290）

在类的成员函数后加const以保证函数不会修改成员变量（和参数无关），const类只能调用这样的函数（p295）

初始化类的方式（p296）
```C++
Stock a("123", 100, 1);
Stock a{"123", 100, 1};
Stock a = Stock("123", 100, 1);
Stock a = {"123", 100, 1};
Stock a = new Stock("123", 100, 1);
Stock a = new Stock{"123", 100, 1};

Bozo b = 32;//special form for one-argument constructors

//在C++中使用(){}等价，使用new在堆上动态分配空间，第三种方式创建临时变量后拷贝构造
```
<font color = red>如果构造函数使用了new，则必须提供使用delete的析构函数</font>

在类作用域中声明常数（p303）
* 使用枚举
* static
类枚举不能隐式转为整型，可以指定底层类型，要用::修饰

<font color = green>End of Chapter</font>

### 第十一章 使用类

<font color = red>Error</font>（p315）
在讨论操作符重载时，原书给出了这样一个例子
```C++
t4 = t1 + t2 + t3;//operator+
//原书里认为该式子等价于
t4 = t1.operator+(t2.operator+(t3));
//于是当年的我提出了这样一个问题并写在了旁边

//operator-?
t4 = t1 - t2 - t3;
t4 = t1.operator-(t2.operator-(t3));
//显然这不是合理的计算顺序

//原书里似乎也没提到操作符重载会不会更改原操作符的结合性，于是自己试试
```
一个简单的验证程序
```C++
#include <iostream>

class Cents
{
private:
    int m_cents;

public:
    Cents(int cents)
        : m_cents{ cents }
    {};

    Cents operator+(const Cents& a) const;
    int getCents() const { return m_cents; };
};

int main()
{
    Cents c1(6);
    Cents c2(8);
    Cents c3(7);
    Cents c4 = c1 + c2 + c3;
    std::cout << "result:" << c4.getCents() << std::endl;
    return 0;
}

Cents Cents::operator+(const Cents& a) const
{
    std::cout << m_cents << "+" << a.m_cents << std::endl;
    return Cents(m_cents + a.m_cents);
}

//运行结果
//6+8
//14+7
//result:21

//更直观的，这是换成operator-后的结果
//6-8
//-2-7
//result:-9
```
于是不言而喻，C++运算符重载不会改变原运算符的结合性
即：
```C++
t4 = t1 + t2 + t3;
//等价于
t4 = (t1.operator+(t2)).operator+(t3);
```

友元函数（p320）
在类中声明，前面加friend，不是成员函数，但可以访问类的私有变量，在定义时不要加friend和类名
如果要为类重载运算符，并将非类的项作为第一个操作数，可以用友元函数来反转操作数顺序。常见的用法是重载cout<<

在构造函数前使用explicit禁止隐式类型转换（p336）

使用转换函数定义类的转换，这是一个没有返回值但必须返回的函数（p338）
在矩阵类中很有用

<font color = green>End of Chapter</font>

### 第十二章 类和动态内存分配

带有类内初始项的成员必须为常量，不能在类的声明中初始化类的静态成员，const和enum例外，应该在类的声明之外用单独的初始化语句（p349）

拷贝构造函数（p354）
```C++
//在进行这样的操作时
//拷贝构造函数只用在初始化
Class T;
T a;
T b = a;//初始化
T c = T(a);//初始化
T d(a);
//调用拷贝构造函数
//如果没有定义，会使用默认拷贝构造函数，默认拷贝构造函数进行值传递，对所有的数组进行浅拷贝，但是对类的话会使用各自的拷贝函数
```

赋值构造函数（p356）
```C++
Class T;
T a;
T b;
b = a;

//赋值构造函数处理已经存在的对象
//对原来的数据要进行处理
//1. 释放之前分配的内存
//2. 检查是否赋值给自己，如果是直接返回
//3. 返回自己的引用
//example:
T& T::operator=(const T& t)
{
	if(this == &t)
		return *this;
	//释放之前分配的内存
	delete[] str;
	//...
	//深拷贝
	//do something
	return *this;

}
```

delete和delete[]都可以处理空指针nullptr，所以在默认构造函数中对指针赋值nullptr不会导致析构函数中delete出错（p364）

使用定位new函数在buffer上为对象分配空间时，和前面讲的一样，无法使用delete，只能对buffer进行delete[]，并且这样无法调用类的析构函数，因此需要手动调用，注意调用的顺序应该是后构造的对象先被析构（p373）
<font color = red>这是少有的需要手动析构的情况之一</font>

只有构造函数可以使用成员初始化列表，const和引用必须使用成员初始化列表，使用成员初始化列表效率更高（p379）

在不需要时手动把拷贝构造函数和赋值构造函数声明为private，以防止错误的使用（p382）

C++11可以在类内进行成员初始化，可以替代初始化列表中的const，但构造函数的初始化会将其覆盖，并且静态变量依然需要在外进行初始化（p388）

<font color = green>End of Chapter</font>

### 第十三章 类继承

派生类的构造函数应该使用成员初始化函数将基类信息传递给基类构造函数，派生类不能直接访问基类的私有成员，只能通过public，protect接口访问。对象声明时，先执行基类的构造函数（在初始化阶段执行），然后执行派生构造函数（在构造函数阶段执行），析构过程与之相反。如果没有使用基类构造函数，将使用默认的基类构造函数（p397）

基类指针和引用可以直接指向派生类，但只能使用基类的函数，这也是虚函数的基础（p399）
由此，可以将派生类赋值或者拷贝给基类，但只传递基类部分）

公有继承是is-a的关系，派生类可以使用基类的所有公有接口，但不能访问其私有变量（p400）

OOP的三大特性之一：多态，即基类和派生类可以定义一个函数的不同表现，实现的方式可以是重写和虚函数。非虚函数根据指针类型来选定，而虚函数则根据指向的类型来调用函数。采用继承的类，基类应该默认有一个虚析构函数，保证派生类虚构函数的正确调用，而不应该有虚构造函数出现（p401）

<font color = red>注意：使用普通的析构函数在delete的时候也会释放派生部分，但是如果析构函数有其他功能就必须使用虚析构函数（p409）</font>

为了进行动态联编（在运行时确定调用哪个函数），C++为定义虚函数的对象指定一个隐藏变量：虚函数表地址，每个类有自己的虚函数表，指向自己应该调用的虚函数。进行动态联编时，对象通过隐藏变量找到虚函数表，再定位到需要的函数（p412）

友元函数不能是虚函数，因为友元不是成员函数，但可以在友元中调用类的虚函数。
如果没有对虚函数重新定义，将会使用继承链中最近的那一个
如果试图对虚函数重载，他会覆盖掉其他基类的实现，如果基类定义了重载的多个虚函数，在继承类也要全部定义（p413）

protect 派生类中可以访问，但在类外面不能直接访问，对类数据成员使用protect，继承类会打破对数据成员的保护！protect成员应该是希望基类和派生类使用，但不希望外部访问的（p414）

抽象基类ABC 使用纯虚函数作为接口，派生到不同类，不能定义抽象基类的实例（p416）

如何在派生类的友元函数类调用基类的友元函数（p426）
使用强制类型转换转为基类

应该尽可能使用引用的几个理由（p428）
1. 在函数的参数或者返回值采用值传递，会进行临时变量的产生和销毁，多进行一次拷贝构造函数和析构函数
2. 使用引用可以调用对应派生类对象的虚函数


应该尽可能使用const的几个理由（p429）
1. 保证对本该不变的值的错误修改
2. 对成员函数的const声明使得const对象可以调用
3. 对char*的const声明使得可以直接复制引号括起来的字符串
4. 返回值为const可以避免意外的为返回值再赋值

<font color = blue>建议多看看p427 - p432</font>

<font color = green>End of Chapter</font>

### 第十四章 C++的代码重用

has-a关系中，派生类不能使用拥有类的接口，但可以在类中使用他们的实现（p438）

类成员初始化的顺序和初始化列表无关，按类中声明的顺序进行初始化，这在成员间有依赖时特别重要。在初始化列表结束以后，对象里的成员就应该有初始值。如果初始化列表里没有，则使用默认构造函数。因此如果在构造函数里进行初始化，实质是执行一次默认构造函数，一次赋值构造函数（p440）

has-a关系可以用私有成员对象来实现，这是一种直观地方式。此外使用私有继承也可以有相同的效果，但需要注意一些地方（p444）
1. 私有继承会隐藏基类的接口，只能在类里使用它的实现
2. 私有继承类的指针和引用无法隐式转换为基类（基类的接口失效，转换自然无意义了）
3. 对基类的访问，采用强制转换
4. 对基类的初始化，和公有继承一样，直接调用构造函数
5. 继承无法使用多个同类的对象，因为没有名称加以区分
6. 继承可以访问protect成员，并且可以使用虚函数，不过为什么私有继承需要使用虚函数呢？

protect继承，把公有和保护成员变成派生类的保护成员（p448）
使用using 基类函数名（无const，返回值，特征标）以在private派生类中使用基类的接口

<font color = pink>多重继承</font>（p449 - 462）
* 对每个类的继承要有自己的访问规则，如果没有默认为private
* 菱形继承，即派生类的两个基类有共同的基类，会导致基类出现两个。用这样的基类指针或引用指向派生类对象时会导致二义性（有两个基类地址可以定位）
	- 由此，引出了虚基类（虚拟继承），使用关键字virtual指定虚拟继承
	- 虚拟继承的基类在菱形继承的派生类中共享，并且，虚基类不在由中间类访问，而变成了派生类自己的成员，因此在初始化列表中要手动使用虚基类的构造函数，否则使用默认的虚基类构造函数
	- 派生类调用基类同名函数时，会优先调用最近层次的函数，这一规则与访问规则无关，即使该函数为private无法访问，还是会尝试调用它而导致访问错误
	- 试图访问同一层次中间类的共同函数会导致二义性，好的做法是在每个类中用另一个函数定义自己独有的部分，然后在函数中调用需要的基类的部分

<font color = pink>类模板</font>（p462 - 482）
* 谨慎使用指针实例化模板类，注意指针不能像一般变量那样直接深拷贝
* 模板类可以有非类型参数，这样的参数只能为整形，指针，引用，枚举
* 模板具体化
	- 隐式实例化：在需要对象时生成
	```C++
	Array<double 30>* pt;//只是一个指针
	pt = new Array<double, 30>;//在这里才进行隐式实例化
	``` 
	- 显式实例化：手动声明需要的实例化
	- 显式具体化：使用template<>，对需要特殊处理的类型具体化实现
	- 部分具体化：对多个模板参数的部分具体化
* 可以在成员中使用模板，可以将模板用于模板参数
* 模板函数有一定的推导能力，可以根据给定的参数推导模板类型参数
* 模板类和友元
	- 非模板友元：如果要为友元提供模板类参数，则提供需要的显式具体化
	- 约束模板友元：即希望友元的类型和类的实例一致，在类的前面声明友元函数，再在类中用类的模板参数进行实例化
	- 非约束模板友元：友元函数的类型和类本身无关，采用不同的参数名即可，模板函数可以自己推导实现

using可以完全替代typedef，在非模板类型中它们等价，但using可以使用模板提供一系列别名（p482）
```C++
template<typename T>
	using arrtype = std::array<T, 12>;

arrtype<int> days;

typedef array<int, 12> arrint;
typedef array<double, 12> arrdou;
//...
```

<font color = green>End of Chapter</font>

### 第十五章 友元、异常和其他
友元（p488-495）
使用友元类来在不绑定基类的情况下访问类的成员
也可以使用友元成员函数，但要使用前向声明在定义前声明友元所在的类，如果函数对类有依赖，应该在类声明之后定义
两个类可以互相成为朋友，也可以拥有共同的朋友

C++的friend指的是：“我有一个朋友”，而不是“我是谁的朋友”，前者指“我愿意friend使用我的东西”，后者指“我希望使用friend的东西”，friend成立的前提是类自己承认，所以friend并不会违背OOP的原则，相反它给予了更灵活的控制

嵌套类（p495-499）
为什么要使用嵌套类，嵌套类和继承有什么区别
嵌套类并不在类中创建变量，只是在类中进行声明。在嵌套类中采用public，但创建嵌套类的private变量，可以使类能随意访问嵌套类的成员，而类外无法访问。
嵌套类同样可以结合模板使用

使用abort函数直接退出程序，并且显示程序终止信息，这也是默认触发异常的情况（p500）

try, throw and catch（p502）
try：执行程序
throw：定位包含try块的函数，把错误信息（类或字符串）传给对应catch，终止函数，通过栈解构跳转到catch，此过程会结束整个try过程并且对中间的对象变量析构，如果没有找到catch，则直接终止程序。错误信息会自动生成一个副本，即使catch中参数是引用
catch：处理异常，将参数声明为引用有利于调用虚函数

try,throw<->switch
catch<->case//应该把派生类放前面，基类放后面
catch(...)<->default

类型转换运算符（p526）
* dynamic_cast：安全的转换，只允许在类层次上进行向上转换
* const_cast：只消除相同类型的const
* static_cast：比起dynamic_cast允许类向下转换
* reinterpret_cast：为底层准备的低限制转换，不能更改const

<font color = green>End of Chapter</font>

### 第十六章 string类和标准模板库

string类的构造函数（p531）
string是C++常用的类，为字符串提供了自动分配大小，连接，比较，查找，访问等功能，string也是一个模板类，并且C++定义了四个大小不同的具体化

包含memory库以使用智能指针，智能指针只能用于new分配的堆内存指针，不能用于非堆的地方（p541）

auto_ptr和unique_ptr（p544）
二者表明指向的对象只能被一个指针所有，不能被两个指针共同指向，但auto允许使用直接转换所有权
```C++
auto_ptr<string> p1(new string "hhh");
auto_ptr<string> p2;
p2 = p1; // ok
cout << p1;//error
//此时，hhh的所有权转移给p2，p1成为悬挂指针，指向0，试图使用p1将引发异常

unique_ptr<string> pu1(new string "jkl");
unique_ptr<string> pu2;
pu2 = pu1; // not allowed
//新的unique指针禁止了这种转换，而采用更安全的移动语义
pu2 = move(pu1); // allowed
//同时unique允许合理的转换，如果源unique_ptr是临时右值，就允许转换
unique_ptr<string> demo(const char* s)
{
	unique_ptr<string> temp(new string(s));
	return temp; // temporary value
}
unique_ptr<string> pfu1 = demo("hh");// ok

//此外，如果希望把unique_ptr作为函数参数，记得用引用
//如果使用不引用的auto_ptr会出现严重错误，为什么？
```

for_each使用的函数不能更改容器的值（p550）

C++的前缀++和后缀++（p555）
```C++
// C++把operator++()作为前缀， operator++(int)作为后缀
// 以迭代器为例
iterator& operator++()
{
	pt = pt->next;
	return *this;
}

iterator operator++(int)
{
	iterator temp = *this;
	pt = pt->next;
	return temp;
}
```

C++定义了五种迭代器，呈一定层次结构，目的在于尽可能使用最低层次的迭代器（p557）
输入迭代器，输出迭代器 -> 正向迭代器 -> 双向迭代器 -> 随机访问迭代器

在类中重载operator()以生成一个函数对象，for_each函数的第三个参数可以传入普通的函数，也可以传入函数对象（p572）

引用头文件functional以使用预定义函数符，如plus<double>()（p575）

使用适配器bind1st(),bind2nd()将二元函数转为一元，如bind1s(multplies<double>(), 2.5)

stl的功能非常丰富，对他能做什么留个印象，如果需要的话查一下就好了，而且感觉很多功能其实还是自己写清晰易懂的实现比较好

<font color = green>End of Chapter</font>

### 第十七章 输入、输出和文件

```C++
fstream finout;// file streams
finout.open{filename, ios_base::in | ios_base::out | ios_base::binary ...};
finout.is_open();// 判断是否打开文件

//使用结构读取
finout.read((char*)&pl, sizeof(pl));
finout.write((char*) &pl, sizeof(pl));

//文件流指针移动
finout.seekg();//输入文件指针
finout.seekp();//输出文件指针
```

内核格式化sstream，对字符串采用输入输出流（p638）

输入输出流使C++对文件和终端的访问拥有类似于缓存的方式，磁盘和流通过数据块进行交互，流和程序通过字节传输

<font color = green>End of Chapter</font>

### 第十八章 探讨C++新标准

为什么应该使用nullptr而不是NULL或者0（p646）
nullptr被禁止传递给整型参数，而0可以

右值引用能够为右值提供身份，将它储存在某个位置，并且可以访问其地址（649）
右值引用服务于移动语义，声明以右值引用为参数的类似拷贝或赋值的构造函数以定义移动语义，移动语义消除了创建临时变量，使用临时变量，析构临时变量的过程，直接交换所有权。
使用std::move()强行转换左值为右值，拒绝赋值构造，使用移动语义（赋值是希望生成两个一样的对象，如果只是想交换所有权，大可以直接移动）

类会在没有且需要的时候提供默认的特殊成员函数，它们包括：构造析构，拷贝赋值，移动，构造函数不会初始化内置类型，但会对类成员调用它们自己的默认构造函数。如果声明了左值右值之一，另一类不会提供默认的函数（p658）

虚函数声明 = 0;//纯虚函数
特殊成员函数 = default;//显示使用默认函数
特殊成员函数或想要禁止的类型转换 = delete;//禁止使用

委托构造函数：在初始化列表使用已定义的构造函数，就像派生类的构造函数一样
继承构造函数：使用using继承基类的函数

在虚函数参数列表后：（p661）
override 覆盖虚函数在基类的实现（如果再使用基类实现会编译错误）
final 禁止派生类重新定义

使用函数对象的三个方法（p662）
1. 普通函数指针
2. 函数符
	- 在类中重定义operator()
	- 类的对象是一个函数
	- 构造函数本身也可以用作函数对象
3. lambda函数
	- [捕获 =变量：按值访问变量 |&变量：按引用访问变量 |=/&：按值/引用访问所有其他变量]
	- (参数)
	- -> 返回类型 如果函数内容是单个return语句可以省略
	- {函数内容}
	- 可以使用auto name = lambda 为lambda函数绑定名称

使用适配器为函数提供更统一合适的接口，减少模版生成次数（p666）

可变参数模版，同时处理一堆不同的参数类型（p669）
如果有一天我用到这个功能我会来把这里补全的