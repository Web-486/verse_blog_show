---
date : '2025-07-21T11:14:48+08:00'
draft : true
title : '面向对象程序设计'
categories:
    - Test
    - 测试
tags:
    - 中文
    - C++
---
# 面向对象程序设计：复习提纲

## C++的初步知识

### 函数



#### C++程序由函数驱动，主函数(main函数)、普通函数（功能函数）、主调函数、被调函数等概念及其关系；

* 每个 C++ 程序都有且只有一个 main函数，程序运行从main函数开始到main函数结束，main函数只能是主调函数
* 若函数 f1() 调用函数 f2(), 则称 f1()为主调函数 ,  f2()为被调函数

#### 函数的定义、调用、声明（原型）的写法；理解函数调用机制；

* 被调函数出现在主调函数之后时 需进行函数声明

#### 理解函数间数据联系的渠道（参数、返回值、全局变量）

* 全局变量可以被函数体直接访问，参数只能在函数体中访问，返回值是函数体返回的结果

#### C++特有函数

##### inline 内联函数的思想

* 通过关键字 **inline** 将一个函数声明成内联函数后，编译器会将该函数的调用处理成**编译前的代码替换**而不是像普通函数在**编译时的控制转移**从而提高了效率。
* 不会再开空间生成？inline不是一定展开，只是给编译器建议，具体是否展开由编译器展开，递归函数不能展开

##### 重载的概念、分类、区分依据、解析次序（结合第 4 章）

* 概念：在不同类型上做类似运算而又用相同名字的情况称为重载，即重新定义语义。
* 分类：函数重载，运算符重载，构造函数重载（注意函数重载必须在一个同一个域）
* 区分依据：参数个数，类型，顺序三者种必须至少有一种不同（**返回类型不能单独作为重载解析的依据** ）
* 解析次序：

​	（1）寻找一个严格的匹配

​	（2）通过内部转换寻求一个匹配

​	（3）通过用户定义的转换寻求一个匹配

```C++
void print(int);
void print(double);
int main(void){
    print(1);	//int
    print(1.0);	//double
    print('a');	//int
    printf(3.1415f);	//double
}
```

##### 带参数默认值的函数的写法，默认参数的定义次序

* 写法：void func(int a, int b =2, int c =3, int d =4);

* 声明：**既有声明又有定义时 定义中可省略默认参数**，只有定义时 默认参数须出现在定义中

* 定义次序：严格遵守默认参数从右向左依次定义，并且调用函数时是从左向右匹配参数的

  ```C++
  void func(int a = 1, int b, int c = 3, int d = 4);	//error:默认参数必须从右向左连续定义，否则会引起调用歧义。
  ```

##### 模板的概念、分类，函数模板的写法，类模板的写法（结合第 3 章）

* 函数模板：建立一个通用函数，其函数类型和形参类型不具体指定 用一个**虚拟类型**来代表这个**通用函数**就称为函数模板

```C++
template <typename T>	//模板声明，其中T为类型参数
T max(T a, T b, T c){	//定义一个通用函数，用T作虚拟的类型名
    if(b > a) a = b;
    if(c > a) a = c;
    return a;
}
```

### 标准名字空间的用法(using namespace std)

* 如果使用了命名空间 std，则在使用 #include 编译预处理命令包含头文件时， **必须去掉头文件的扩展名 .h**。

### 输入输出

####  C 语言中常用输入输出函数的用法(getchar、putchar、gets、puts、scanf、printf)

* getchar/putchar函数（字符输入/输出函数）

```C++
c=getchar( ) ); putchar(c+32); n’);	//输入A，则输出a（ASCII码）
```

* gets/puts函数 （）

```C++
//gets函数目前已废弃
puts("Hello World");// 自动在结尾添加换行,且无法像printf一样格式化输出(即使用%d一类)
```

* scanf/printf函数（）

```C++
scanf("%d,%d",&num1,&num2);	//输入: 1,2
printf("%d %d",num1,num2);	//输出: 1 2
```

#### 标准输入输出流类 iostream，标准输入流对象 cin、标准输出流对象 cout、流插入运 算符<<、流提取运算符>>的基本概念及用法；输入输出流中常用控制符的使用

* <p style="color:red;">大题</p>

* 使用setw()前记得导入 <iomanip> 头文件

![image-20250604175801350](./../Pictures/typora/image-20250604175801350.png)

```C++
//eg1：控制浮点数值显示
#include <iostream>  // 包含输入输出流库
#include <iomanip>   // 包含输入输出格式化操作库（用于setprecision等控制符）
using namespace std;  // 使用标准命名空间

int main() {
    double amount = 22.0 / 7;// 计算22除以7的浮点数结果（约等于π）
    
    // 默认输出（保留6位有效数字）
    cout << amount << endl;  // 输出：3.14286
    // 设置精度为0（实际会显示整数部分）
    cout << setprecision(0) << amount << endl;  // 输出：3
    // 设置精度为1（总有效数字位数）
    cout << setprecision(1) << amount << endl;  // 输出：3
    // 设置精度为2
    cout << setprecision(2) << amount << endl;  // 输出：3.1
    // 设置精度为3
    cout << setprecision(3) << amount << endl;  // 输出：3.14
    // 启用固定小数格式（影响后续所有输出）
    cout << setiosflags(ios::fixed);
    // 设置小数位数为8（fixed模式下）
    cout << setprecision(8) << amount << endl;  // 输出：3.14285714
    // 启用科学计数法格式（覆盖fixed标志）
    cout << setiosflags(ios::scientific) << amount << endl;//输出:3.14285714e+00
    // 恢复默认精度设置（6位有效数字）
    cout << setprecision(6);  // 影响后续输出
    
    return 0;  // 程序正常结束
}
```

```C++
//eg2：使用填充字符
#include <iostream>  // 包含输入输出流库
#include <iomanip>   // 包含输入输出格式化操作库（用于setw, setfill等控制符）
using namespace std;  // 使用标准命名空间

int main() {
    // 设置填充字符为'*'（影响后续所有使用setw的输出）
    cout << setfill('*');
    // 设置字段宽度为2，输出21（宽度不足时用'*'填充左侧）
    cout << setw(2) << 21 << endl;  // 输出：21（实际宽度=2，无需填充）
    // 设置字段宽度为3，输出21（左侧填充1个'*'）
    cout << setw(3) << 21 << endl;  // 输出：*21
    // 设置字段宽度为4，输出21（左侧填充2个'*'）
    cout << setw(4) << 21 << endl;  // 输出：**21
    // 尝试将填充字符设置为空格，恢复默认设置
    cout << setfill(' '); 
    
    return 0;  
}
```

