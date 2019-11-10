1. In c++, if we do not write our own, the compiler will automaticly create a default constructor, copy constructor and an assignment operator for every class
2. When a copy constructor wil be called?
   - when an object of a class is return by value
   - when an object of a class is passed by value as argument
   - when an object is constructed based on another object of the same class
   - when compiler generate a temporary object
3. We must use initializer list in a constructor when
   - For initialization of non-static const data members
   - For initialization of reference members
   - For initialization of member objects which do not have default constructor
   - For initialization of base class members
   - When constructor’s parameter name is same as data member
4. Why copy constructor argument should be const in C++?
   - One reason for passing const reference is, we should use const in C++ wherever possible so that objects are not accidentally modified
5. Implicit return type of a class constructor is the class type itself
6. Static methods can only access static members (data and methods)

8. 构造函数与复制构造函数
   - 复制构造函数（copy constructor）
   - 只有一个参数， 即对同类对象的引用
   - 形如 X::X(X&) 或 X::X(const X&), 后者能以常量对象作为参数
   - 如果没有定义复制构造函数， 那么编译器生成默认，执行复制的工作

复制构造函数起作用的三种情况
   - 用一个对象去初始化同类的另一个对象  Complex c2(c1) / Complex c2 = c1
   - 如果某函数有一个参数是类A的对象， 那么该函数被调用时， 类A的复制构造函数将被调用
   - 如果函数的返回值是类A的对象时，则函数返回时，A的复制构造函数被调用

类型转换构造函数
   - 只有一个参数
   - 不是复制构造函数

9. 静态成员变量和静态成员函数
   - 关键字： static
   - 静态成员变量 - 为所有对象共享
   - 静态成员函数 - 不具体作用于某个对象
   - 静态成员不需要通过对象就能访问

访问静态成员
 - 类名::成员名 CRectangle::Print()
 - 对象名.成员名 CRectangle r; r.Print()
 - 指针->成员名 CRectangle *p = &r; p->Print()
 - 引用.成员名 CRectangle & ref = r; ref.Print()

   - 静态成员变量本质上是一个全局变量， 哪怕一个对象都不存在，类的静态成员变量也存在
   - 静态成员函数本质上是一个全局函数
   - 用静态成员将这两个变量封装进类中，容易理解和维护

注意：在静态成员函数中，不能访问非静态成员变量，也不能调用非静态成员函数

2. 成员对象和封闭类
- 成员对象：一个类的成员变量是另一个类的对象
- 包含成员对象的类叫封闭类
初始化封闭类，添加初始化列表：
类名::构造函数(参数表): 成员变量1(参数表),成员变量2(参数表), ...
{
    ...
}
当封闭类对象生成时，
- S1：执行所有成员对象的构造函数
- S2：执行封闭类的构造函数
成员对象的构造函数调用顺序
- 和成员对象在类中的说明顺序一致
- 与在成员初始化列表中出现的顺序无关
当封闭类的对象消亡时
- S1：先执行封闭类的析构函数
- S2：执行成员对象的析构函数
析构函数与构造函数的调用顺序相反
******************************************************************************************/

/******************************************************************************************
3. 友元(friend)
友元函数 - 一个类的友元函数可以访问该类的私有成员
将一个类的成员函数（包括构造，析构函数）定义为另一个类的友元

class B {
    public:
        void function();
}
class A {
    friend void B::function();
    friend class B;
}

友元类
B是A的友元类 -> B的成员函数可以访问A的私有成员

**********************************************************************************/

/**********************************************************************************
4. 常量对象
- 定义对象对象时在前面加const关键字
const Demo obj; // 常量对象
常量对象上不能执行非常量成员函数

常量成员函数
- 在类的成员函数说明后面加const关键字
- 常量成员函数执行期间不应修改其所作用的对象。因此，在常量成员函数中不能修改成员变量的值（静态成员变量除外），
也不能调用同类的非常量成员函数（静态成员函数除外）
- 两个成员函数，名字和参数表都一样，但是一个是const，一个不是，算重载

常引用 - 避免复制构造函数，提高效率
******************************************************************************************/

#include <iostream>
using namespace std;

class Sample {
public:
    int value;
    void getValue() const;
    void func() {};
    Sample() {};
};

void Sample::getValue() const {
    value = 0; //error 常量成员函数中不能修改成员变量的值
    func(); //error 不能调用非常量成员函数
}

int main {
    const Sample a;
    a.value = 100; //error, 常量对象不可被修改
    a.func(); //error, 常量对象中不可执行非常量成员函数
    a.getValue(); //ok, 常量对象中执行常量成员函数
    return 0;
}