### const 定义常变量，必须初始化

* eg: const int pi=3.1415926;

###  引用与指针

#### 引用的概念、声明方法（必须初始化、引用常量）、使用方法、 用 const 修饰引用（常量引用常量）

* 引用是个**别名**，引用不是值，不占存储空间；引用声明即定义；引用在声明时**必须初始化**；
* 引用一旦初始化，它就维系在一定的目标上，再也不分开，即**引用常量**；
* 只有某一确定类型的变量或对象，才能被引用。
* 使用方法：

​	（1）传递引用（双向传递）**（大题）**：传递引用和传递指针的效果是一样的，**传递的是原来的变量或对象，而不是在函数作用域内建立副本**

```C++
void swap(int & x,int & y){
    int temp = x;
    x = y,y = temp;
}
//...
swap(x,y);	//有效交换x和y的值（注意此处无&号）
```

​	（2）返回引用：返回引用使得一个函数调用表达式成为左值表达式

```C++
//计算A类学生和B类学生的人数
level(array[i], gradesize, typeA, typeB)++;//函数调用作为左值，直接作增量操作
//...
int& level(int grade[], int size,int & tA , int& tB){
    //...
    if(sum>=80) return tA;	//返回A类学生
    else return tB;	//返回B类学生
}
```

* const修饰引用：传递指针和引用存在传值所没有的潜在危险，故必要时用 const 加以修饰。

* > 注意传递**常量的引用**并不是**引用常量**，一般的引用就是引用常量，而这里是**常量的引用**，即**常量引用常量**。简单来说就是const double &p 和普通常量的性质一样，不能修改值。

#### 用 const 修饰指针（常量指针、指针常量、常量指针常量）

* <p style="color:red;">小题</p>

* > 简单辨别：只看const和*的位置， * 在const后面就是常指针，int* const p就是指针常量 

* 常量指针：指针指向的值是常量（不能通过指针修改变量（常量）的值，但指针本身可变（可以重新指向其他地址），称为"指向常量的指针"；

```c++
// 声明一个整型变量a并初始化为3
int a = 3;
// 声明一个指向常量整数的指针p（底层const）
// 特点：不能通过p修改指向的值，但指针本身可以重新指向其他地址
const int *p = &a;  // p指向a的地址（也可以写成int const *p ）
    
// 直接修改变量a的值（允许，因为a不是常量）
a = 5;
// 输出变量a的值（输出5）
cout << a << endl;
// 输出指针p指向的值（输出5，因为p指向a）
cout << *p << endl;
// 试图通过指针p修改指向的值（编译错误）
// 错误原因：p被声明为指向const int的指针，不能通过它修改值
// 即使a本身不是const，通过p访问时也视为常量
//*p = 5; 

// 注意：以下操作是允许的（修改指针指向）
int b = 10;
p = &b;  // p可以重新指向b的地址
```

* 指针常量：即指针是常量，**必须初始化（但是devC++中不初始化也可运行）**；

```C++
int* const p = &a;  // 指针本身是常量（不能改变指向）
*p = 10;             // 但可以通过指针修改值（允许）
//p = &b; //ERROR
```

* 常量指针常量：指向指针的指针常量，简单理解为二者叠加版，同样**必须初始化**。

```C++
const int* const p = &a;
//*p = 5; //error
//p = &b; //error
```

#### 理解用引用代替指针的好处

* 传递指针给用户增加了编程的理解和负担，而传递引用则无此麻烦。

### 作用域与生命期

#### 作用域（五种）、可见性、::运算符的两种用法、支配（覆盖）规则

* 五种作用域：局部作用域，函数作用域，函数原型作用域，文件作用域，类作用域
* 局部作用域：当标识符的声明出现在由一对花括号括起来的一段程序(块)内时 该标识符的作用域从声明点开始，到块结束处为止;

![image-20250604190628030](./../Pictures/typora/image-20250604190628030.png)

* 函数作用域：和标号有关，不常用；
* 函数原型作用域：函数原型声明中所作的参数声明在此作用域中，该作用域开始于函数原型声明的左括号，结束于右括号。如int MAX(int a,int b)**；**中参数a，b在离开**；**后作用域就不存在了，所以可写成int MAX(int,int)；
* 文件作用域：也称全局作用域，是在所有函数定义之外说明的，其作用域从说明点开始**,**一直延伸到源文件结束。注意：在头文件的文件作用域中所进行的声明，一旦该头文件被某个源文件嵌入(即包含)，则声明的作用域也扩展到该源文件中，直到该源文件结束，例如#include <iostream> 后可以调用cin和cout；
* 类作用域：指类定义内部形成的独立作用域，它封装了类的成员（数据成员和成员函数），使得这些成员在类外部不可直接访问，需要通过类名或对象名进行访问。
* 可见性？作用域描述的是标识符的有效范围 而可见性描述的是标识符在某一位置的有效性 所以从本质上讲作用域与可见性是一致的。

```C++
#include <iostream>
using namespace std;
int id = 3;
int main() {
	int id = 5;
	{
		int id = 7;
		cout << id << endl;//输出7 
	}
	cout << id << endl;//输出5 
	// :: 全局访问运算符 
	cout << ::id << endl;//输出3
	
	// :: 还可以作为 作用域运算符，如Tdate::month 
}
```

#### 生命期、理解静态局部变量、静态全局变量

* 三种生命期：静态生命期（代码区+数据区），局部生命期（栈区），动态生命期（堆区）

##### 静态生命期

* 与程序的运行期相同，一旦程序开始运行，这种生命期的变量就存在，当程序结束时，其生命期就结束；
* 全局变量，静态全局变量，**静态局部变量**，函数都具有静态生命期，驻留在内存的全局数据
  区或代码区；

##### 局部生命期：

* 在函数内部声明的变量或者是块中声明的变量，具有局部生命期。该生命期起始于声明点，结束于作用域结束处；

* > 具有局部生命期的变量肯定具有局部作用域，若为静态局部变量则具有静态生命期；

##### 动态生命期

* 这种生命期由程序中特定的函数调用(malloc()和free())或操作符 (new 和 delete) 来创建和释放；
* 当用函数malloc()或操作符new为变量分配空间时，生命期开始；当用函数free()或操作符delete释放该变量的空间或程序结束时，生命期结束；
* 具有动态生命期的变量驻留在内存的堆区中；

#### new 和 delete 对堆区操作的基本用法

```C++
#include <iostream>
using namespace std;

int main() {
	
    int* p;
	p = new int;
	*p = 10;
	cout << *p << endl;	//输出：10
	delete p;
	//动态数组
	p = new int[10];
	for(int i = 0; i < 10; i++){
		p[i] = i+1;
	}
	for(int i = 0; i < 10; i++){
		cout << p[i] << " ";
	}
    //输出：1 2 3 4 5 6 7 8 9 10
	delete[] p;
}
```

### string 类、字符串对象的概念（区分 cstring、string.h 和 string）

* cstring：C语言风格字符串处理；
* string.h：C++对C语言字符串的封装；
* string类：C++的字符串类，每一个字符串变量都是 string 类的一个对象；

```C++
#include <iostream>
#include <string>  // 必须包含 string 头文件
using namespace std;
int main() {

	string greeting = "Hello, World!";  // 直接初始化
	string name("Alice");              // 构造函数初始化
	string emptyStr;                   // 默认构造（空字符串）
	
	name += " Smith";                       // 使用 += 操作符
	string fullGreeting = greeting + " My name is " + name;  // 使用 + 操作符

	cout << "字符串内容: " << fullGreeting <<  endl;
	cout << "字符串长度: " << fullGreeting.length() <<  endl;  // 或 size()
	cout << "是否为空: " << (emptyStr.empty() ? "是" : "否") <<  endl;
	
	return 0;
/*	输出结果：
	字符串内容: Hello, World! My name is Alice Smith
	字符串长度: 36
	是否为空: 是
*/
}
```

### C++程序的上机步骤

* 编辑 cpp、编译 obj、连接 exe、运行；

## 类和对象

### 面向对象程序设计的三大特点：封装、继承和多态性

* 封装：通过类这种抽象数据类型把数据集和定义在该数据集之上的操作封装成为一体；
* 继承：允许子类共享父类的数据和操作的机制；
* 多态：让每个对象都有独特的表现方式： 重载、虚函数、子类型化；

### 理解用 class 和 struct 声明类的异同

*  C++ 的类，既能包含数据成员，又能包含成员函数，而C语言只能把相关的不同数据组合一个统一体，不能有函数在内；

### 类中的两种成员，三种访问权限控制符的区别

* 三种访问权限控制符：公有public，保护protected，私有private；

  公有权限（public）。被赋予公有权限的类成员是开放的，称为公有成员；

  私有权限（private）。被赋予私有权限的类成员将被隐藏，称为私有成员；

  保护权限（protected）。被赋予保护权限的类成员是半开放的，称为保护成员；

* 半开放？体现在**保护成员可以背派生类的成员函数访问**，而私有则不行；

![image-20250609164334118](./../Pictures/typora/image-20250609164334118.png)

* 两种成员：数据和函数，分别称为**数据成员**和**成员函数**

  | **场景**            | 数据成员                      | 成员函数                         |
  | :------------------ | :---------------------------- | :------------------------------- |
  | **内存分配**        | 占用对象内存空间              | 不占用对象内存（代码段共享）     |
  | **`const`对象访问** | 不能修改（除非`mutable`）     | 只能调用`const`成员函数          |
  | **`static`修饰**    | 所有对象共享同一份数据        | 无`this`指针，不能访问非静态成员 |
  | **生命周期**        | 与对象生命周期相同            | 在调用期间存在                   |
  | **访问方式**        | `obj.member` 或 `ptr->member` | `obj.func()` 或 `ptr->func()`    |

### 类的声明和成员函数定义的规范写法

```C++
#include <iostream>
using namespace std;

class Tdate {
	public:
		void Set(int,int,int); // 成员函数声明
		int IsLeapYear();
		void Print();
	private:
		int month;
		int day;
		int year;
};

void Tdate::Set (int m,int d,int y) {
	month=m;
	day=d;
	year=y;
}

int Tdate::IsLeapYear() {
	return (year%4==0&&year%100!=0)||(year%400== 0);
}

void Tdate::Print() {
	cout <<month <<"/" <<day <<"/" <<year <<endl;
}

int main() {
	Tdate obj;
	obj.Set(2025,6,5);
	obj.Print();	//输出：2025/6/5
	cout << obj.IsLeapYear();	//输出：0

	return 0;
}
```

### 对象的存储结构

* 对象=数据+操作代码

### this 指针的概念及用法

* <p style="color:red;">简答</p>

* this 指针是一个隐含于每个非静态成员函数中的特殊指针，用来指向不同的对象，从而在调用不同对象的成员函数时，不同的对象使用的是同一个函数代码段，还能够分别对不同对象中的数据进行操作。（一定要理解，运算符重载中重载双目运算符时成员函数相较于普通函数可以少一个对象参数就是因为成员函数有this指针）

```C++
class MyClass {
    int x;
    void foo() {
        x = 10; // 等价于 this->x = 10;
    }
};
```

## 关于类和对象的进一步讨论

### 类中的四个特殊成员函数（大题、小题）

#### 构造函数

##### 概念、作用、声明及定义方法（成员初始化列表）、调用时机

* 概念：以类名作为函数名的成员函数称为类的构造函数;
* 作用：创建对象，完成对象的初始化工作；
* 声明及定义方法：

```C++
//声明构造函数原型的一般形式：
Student(int sid, string sname, double sscore);

//定义构造函数原型的一般形式：
Student(int sid, string sname, double sscore){
    id = sid, name = sname, score = sscore;
}

//法二 成员初始化列表（多用于继承和聚集类，且只能用于构造函数）：
Student(int a, string b, double c): id(a),name(b),score(c){};
//如果在类内声明，类外定义，则声明时不应包括成员初始化列表
```

* > 调用时机：对象创建时自动调用，即执行一个对象声明语句或者用操作符new创建对象时

##### 特点

> 无参构造函数（缺省构造函数）、带参构造函数、构造函数重载、构造函数可带参数默认值、无名、无返回类型

```C++
Box( ); //声明一个无参的构造函数
Box(int h=1,int w=2,int len=3):height(h),width(w),length(len){
//声明一个有参构造函数，并对Box()函数重载，用参数的初始化列表对数据成员初始化
```

### 析构函数

#### 概念、作用、声明及定义方法、调用时机

* 概念：以波浪号~为首字符，后面跟类名构成的名字为函数名的成员函数称为类的析构函数；
* 作用：销毁对象，完成对象的清除工作；
* 声明及定义方法：

```C++
//声明的一般形式：
~Student();
//定义的一般形式：
~Student(){
    cout << "Destructor called." << endl;//Student类内没有动态分配操作,无需delete
}
```

* > 调用时机：对象生命周期结束时自动执行

#### 特点

> 无名、无参、无返回类型

#### 执行次序

> 栈式管理（与构造函数严格相反）

###  拷贝构造函数

#### 概念、作用、声明及定义方法、调用时机