/************************************************************************
5. 运算符重载
- 对已有的运算符赋予多重的含义
- 使同一运算符作用于不同类型的数据时->不同类型的行为
- 扩展c++提供的运算符的适用范围，以用于类所表示的抽象数据类型
- 运算符重载的实质是函数重载

返回值类型 operator 运算符 （形参表）
{
    ...
}

重载为普通函数时，参数个数为运算符目数

在程序编译时：
- 把 含运算符的表达式 -> 对运算符函数的调用
- 把 运算符操作数 -> 运算符函数的参数
- 运算符被多次重载时，根据实参的类型决定调用哪个运算符函数
 *********************************************************************/

//运算符重载为成员函数
class Complex {
public:
    Complex(double r=0.0, double m=0.0):
        real(r), im(m) {} //constructor
    Complex operator+ (const Complex &);
    Complex operator- (const Complex &);
private:
    double real;
    double im;
};

//重载为成员函数时，参数个数为运算符目数减一

Complex Complex::operator+ (const Complex& operand2) {
    return Complex(real + operand2.real, im + operand2.im);
}
Complex Complex::operator- (const Complex& operand2) {
    return Complex(real - operand2.real, im - operand2.im);
}

int main {
    Complex x, y(4.3, 8.2), z(3.3, 1.1);
    x = y+z; //相当于 y.operator+(z)
    x = y-z; //相当于 y.operator-(z)
    return 0
}

/***************************************************************
6. 赋值运算符 = 的重载
赋值运算符“=”只能重载为成员函数
 ****************************************************************/

class String {
private:
    char * str;
public:
    String() : str(NULL) {}
    const char * c_str() {return str;}
    char * operator= (const char * s);
    ~String();
}

char * String::operator = (const char * s) {
    if(str) delete [] str;
    if(s) {
        str = new char[strlen(s)+1];
        strcpy(str, s);
    }
    else
    {
        str = NULL;
    }
    return str;
}

String::~String() {
    if(str) delete [] str;
}

int main {
    String s;
    s = "Good Luck"; //s.operator=("Good Luck")
    cout << s.c_str() << endl;
}

/**************************************************************************
重载赋值运算符的意义 - 浅复制和深复制
s1 = s2
浅复制
- 执行逐个字节的复制工作
深复制
- 将一个对象中的指针变量指向的内容 -> 复制到另一个对象中指针成员对象指向的地方
 **************************************************************************/

//深复制
//在class MyString 里添加成员函数
String & operator= (const String & s) {
    if(str == s.str) return * this;
    if(str) delete [] str;
    str = new char[strlen(s.str)+1];
    strcpy(str, s.str);
    return * this;
}

/*****************************************************************************
7.继承与派生
继承：在定义一个新的类B时，如果该类与某个已有的类A相似（指的是B拥有A的全部特点）
那么就可以把A作为一个基类，而把B作为基类的一个派生类（子类）
- 派生类是通过对基类进行修改和扩充得到的，在派生类中，可以扩充新的成员变量和成员函数
- 派生类一经定义后，可以独立使用，不依赖于基类
- 派生类拥有基类的全部成员函数和成员变量
- 派生类的各个成员函数中，不能访问基类中的private成员
写法：
class 派生类名 ： public 基类名
{
    ...
};
- 派生类对象的体积，等于基类对象的体积，加上派生类对象自己的成员变量的体积。派生类对象中，
包含着基类的对象，而且基类对象的存储位置位于派生类对象新增的成员变量之前

继承关系与复合关系
继承：“是”关系
逻辑上要求：“一个B对象也是一个A对象”

复合：“有”关系
- 成员对象

基类和派生类有同名成员的情况
访问范围说明符
基类的private成员：可以被下列函数访问
- 基类的成员函数
- 基类的友元函数
基类的public成员：可以被下列函数访问
- 基类的成员函数
- 基类的友元函数
- 派生类的成员函数
- 派生类的友元函数
- 其他的函数
基类的protected成员：可以被下列函数访问
- 基类的成员函数
- 基类的友元函数
- 派生类的成员函数可以访问访问当前对象的基类保护成员

派生类的构造函数
- 派生类对象 包含 基类对象
- 执行派生类的构造函数之前，先执行基类的构造函数
- 派生类交代基类初始化，具体形式：--初始化列表
构造函数名（形参表）：基类名（基类构造函数实参表）
{

}
Bug -> FlyBug
FlyBug::FlyBug(int legs, int color, int wings):Bug(legs, color) {
    nWings = wings;
}

在创建派生类对象时，
- 需要调用基类的构造函数：
  初始化派生类对象中从基类继承的成员
- 在执行一个派生类的构造函数之前，
  总是先执行基类的构造函数

调用基类构造函数的两种方式
- 显式方式
  派生类的构造函数中 -> 基类构造函数提供参数
  derived::derived(ard_derived-list):base(arg_base-list)
- 隐式方式
  派生类的构造函数中，省略基类构造函数时
  派生类的构造函数，自动调用基类的默认构造函数
派生类的析构函数被执行时，执行完派生类的析构函数后，自动调用基类的析构函数

在创建派生类对象时，执行派生类的构造函数之前：
- 调用基类的构造函数
- 调用成员对象类的构造函数
执行完派生类的析构函数后：
- 调用成员对象类的析构函数
- 调用基类的析构函数
析构函数的调用顺序与构造函数的调用顺序相反

public继承的赋值兼容规则
class base { };
class derived : public base { };
base b;
derived d;
1）派生类对象可以赋值给基类对象
b = d;
2）派生类对象可以初始化基类引用
base & br = d;
3) 派生类对象的地址可以赋值给基类指针
base * bp = &d;
****************************************************************/