* 作用：初始化一个新对象为另一个同类型对象的副本;
* 声明及定义方法：

```C++
MyClass(const MyClass& other);	//类内声明，const可以省略，但一般加上，因为不写就无法接受 const 实参，不能用 const 对象来初始化新对象
MyClass::MyClass(const MyClass& other) {	//类外定义
   	//...
}
```

* > 调用时机：显式初始化，函数参数传递，函数返回值；

```C++
MyClass obj1;		 // 调用构造函数
MyClass obj2 = obj1;  // 调用拷贝构造函数（显式初始化）
MyClass obj3(obj1);   // 调用拷贝构造函数（显式初始化）

void func(MyClass temp); // 函数声明
func(obj);  // 调用拷贝构造函数创建temp（函数参数传递）

MyClass create() {
    MyClass local;
    return local;  // 调用拷贝构造函数（函数返回值）
}
```

#### 特点：

> 无名、有参、无返回类型

#### ~~缺省拷贝构造函数、深拷贝与浅拷贝~~

### 拷贝赋值操作

#### 概念、作用、声明及定义方法、调用时机（区别于拷贝构造函数）

* 作用：实现两个已存在对象之间的赋值操作
* 声明及定义方法：

```C++
MyClass& operator=(MyClass& other);	//类内声明
MyClass& MyClass::operator=(MyClass& other) {	//类外定义
	//...
    return *this;
}
```

* > 调用时机：显式赋值操作，链式赋值；

```C++
MyClass obj1, obj2,obj1;	 //调用构造函数
obj1 = obj2;  			    // 调用拷贝赋值操作符（显式赋值操作）（注意与Myclass obj1 = obj2区分，这是初始化，调用拷贝构造函数）
obj3 = obj2 = obj1;  		// 两次调用拷贝赋值操作符（链式赋值）
```

#### 特点

> 有名、有参、有返回值

#### 缺省拷贝赋值操作、~~深拷贝与浅拷贝~~

```C++
// 缺省行为：浅拷贝（逐成员复制）
MyClass& MyClass::operator=(const MyClass& other) {
    if (this != &other) { // 防止自赋值
        // 复制非静态成员（若成员为指针，仅复制地址！）
        data = other.data; // 需深拷贝时需手动重写
    }
    return *this;
}
```

### 对象数组的概念（会导致多次调用该类的构造函数）

```C++
//...
Box a[3] = Box(10,12,15),Box(15,18,20),Box(16,20,26);
for(int i = 0; i < 3; i++){
    cout << a[i].volume << " ";	//输出：1800 5400 8320
}
```

### 对象指针的概念（不会导致调用该类的构造函数）、大小（4byte/8byte，取决于电脑系统）

```C++
//...
Box obj;
Box *pt = &obj;	//pt是指向Box类对象的指针变量，它指向对象obj
cout << (*pt).volume << pt->volume;	//访问方式2种
```

### const 修饰对象或成员（常对象、常量数据成员、常量成员函数 )的概念、用法； 理解数据保护

* <p style="color:red;">简答</p>要会写代码，掌握基本用法

```C++
//常对象：可以保证其数据成员不被改变，并且常对象必须要有初值
Time const t1(12,34,46);	//t1是常对象，也可以写成const Time t1(12,34,46);
//常对象不能调用该常对象的非const型的成员函数，以避免其修改常对象中数据成员的值

//常对象成员：常量数据成员，常量成员函数
Time::Time(int h,int m,int s):hour(h),minute(m),second(s){};
void get_time() const{
    //...
};	//注意const的位置在函数名和括号之后
/*  常数据成员只能通过构造函数的参数初始化表对常数据成员进行初始化
    常对象的数据成员都是常数据成员
    不同对象中常数据成员的值可以互不相同
	
    常成员函数：常成员函数只能引用本类中的数据成员，而不能修改他们
    在声明函数和定义函数时都要有const关键字，在调用时不必加const
*/
```

| 数据成员类型             | 非 const 成员函数         | const 成员函数          |
| :----------------------- | :------------------------ | :---------------------- |
| **非 const 数据成员**    | 可以引用 也可以改变值     | 可以引用 但不可以改变值 |
| **const 数据成员**       | 可以引用 但不可以改变值   | 可以引用 但不可以改变值 |
| **const 对象的数据成员** | 不允许引用 也不允许改变值 | 可以引用 但不可以改变值 |

| **`const Time t1;`** **`Time const t1;`** | `t1` 是常对象，其数据成员在任何情况下都不能被修改            |
| ----------------------------------------- | ------------------------------------------------------------ |
| **`void Time::fun() const`**              | `fun` 是 `Time` 类中的常成员函数，可以引用但不能修改本类的数据成员 |
| **`Time \* const p;`**                    | `p` 是指向 `Time` 类对象的常指针，`p` 的值（即指针的指向）不能改变 |
| **`const Time \*p;`**                     | `p` 是指向 `Time` 类常对象的指针，其指向的对象的值不能通过指针修改 |
| **`Time &t1 = t;`**                       | `t1` 是 `Time` 类对象 `t` 的引用，二者指向同一内存空间       |

### static 修饰成员（静态数据成员、静态成员函数）的概念、用法

* 静态数据成员

  1. 它不属于某一个对象，在所有对象之外单独开辟空间；

2. 在程序编译前被分配空间，到程序结束时才释放空间；
  3. 只能在类体外进行初始化；
4. 既可以通过对象名引用看，也可以通过类名来引用；

```C++
#include <iostream>
using namespace std;

class Box {
	public:
		static int height;
		int width;
		int length;
		Box(int w,int l):width(w),length(l) {

		};
		void printVolume() {
			cout << "Volume:" << height * width * length << endl;
		}
};
int Box::height = 10;	//不能在main函数中初始化，需要在声明Box类后初始化
int main() {
	cout << Box::height<< endl;	//通过类名引用静态数据成员
	Box obj1(10,12);
	obj1.printVolume(); //输出：Volume:1200
	
	return 0;
}
```

* 静态成员函数

  1. 静态成员函数的作用是处理静态数据成员；

2. 静态成员函数没有this指针，不能以默认方式访问本类中的非静态成员；

```C++
class MyClass {
    int x;
public:
    static void bar(MyClass& obj) {
        obj.x = 10; // 通过对象实例访问,不能简单x = 10
    }
};
```

### 友元的概念、分类、用法、好处及弊端

* 概念：友元可以访问与其有好友关系的类中的所有成员，包括私有成员
* 分类：友元函数，友元类；
* 用法：

```C++
//友元函数：将普通函数声明为友元函数
//友元成员：将成员函数声明为友元函数
//友元类：

#include <iostream>
#include <cmath>
using namespace std;

// 前向声明
class Complex;
class ComplexPrinter;

// 先声明 ComplexOperations类
class ComplexOperations {
public:
    void multiplyByScalar(Complex& c, double scalar);
    void tryAccess(const Complex& c);
};

// 复数类
class Complex {
private:
    double real;    // 实部
    double imag;    // 虚部

public:
    Complex(double r = 0.0, double i = 0.0) : real(r), imag(i) {}

    double getReal() const { return real; }
    double getImag() const { return imag; }
    
    void display() const {
        cout << real;
        if (imag >= 0) cout << " + " << imag << "i";
        else cout << " - " << -imag << "i";
    }
    
    // 声明友元函数（全局函数）
    friend Complex operator+(const Complex& c1, const Complex& c2);
    
    // 声明友元类
    friend class ComplexPrinter;
    
    // 声明友元成员函数（来自另一个类）
    friend void ComplexOperations::multiplyByScalar(Complex& c, double scalar);
};

// 实现 ComplexOperations 的成员函数:复数 x 标量 
void ComplexOperations::multiplyByScalar(Complex& c, double scalar) {
    c.real *= scalar;
    c.imag *= scalar;
}

//非友元成员函数访问限制
void ComplexOperations::tryAccess(const Complex& c) {
    // cout << "Trying to access real part: " << c.real << endl; // 报错，无法访问私有成员 
    cout << "Can only access public members: " << c.getReal() << endl;
}

// 友元函数：复数加法（全局函数）
Complex operator+(const Complex& c1, const Complex& c2) {
    return Complex(c1.real + c2.real, c1.imag + c2.imag);
}

// 友元类：专门打印复数的类,其成员函数都可访问友元的私有成员 
class ComplexPrinter {
public:
    void printDetails(const Complex& c) const {
        cout << "Complex details: ";
        c.display();
        cout << "\nReal part: " << c.real << ", Imaginary part: " << c.imag << endl;
    }
};

int main() {
    Complex c1(3.0, 4.0);	//c1 = 3 + 4i 
    Complex c2(1.0, -2.0);	//c2 = 1 - 2i
    Complex sum = c1 + c2;	//友元函数，sum = 4 + 2i
    
    ComplexPrinter printer;
    printer.printDetails(c1);//友元类的成员函数， 3+4i
    cout << endl;
    
    ComplexOperations ops;
    c2.display();
	cout << endl; 	//1-2i 
    ops.multiplyByScalar(c2, 2.5);	//友元成员函数
    c2.display();	//2.5 - 5i
    cout << endl;
    
    ops.tryAccess(c1);
    
    return 0;
}
```

* 好处与弊端：友元可以访问其他类的私有成员。
  1. 好处：有助于数据共享，提高程序效率；
  2. 弊端：对封装原则的一个小的破坏，因此只有在它能大大提高程序效率时才使用友元。

### 类模板的概念、写法（结合第 1 章）

* 概念：定义通用的类。用同一套代码处理不同的数据类型，而不需要为每种类型重复编写相似的类。

```C++
//mystack.h
#include <iostream>
using namespace std;

template <typename T>	//最重要的一句，后面都可以用T代指类型

class myStack {
private:
    T a[10001];  // 存储元素的数组
    int tt;      // 栈的大小
public:
    myStack() : tt(0) {}  // 构造函数
    void push(T t) {  // 入栈
        a[tt++] = t;
    }
    void pop() {  // 出栈
        if (tt > 0) tt--;
        else {
            cout << "error!栈内已无元素。" << endl;
        }
    }
    bool isEmpty() const {  // 判断栈是否为空
        return tt == 0;
    }
    T top() const {  // 获取栈顶元素
        if (tt > 0) return a[tt - 1];
        else {
            cout << "error!栈内已无元素。" << endl;
            return T();  // 返回类型的默认值
        }
    }
};

int main(){
    myStack<int> nums;	//int类型的栈
    myStack<char> ops;	//char类型的栈
}
```

## 运算符重载

* <p style="color:red;">大题</p>

### 理解运算符重载的概念、规则及特殊情况

* 概念：操作符（运算符）实际上也是函数，是系统的预定义函数，所以操作符和用户自定义函数一样也可以重载。

* 规则：

  （1）C++不允许用户自己定义新的运算符，只能对已有的C++运算符进行重载；

  （2）重载不能改变操作数个数；

  （3）重载不能改变运算符优先级；

  （4）重载不能改变运算符结合性；

  （5）重载运算符的函数不能有默认参数

  （6）重载运算符参数应至少有一个是类对象/类对象的引用；

  （7）“=”和  “&”不必用户重载；

  （8）.*     ::   sizeof     ?:    .     这五个不能重载；

* 双目运算符一般重载为友元函数、单目运算符一般重载为成员函数、极少数时候重载成普通函数；

```C++
//例如：对复数类中加号的2种重载方式
Complex Complex::operator+(const Complex &c){
    return Complex(real + c.real,image + c.image);
}

friend Complex operator+(Complex &c1, Complex &c2){		//友元函数因为没有this指针，所以形参会多一个
    return Complex(c1.real + c2.real, c1.image + c2.image);
}

//重载双目运算符：（本段代码无法在vs2022运行，会显示无法匹配合适的构造函数）
#include <iostream>
#include <cstring> 
using namespace std;
class String {
public:
	//默认构造函数
	String() {
		p = NULL;
	}
	String(char* str);
	friend bool operator>(String& string1, String& string2);
	friend bool operator<(String& string1, String& string2);
	friend bool operator==(String& string1, String& string2);
	void display();
private:
	char* p;
};
//构造函数
String::String(char* str) {
	p = str;
}

void String::display() {
	cout << p;
}
//都通过友元函数重载
bool operator>(String& string1, String& string2) {
	if (strcmp(string1.p, string2.p) > 0) return true;
	else return false;
}

bool operator<(String& string1, String& string2) {
	if (strcmp(string1.p, string2.p) < 0) return true;
	else return false;
}

bool operator==(String& string1, String& string2) {
	if (strcmp(string1.p, string2.p) == 0) return true;
	else return false;
}

//普通函数
void compare(String& string1, String& string2) {
	if (operator>(string1, string2) == 1) {
		string1.display();
		cout << ">";
		string2.display();
	}
	else if (operator<(string1, string2) == 1) {
		string1.display();
		cout << "<";
		string2.display();
	}
	else if (operator==(string1, string2) == 1) {
		string1.display();
		cout << "=";
		string2.display();
	}
	cout << endl;
}

int main() {
	String string1("hello"), string2("Book"), string3("Computer"), string4("Hello");
	compare(string1,string2);
	compare(string2,string3);
	compare(string1,string4);
}
```