/****************************************************************
8.多态与虚函数
在类的定义中，前面有virtual关键字的成员函数就是虚函数
class base {
    virtual int get();
};
int base::get(){}
- virtual关键字只用在类定义里的函数声明中，写函数体不用
- 构造函数和静态成员函数不能是虚函数

多态的表现形式一
- 派生类的指针可以赋给基类指针
- 通过基类指针调用基类和派生类中的同名虚函数时
1）若该指针指向一个基类对象，那么被调用的是基类的虚函数
2）若该指针指向一个派生类对象，那么被调用的是派生类的虚函数
这种机制就叫“多态”

多态的表现形式二
- 派生类的对象可以赋给基类引用
- 通过基类引用调用调用基类和派生类的同名虚函数时
1）若该引用引用的是一个基类的对象，那么被调用的是基类的虚函数
2）若该引用引用的是一个派生类的对象，那么被调用的是派生类的虚函数
这种机制也叫“多态”

多态的作用
在面向对象的程序设计中使用多态，能够增强程序的可扩充性，即程序需要修改或增加功能时，
需要改动和增加的代码较少

用基类指针数组存放指向各种派生类对象的指针，然后遍历该数组，就能对各个派生类对象做各种
操作，是很常用的做法

在非构造函数，非析构函数的成员函数中调用虚函数，是多态

在构造函数和析构函数中调用虚函数，不是多态

多态实现的关键 -- 虚函数表
每一个有虚函数的类（或有虚函数的类的派生类）都有一个虚函数表，该类的任何对象中都放着虚函数
表的指针。虚函数表中列出了该类的虚函数地址。多出来的 4个字节就是用来放虚函数表的地址的

虚析构函数
- 通过基类指针删除派生类对象时
->先调用派生类的析构函数
->再调用基类的析构函数
解决办法：
把基类的析构函数声明为virtual（派生类的析构函数virtual可以不进行声明）

类如果定义了虚函数，则最好将析构函数也定义成虚函数
note: 不允许以虚函数作为构造函数

纯虚函数：没有函数体的虚函数
抽象类：包含纯虚函数的类
- 自能作为基类来派生新类使用
- 不能创建抽象类的对象
- 抽象类的指针和引用->由抽象类派生出来的类的对象
抽象类中：
- 在成员函数中可以调用纯虚函数
- 在构造函数和析构函数内部不能调用纯虚函数
如果一个类从抽象类派生而来
->它实现了基类中的所有纯虚函数，才能成为非抽象类
 *******************************************************************/

/*
文件操作
数据的层次
位 bit
字节 byte
域/记录
将所有记录顺序地写入一个文件 -> 顺序文件
顺序文件 - 一个有限字符构成的字符流
c++:ifstream, ofstream, fstream共三个类
 */

/*
函数模板
template <class 类型参数1， class 类型参数2， ...>
返回值类型 模板名(形参表) {
    函数体
}

函数模板可以重载

类模板
template <类型参数表>
class 类模板名 {
    成员变量和成员函数
};

-类模板的成员函数，如在类模板外定义时
template <类型参数表>
返回值类型 类模板名<类型参数表>::成员函数名(参数表) {
    函数体
}

用类模板定义对象的写法如下
类模板名 <真实类型参数表> 对象名(构造函数实际参数表)
编译器由类模板生成类的过程叫类模板的实例化，类类模板实例化得到的类叫模板类
- 为类型参数指定的数据类型不同，得到的模板类不同
- 同一个类模板的两个模板类是不兼容的

类模板与继承
- 类模板派生出类模板
- 模板类派生出类模板
- 普通类派生出类模板
- 模板类派生出普通类
 */