* <<、>>只能重载为友元函数；( )、[]只能重载为成员函数；

```C++
char operator[](int i);
const char* operator()();
friend ostream& operator<<(ostream&, Complex&);
friend istream& operator>>(istream&, Complex&);
```

* 对于前置单目运算符，重载函数没有形参；对于后置单目运算符，重载函数需要有一个整数形参以示区别；

```C++
//将单目运算符++重载为时钟类的成员函数
#include <iostream>
#include <iomanip> 
using namespace std;
class Clock {
public:
	Clock(int NewH = 0, int NewM = 0, int NewS = 0) :Hour(NewH), Minute(NewM), Second(NewS) {};
	void ShowTime() {
		cout << setw(2) << Hour << ":" << Minute << ":" << Second << endl;
	}
	Clock& operator++();	//前置单目运算符重载
	Clock operator++(int);	//后置单目运算符重载
private:
	int Hour, Minute, Second;
};
//前置单目运算符重载函数
Clock Clock:: operator++() {
	Second++;
	if (Second >= 60) {
		Second = Second - 60;
		Minute++;
		if (Minute >= 60) {
			Minute = Minute - 60;
			Hour++;
			Hour = Hour % 24;
		}
	}
	return *this;	//通过this指针返回自增后的当前对象
}

//后置单目运算符重载函数
Clock Clock::operator++(int) {
	Clock old = *this;
	++(*this);
	return old;	//返回的是自增前的对象old
}

int main() {
	Clock myClock(23, 59, 59);
	cout << "First time output:";
	myClock.ShowTime();
	cout << "Show myClock++:";
	(myClock++).ShowTime();	//先引用并显示 23:59:59 ；后加变为：0:0:0
	cout << "Show ++myClock:";
	(++myClock).ShowTime();	//先加变为 0:0:1 ，同时显示出来
	return 0;
}
```

* 熟练掌握常用运算符重载函数的写法；

查阅课本P221-P224，**多加练习**

### ~~类型转换~~

#### C 语言中强制类型转换和自动类型转换

#### 转换构造函数的概念、作用及用法

##### 隐式调用将产生临时对象

##### 显式调用将产生无名对象

#### 强制类型转换运算符重载函数的概念、作用及用法（隐式调用和显式调用都将产生临 时变量，而原对象的类型未变）

### 了解临时变量、临时对象、无名对象的概念、作用域及特殊情况

| 特性         | 临时变量                | 临时对象             |       无名对象       |
| :----------- | :---------------------- | :------------------- | :------------------: |
| **类型**     | 基本类型 (int, float等) | 类类型               |        类类型        |
| **创建方式** | 编译器隐式创建          | 编译器隐式创建       |    程序员显式创建    |
| **可见性**   | 完全不可见              | 可通过引用访问       |      语法上可见      |
| **典型场景** | 表达式中间结果          | 隐式转换、返回值     |   显式构造函数调用   |
| **生命周期** | 表达式结束              | 表达式结束（可延长） | 表达式结束（可延长） |

* **临时变量或临时对象初始化 const 引用时，作用域被扩展**

* #### 1. **临时变量 (Temporary Variables)**

  **概念**：

  - 编译器在表达式求值过程中自动创建的**基本类型**的中间存储
  - 用于存储表达式计算的中间结果

  **示例**：

  ```C++
  int a = 5, b = 3;
  int c = a + b * 2;  // b*2的结果(6)存储在临时变量中
  ```

  **特点**：

  - 生命周期：当前完整表达式结束（分号处）
  - 不可见：无法通过标识符访问
  - 作用：优化计算过程，保存中间结果

  ------

  #### 2. **临时对象 (Temporary Objects)**

  **概念**：

  - 编译器在表达式求值过程中自动创建的**类类型**的中间实例
  - 通常由隐式类型转换或函数返回值产生

  **示例**：

  ```C++
  class MyClass {
  public:
      MyClass(int x) { /*...*/ }
  };
  
  void func(MyClass obj) {}
  
  func(10);  // 从int创建临时MyClass对象
  ```

  **特点**：

  - 生命周期：当前完整表达式结束（C++17前）
  - 作用：实现隐式转换、传递函数参数、存储返回值
  - 特殊规则：可绑定到`const&`或`&&`引用延长生命周期

  ------

  #### 3. **无名对象 (Anonymous Objects)**

  **概念**：

  - **显式创建**的、没有命名的类类型实例
  - 程序员直接调用构造函数创建的对象

  **示例**：

  ```C++
  class Point {
  public:
      Point(int x, int y) {}
  };
  
  // 显式创建无名对象
  Point(3, 4);  // 无名对象
  func(Point(1, 2));  // 作为参数的无名对象
  ```

  **特点**：

  - 生命周期：当前完整表达式结束
  - 作用：简化代码，避免命名中间变量
  - 与临时对象的关系：
    - 所有无名对象都是临时对象
    - 但临时对象不一定是无名对象（可能是隐式转换产生的）

  ------

  ### 生命周期与作用域规则

  #### 通用规则：

  1. **默认生命周期**：

     - 在完整表达式结束时销毁

     ```C++
     func(MyClass(10));  // 无名对象在分号后销毁
     ```

  2. **生命周期延长**：

     - 绑定到`const T&`：延长至引用作用域结束

     ```C++
     {
       const MyClass& ref = MyClass(10);  // 生命周期延长至块结束
     }  // 此处销毁
     ```

  3. **返回值优化**：

     - 编译器可消除返回时的临时对象

     ```C++
     MyClass create() {
       return MyClass(30);  // 可能直接构造在调用处
     }
     ```

  #### 特殊情况：

  1. **成员初始化列表**：

     ```C++
     class Container {
       MyClass member;
     public:
       Container() : member(MyClass(40)) {} 
       // 无名对象在构造函数体开始前销毁
     };
     ```

## 继承与派生

### 继承的概念、意义及分类

* 意义：实现可重用性，减少重复的工作量

#### 单继承

* 一个派生类（子类）只由一个基类（父类）派生

##### 派生类的声明方法

```C++
class Student1:public Student{	//不标明继承方式会默认私有继承，私有派生类不常用
    public:
    void display_1(){	//新增加的成员函数
        cout << "age:" << age << endl;
        cout << "address:" << addr << endl;
    }
    private:
    	int age;		//新增加的数据成员
    	string addr;	//新增加的数据成员
}
```

##### 三种不同的声明方式的区别

* 公有继承：基类的公用成员和保护成员在派生类中保持原有访问属性，其私有成员仍为基类私有
* 保护继承：基类的公用成员和保护成员在派生类中成了私有成员，其私有成员仍为基类私有
* 私有继承：基类的公用成员和保护成员在派生类中成了保护成员，其私有成员仍为基类私有

![a1cd4c88d1b8df0fd63bf1b669c4cdd7](./../Pictures/typora/a1cd4c88d1b8df0fd63bf1b669c4cdd7.png)

##### 派生类对象的组成（三部分），各部分成员初始化的分工及执行次序

* 派生类对象的**内存结构**由以下三部分组成：

* ### 1. **基类部分（Base Class Subobject）**

  ```C++
  class Base {
      int base_data;  // 基类成员
  };
  class Derived : public Base {
      // 基类部分包含 base_data
  };
  ```

  ### 2. **派生类部分（Derived Class Members）**

  - **组成**：派生类自身定义的非静态数据成员

  - **位置**：紧接在基类部分之后

  - **特点**：

    - 仅包含派生类新增的成员变量**(新增对象成员 + 新增普通成员)**
    - 不包含基类已存在的成员

  - **示例**：

    ```C++
    class Derived : public Base {
        int derived_data;  // 派生类新增成员
    };
    ```

  ### 3. **虚函数表指针（vptr）**（当存在虚函数时）

  - **组成**：指向虚函数表的指针（通常4/8字节）

  - **位置**：通常位于对象起始位置（编译器相关）

  - **特点**：

    - **每个多态类型一个vptr**（多重继承时可能有多个）
    - **虚函数表（vtable）包含**：
      - 类类型信息（RTTI）
      - 虚函数地址列表
      - 虚继承偏移量（若有虚继承）

  - **触发条件**：

    ```c++
    class Base {
    public:
        virtual void func() {}  // 虚函数导致vptr生成
    };
    ```

  ------

  ### 内存布局示意图（单继承）

  ```C++
  +-----------------------+
  |       vptr            |  // 虚函数表指针（若有虚函数）
  +-----------------------+
  |  Base class members   |  // 基类部分
  +-----------------------+
  | Derived class members |  // 派生类部分
  +-----------------------+
  ```

  ### 特殊情形说明

  1. **多重继承**：

     ```C++
     class A { int a; };
     class B { int b; };
     class C : public A, public B { int c; };
     ```

     ```C++
     [A部分][B部分][C部分]
     ```

  2. **虚继承**：

     ```C++
     class Base { int base; };
     class Derived : virtual public Base { int derived; };
     ```

     ```C++
     [Derived部分][虚基类指针][Base部分]
     ```

  3. **无虚函数时的优化**：

     - 若基类和派生类均无虚函数，则无vptr
     - 对象大小仅为：∑基类成员 + ∑派生类成员

     

------

* > 派生类构造函数分工执行次序？

（1）调用基类构造函数，对基类数据成员初始化；

（2）调用对象成员所在类的构造函数，对对象成员初始化；

（3）执行派生类构造函数本身，对派生类普通数据成员初始化；

* 在派生类对象释放时，先执行派生类析构函数，再执行其基类析构函数
* （2）中如果有**多个对象成员**，则以**声明的次序为准**，而不受成员初始化列表中次序的影响

##### 派生类的构造函数、析构函数、拷贝构造函数的写法~~（特殊情况）~~

* 派生类构造函数：
  1. 调用次序：见上；
  2. 特殊形式：不需要对派生类新增成员进行任何初始化操作时，**派生类构造函数的函数体可以为空**；如果在基类和对象成员类所在的类声明中都没有定义带参数的构造函数，**可以不必显示定义派生类构造函数**；
* 派生类析构函数：
  1. 派生类不能继承基类析构函数（构造函数也不可以）；
  2. 基类的清理工作由基类的胸骨函数负责；
  3. 调用次序：严格和构造函数的调用次序相反；
* 派生类拷贝构造函数：
  1. 成员初始化列表中**未被列出的调用**，系统将调用**缺省的构造函数**而不是缺省的拷贝构造函数去初始化对应的成员；
  2. 调用时机：和非派生情况的结论相同；
  3. 调用次序：与创建派生类对象时各构造函数调用次序相同；

```C++
class Student1 : public Student {
public:
    // 派生类构造函数
    Student1(int n, string nam, char s, int a, string ad) 
        : Student(n, nam, s) {
        //在函数体中只对派生类新增的数据成员进行初始化
        age = a;
        addr = ad;
    }
    
    // 派生类拷贝构造函数
    Student1(const Student1& stud) 
        : Student(stud),           // 调用基类拷贝构造函数
          age(stud.age),           // 拷贝派生类成员age
          addr(stud.addr) {        // 拷贝派生类成员addr
        // 可以在这里添加额外的拷贝逻辑
    }
    
    void show() {
        cout << "num:" << num << endl;
        cout << "name:" << name << endl;
        cout << "sex:" << sex << endl;
        cout << "age:" << age << endl;
        cout << "address:" << addr << endl << endl;
    }
    
    // 派生类析构函数
    ~Student1() {};

private:
    int age;
    string addr;
};
```

#### 多重继承

* 一个派生类由两个或多个基类派生

* > 各基类排列顺序任意，调用基类构造函数的顺序是按照声明派生类时基类出现的顺序；（虚基类会插队，并且虚基类从始至终只调用一次构造函数）

##### 二义性问题

* 最常见的问题是**继承的成员**同名，产生二义性问题；

1. 两个基类有同名成员：用基类名限定（c1.A::display();c1.B::display()）
2. 基类和派生类有同名成员：
   * **同名覆盖规则**：派生类新增加同名成员覆盖基类同名成员（和 函数重载 区分开）；
3. 类 A 和类 B 是从同一个基类派生的（菱形继承）：*用虚基类*

##### 虚基类（虚拟继承）的概念、写法及意义

* <p style="color:red;">写程序结果</p>

* 概念：通过虚基类，使得在继承间接共同基类时只保留一份成员；

* 写法：

```C++
#include <iostream>
#include <string>
using namespace std;

class Person {
public:
	Person(string nam, char s, int a)
	{
		name = nam; sex = s; age = a;
	};
	protected: 
		string name;
		char sex;
		int age;
};
//需要注意：为了保证虚基类在派生类中只继承一次，应当在该基类的所有直接派生类中声明为虚基类。否则仍然会出现对基类的多次继承
class Teacher:virtual public Person{	//虚拟公有继承
public:
	Teacher(string nam, char s, int a, string t) :Person(nam, s, a) {
		title = t;
	}
protected:
	string title;
};

class Student :virtual public Person {	//再次虚拟公有继承
public:
	Student(string nam, char s, int a, float sco) :Person(nam, s, a), score(sco) {

	}
protected:
	float score;
};
//最派生类
class Graduate :public Teacher, public Student {
public:Graduate(string nam, char s, int a, string t, float sco, float w) :Person(nam, s, a), Teacher(nam, s, a, t), Student(nam, s, a, sco), wage(w) {}
	  void show() {
		  cout << "name:" << name << endl;
		  cout << "age:" << age << endl;
		  cout << "sex:" << sex << endl;
		  cout << "score:" << score << endl;
		  cout << "title:" << title << endl;
		  cout << "wages:" << wage << endl << endl;
	  }
private:
	float wage;

};

int main() {
	Graduate grad1("Wang-li", 'f', 24, "assistant",89.5, 1234.5);
	grad1.show();	//请读者自己判断运行结果
	return 0;
}
```

* 意义：避免产生二义性

##### 最派生类的概念、写法及意义

* <p style="color:red;">简答</p>

* 概念：最后的派生类；在最后的派生类中不仅要负责对其直接基类进行初始化，还要负责对虚基类初始化，也只有最派生类对虚基类初始化；

* 写法：见 Fence 55；

* 意义：C++ 编译系统只执行最后的派生类对虚基类的构造函数的调用，保证了 **虚基类的数据成员不会被多次初始化**。（构造函数调用次序见5.1.2）；

> 1. 虚基类构造函数（按继承顺序）
> 2. 直接基类构造函数（按声明顺序）
> 3. 成员对象的构造函数
> 4. 自身构造函数

### 子类型的概念、用法及特点

* 公用派生类是基类真正的**子类型**，完整地继承了基类的功能；

* > 特点：单向、不可逆，可传递，有助于实现多态性；

* 赋值兼容规则：派生类的值赋给基类对象，用基类对象时可以用子类对象代替；

![image-20250610210422408](./../Pictures/typora/image-20250610210422408.png)

* 注意：指向基类对象的指针变量也可以指向派生类对象，但实际上指向基类的指针变量是派生类从基类继承的部分，通过指向基类对象的指针只能访问派生类中的基类成员，而不能访问派生类中新增成员（注意与 同名覆盖规则 对比）；怎么解决？*用虚函数和多态性*

### 继承与组合

* 继承是垂直的，组合（即聚集）是水平的;二者都是为了在某种程度上实现软件复用，即共享

## 多态性与虚函数

* <p style="color:red;">写程序结果</p>

### 多态性的概念、分类

* 多态性：程序设计中，多态性是指具有不同功能的函数可以用同一个函数名，这样就可以用一个函数名调用不同内容的函数；

#### 静态多态性

* 又称编译时的多态性，采用静态联编（先期联编，即程序编译阶段就可以确定的多态性）技术，有两种实现形式：

1. **强制多态（类型强制）**，可以简单理解为强制类型转换；
2. **重载多态（重载）**，可以简单理解为函数重载；

![59ada3dc1dcb516f02feb7ac093e176c](./../Pictures/typora/59ada3dc1dcb516f02feb7ac093e176c.png)

#### 动态多态性

* 又称运行时的多态性，采用动态联编（滞后联编，即程序运行阶段才能确定的多态性）技术，有两种实现方式：

1. **类型参数多态**：可以简单理解为类模板或函数模板；
2. **包含多态**：通过虚函数实现；

##### 虚函数的概念、用法（virtual）；了解其内部实现机制（虚函数表vtable和虚指针 vptr）

* <p style="color:red;">写程序结果</p>

* 虚函数：

  1. 概念：使用`virtual`声明的成员函数，支持运行时多态
  2. 用法：基类声明虚函数，派生类可重写（override显式声明重写，不加override也会隐式声明重写）
  3. 每个多态类有一个虚函数表
  4. 对象内含虚指针(vptr)指向vtable
  5. 调用虚函数时通过vptr间接寻址

```C++
#include <iostream>
using namespace std; 
class Base {
public:
    virtual void func() { cout << "Base func"; }
    virtual ~Base() {}  // 虚析构函数
};

class Derived : public Base {
public:
    void func() { cout << "Derived func"; }
};

int main() {
    Base* b = new Derived();
    b->func();  // 输出"Derived func"（动态绑定）
    delete b;
}
```

* 虚函数表vtable机制

```C++
class Base {
public:
    virtual void f1() {}
    virtual void f2() {}
};

// 内存布局示例：
Base b;
cout << sizeof(b); // 可能输出8（64位系统vptr大小）

// vtable内容：
// [0] &Base::f1
// [1] &Base::f2
```

* 多继承中的vptr：

```C++
class A { virtual void fa(); };
class B { virtual void fb(); };
class C : public A, public B {};

C c;
// 内存布局：
// [vptr_A] -> A的vtable
// [vptr_B] -> B的vtable
// 其他成员
```

##### 实现动态联编的必要条件

* 虚函数、基类指针或引用

### 虚析构函数的概念和意义：

```C++
virtual ~Point(){cout<<"executing Point destructor"<<endl;}
```

* 最好把基类的析构函数声明为虚函数 ；
* 如果将基类的析构函数声明为虚函数时，由该基类所派生的所有派生类的析构函数也都自动成为虚函数；
* **构造函数不能是虚函数**；析构函数能声明虚函数是因为编译器会把函数名统一为destruct；

### 纯虚函数、抽象类的概念、意义及基本用法

* <p style="color:red;">简答</p>

#### 纯虚函数

* 概念：当我们在基类中将某一成员函数定为虚函数，只是为了预留一个函数名，具体功能留给派生类根据需要去定义时，可以**只给出函数原型，并在后面加上“=0”**；

```C++
virtual float area( ) const {return 0;};
//不写无意义的函数体，简化为纯虚函数：
virtual float area( ) const =0;	//纯虚函数，注意最后有分号
```

* 用法：

1. 没有函数体；
2. 只有一个函数名字，不具备功能，因此不能被调用；
3. 派生类中没有对基类的纯虚函数定义，则该虚函数在派生类中还是纯虚函数；

#### 抽象类

* 概念：不用来定义对象而只作为一种基本类型用作继承去建立派生类的类，又因常作为基类，通常称为抽象基类；
* 用法：

1. **凡是包含纯虚函数的类都是抽象类**；
2. 派生类中没有对抽象类中所有纯虚函数定义，就也是抽象类，**不能被实例化**（**定义对象）**；
3. **可以定义指向抽象类数据的指针变量**，在派生类成为具体类后**指向派生类对象**，实现多态性操作；

## ~~输入输出流~~

## ~~C++工具~~

<p align="right">author:Verse</p>

<p align="right">date:2025/6/11</p>