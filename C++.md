# sort and rank an unsorted list of number

```c++
#include<bits/stdc++.h>
using namespace std;
int N,a[100001],b[100001];
map<int,int> m;
int main(){
cin>>N;
for(int i=0;i<N;i++)
{
    cin>>a[i];
    b[i]=a[i];
}
sort(b,b+N);//sort
int c=1;//rank
m[b[0]]=1;
for(int i=1;i<N;i++)
{
    if(b[i]!=b[i-1])
    {
        c++;
        m[b[i]]=c;
    }
}
for(int i=0;i<N;i++)
    if(m[a[i]]!=0)
        cout<<m[a[i]]<<" ";

return 0;
}
```

# lower_bound

__find ">="__

```c++
#include<algorithm>
#include<iostream>

using namespace std;

int main() {
int a[5] = { 1,2,3,3,8 };
  
int   index = lower_bound(a, a + 5, 3)-a;
 
if   (index==5 ) cout << " not found! ";
else  cout << index;
 
return   0;
}
```



# upper_bound

__find "<"__

just the same as above

# binary_search

whether the data appears







# 替代new的char[length]方法

```
int length;

char message=(char* )alloca(lengthsizeof(char));

```





# STATIC

### [为什么要使用静态方法](https://www.cnblogs.com/LvLoveYuForever/p/5846893.html)

静态方法的好处就是不用生成类的实例就可以直接调用。

[static](https://so.csdn.net/so/search?q=static&spm=1001.2101.3001.7020)方法修饰的成员不再属于某个对象，而是属于它所在的类。只需要通过其类名就可以访问，不需要再消耗资源反复创建对象。

在类第一次加载的时候，static就已经在内存中了，直到程序结束后，该内存才会释放。

如果不是static修饰的成员函数，在使用完之后就会立即被JVM回收。

 

### 什么时候使用static？

如果这个方法是作为一个工具来使用的，就声明为static，不需要new一个对象就可以使用。比如：connect DB就可以声明一个Connection()的static方法，

因为是静态的，说明connection DB不是某个对象所特有的功能，只是作为一种连接到DB的工具



# OpenGL debug MACROS(宏)

e.g

``` 
#define GLCall(x) GLClearError();\

	x;\
	ASSERT(GLLogCall());
	
#define ASSERT(x) if(！(x)) __debugbreak();

```



 # goto statement

![1672270213060](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1672270213060.png)

 ```#include <iostream>
using namespace std;
int main ()
{
   // 局部变量声明
   int a = 10;

   // do 循环执行
   LOOP:do
   {
       if( a == 15)
       {
          // 跳过迭代
          a = a + 1;
          goto LOOP;
       }
       cout << "a 的值：" << a << endl;
       a = a + 1;
   }while( a < 20 );

   return 0;
}  
 ```

**结果不会输出15**  



# extern "c"

extern "C"的主要作用就是为了能够正确实现C++代码调用其他C语言代码。加上extern "C"后，会指示编译器这部分代码按C语言的进行编译，而不是C++的。由于C++支持函数重载，因此编译器编译函数的过程中会将函数的参数类型也加到编译后的代码中，而不仅仅是函数名；而C语言并不支持函数重载，因此编译C语言代码的函数时不会带上函数的参数类型，一般之包括函数名。

### extern "C"的含义

extern "C" 包含双重含义，从字面上即可得到：首先，被它修饰的目标是“extern”的；其次，被它修饰的目标是“C”的。
 被extern "C"限定的函数或变量是extern类型的；

**1、extern关键字**
 extern是C/C++语言中表明函数和全局变量作用范围（可见性）的关键字，该关键字告诉编译器，其声明的函数和变量可以在本模块或其它模块中使用。
 通常，在模块的头文件中对本模块提供给其它模块引用的函数和全局变量以关键字extern声明。例如，如果模块B欲引用该模块A中定义的全局变量和函数时只需包含模块A的头文件即可。这样，模块B中调用模块A中的函数时，在编译阶段，模块B虽然找不到该函数，但是并不会报错；它会在**链接阶段**中从模块A编译生成的目标代码中找到此函数。
 与extern对应的关键字是static，被它修饰的全局变量和函数只能在本模块中使用。因此，一个函数或变量只可能被本模块使用时，其不可能被extern “C”修饰。

**2、被extern "C"修饰的变量和函数是按照C语言方式编译和链接的**
 首先看看C++中对类似C的函数是怎样编译的。
 作为一种面向对象的语言，C++支持函数重载，而过程式语言C则不支持。函数被C++编译后在符号库中的名字与C语言的不同。例如，假设某个函数的原型为：
 void foo( int x, int y );
 该函数被C编译器编译后在符号库中的名字为_foo，而C++编译器则会产生像_foo_int_int之类的名字（不同的编译器可能生成的名字不同，但是都采用了相同的机制，生成的新名字称为“mangled name”）。
 ** _foo_int_int这样的名字包含了函数名、函数参数数量及类型信息，C++就是靠这种机制来实现函数重载的。** 例如，在C++中，函数void foo( int x, int y )与void foo( int x, float y )编译生成的符号是不相同的，后者为_foo_int_float。
 同样地，C++中的变量除支持局部变量外，还支持类成员变量和全局变量。用户所编写程序的类成员变量可能与全局变量同名，我们以"."来区分。而本质上，编译器在进行编译时，与函数的处理相似，也为类中的变量取了一个独一无二的名字，这个名字与用户程序中同名的全局变量名字不同。



```cpp
// 模块A头文件　moduleA.h
#ifndef MODULE_A_H
#define MODULE_A_H
int foo( int x, int y );
#endif
```



```cpp
//在模块B中引用该函数：
// 模块B实现文件　moduleB.cpp
#include "moduleA.h"
foo(2,3);
```



```cpp
// 模块A头文件　moduleA.h
#ifndef MODULE_A_H
#define MODULE_A_H
extern "C" int foo( int x, int y );
#endif
```

## 应用场合

- C++代码调用C语言代码、在C++的头文件中使用
  在C++中引用C语言中的函数和变量，在包含C语言头文件（假设为cExample.h）时，需进行下列处理：

  **在C中引用C++语言中的函数和变量时，C++的头文件需添加extern "C"，但是在C语言中不能直接引用声明了extern "C"的该头文件，应该仅将C文件中将C++中定义的extern "C"函数声明为extern类型**

  ```cpp
  extern "C"
  {
  #include "cExample.h"
  }
  ```

- 如果C++调用一个C语言编写的.DLL时，当包括.DLL的头文件或声明接口函数时，应加extern "C"{}。

  

  

  # Class和Struct的区别

  **class 和 struct 最本质的区别 : class 是引用类型，它在堆中分配空间，栈中保存的只是引用；而 struct 是值类型，它在栈中分配空间。**

  class是引用类型，struct是值类型；既然 class 是引用类型，class 可以设为 null；但是我们不能将 struct 设为 null，因为它是值类型。



# RALL

RAII 是 resource acquisition is initialization 的缩写，意为“资源获取即初始化”。它是 C++ 之父 Bjarne Stroustrup 提出的设计理念，其核心是把资源和对象的生命周期绑定，对象创建获取资源，对象销毁释放资源。在 RAII 的指导下，C++ 把底层的资源管理问题提升到了对象生命周期管理的更高层次。



# 智能指针

因为C++没有自动回收内存的机制，因此每一次new出来的动态内存必须手动delete回去。而智能指针可以解决这个问题。



**shared_ptr 允许多个指针指向同一个对象**

**unique_ptr 独占所指向的对象**

**weak_ptr shared_ptr的弱引用**



## shared_ptr描述(in memory):

shared_ptr是一个标准的共享所有权的智能指针，就是允许多个指针指向同一对象，shared_ptr对象中不仅有一个指针指向某某(比如 int型,**以下也拿int类型举例**)对象，还拥有一个引用计数器，代表一共有多少指针指向了那个对象。

## shared_ptr自动销毁所管理的对象

每当创建一个shared_ptr的对象指向int型数据，则引用计数器值+1，每当销毁一个shared_ptr对象，则-1.当引用计数器数据为0时，shared_ptr的析构函数会销毁int型对象，并释放它占用的内存。

## shared_ptr和new的配合使用

接受指针作为参数的智能指针的构造函数是explicit类型，意味着只能以初始化的方式定义。
定义方法:

```cpp
shared_ptr<int> p1;
//被初始化成为一个空指针

shared_ptr<int> p2 (new int(4));
//指向一个值是4的int类型数据

shared_ptr<int> p3 = new int(4);
//错误，必须直接初始化
```

## 4、不能混合使用普通指针和智能指针，因为智能指针不是单纯的赤裸裸的指针

```text
void process(shared_ptr<int> ptr){
//受到参数值传递的影响，ptr被构造并且诞生，执行完函数块后被释放
}

int *x(new int (43));
//x是一个普通的指针

process(x);
//错误,int * 不能转换成shared_ptr<int>类型

process(shared_ptr<int> x);
//临时创造了x,引用数+1，执行完process之后，引用数-1

int j = *x;
//x是一个空悬指针，是未定义的
```

## 5、不能使用get()函数对智能指针赋值或初始化

原因：get()函数得到的是共享对象的地址，是内置指针，指向智能指针管理的对象，而智能指针不仅仅包含地址，两个东西不是一个类型的，也不能彼此包含，因此不能这样做。 **同样，把get（）返回值 绑定到智能指针上也是错误的**
如下：

```cpp
shared_ptr<int> p (new int(22));
int *q = p.get();
//语义没问题

{
shared_ptr<int> (q);
//意味着q被绑定，！！！！引用计数器还是1！！！！
//如果这个被执行，程序块结束以后q和q所指的内容被销毁，
   则代表着以后执行(*p)的解引用操作，就成了未定义的了。
}

int r = *p;
//已经不对了，因为p指向的内存已经在刚才那个代码块里被q释放了
```

## shared_ptr的一些操作

```text
shared_ptr<T> p;
//空智能指针，可指向类型是T的对象

if(p)
 //如果p指向一个对象,则是true

(*p)
//解引用获取指针所指向的对象

p -> number == (*p).number;

p.get();
//返回p中保存的指针

swap(p,q);
//交换p q指针

p.swap(q);
//交换p,q指针

make_shared<T>(args) 
//返回一个shared_ptr的对象，指向一个动态类型分配为T的对象，用args初始化这个T对象

shared_ptr<T> p(q)
//p 是q的拷贝，q的计数器++，这个的使用前提是q的类型能够转化成是T*

shared_pts<T> p(q,d) 
//p是q的拷贝,p将用可调用对象d代替delete
//上面这个我其实没懂，也没有查出来这个的意思

p =q;
//p的引用计数-1，q的+1,p为零释放所管理的内存

p.unique();
//判断引用计数是否是1，是，返回true

p.use_count();
//返回和p共享对象的智能指针数量

p.reset();
p.reset(q);
p.reset(q,d);
//reset()没懂，这个以后再来补充吧
```





# 关于类/对象大小的计算

**首先，类大小的计算遵循结构体的对齐原则**
**类的大小与普通数据成员有关，与成员函数和静态成员无关。即普通成员函数，静态成员函数，静态数据成员，静态常量数据成员均对类的大小无影响。**

静态数据成员之所以不计算在类的对象大小内，是因为类的静态数据成员被该类所有的对象所共享，并不属于具体哪个对象，静态数据成员定义在内存的全局区。

**虚函数对类的大小有影响，是因为虚函数表指针带来的影响**
**虚继承对类的大小有影响，是因为虚基表指针带来的影响**

**空类的大小是一个特殊情况,空类的大小为1**



# volatile

简单地说就是防止编译器对代码进行优化。比如如下程序：

```
XBYTE[2]=0x55;
XBYTE[2]=0x56;
XBYTE[2]=0x57;
XBYTE[2]=0x58;
```

对外部硬件而言，上述四条语句分别表示不同的操作，会产生四种不同的动作，但是编译器却会对上述四条语句进行优化，认为只有XBYTE[2]=0x58（即忽略前三条语句，只产生一条机器代码）。如果键入**volatile**，则编译器会逐一地进行编译并产生相应的机器代码（产生四条代码）。



Consider this code,

```cpp
int some_int = 100;

while(some_int == 100)
{
   //your code
}
```

When this program gets compiled, the compiler may optimize this code, if it finds that the program **never** ever makes any attempt to change the value of `some_int`, so it may be tempted to optimize the `while` loop by changing it from `while(some_int == 100)` to *something* which is equivalent to `while(true)` so that the execution could be fast (since the condition in `while` loop appears to be `true` always). *(if the compiler doesn't optimize it, then it has to fetch the value of some_int and compare it with 100, in each iteration which obviously is a little bit slow.)*

However, sometimes, optimization (of some parts of your program) may be **undesirable**, because it may be that someone else is changing the value of `some_int` from **outside the program which compiler is not aware of**, since it can't see it; but it's how you've designed it. In that case, compiler's optimization would **not** produce the desired result!

So, to ensure the desired result, you need to somehow stop the compiler from optimizing the `while` loop. That is where the `volatile` keyword plays its role. All you need to do is this,

```cpp
volatile int some_int = 100; //note the 'volatile' qualifier now!
```



# thread pool

https://nrecursions.blogspot.com/2014/08/mutex-tutorial-and-example.html





# C++ 类型转换

## C风格的强制转换

在C++基本的数据类型中，可以分为四类：整型，浮点型，字符型，布尔型。其中数值型包括 整型与浮点型；字符型即为char。

（1）将浮点型数据赋值给整型变量时，舍弃其小数部分。

（2）将整型数据赋值给浮点型变量时，数值不变，但是以指数形式存储。

（3）将double型数据赋值给float型变量时，注意数值范围溢出。

（4）字符型数据可以赋值给整型变量，此时存入的是字符的**ASCII**码。

（5）将一个int，short或long型数据赋值给一个char型变量，只将低8位原封不动的送到char型变量中。 
（6）将有符号型数据赋值给长度相同的无符号型变量，连同原来的符号位一起传送。

## C++强制类型转换

在C++语言中新增了四个关键字static_cast、const_cast、reinterpret_cast和dynamic_cast。这四个关键字都是用于强制类型转换的。

新类型的强制转换可以提供更好的控制强制转换过程，允许控制各种不同种类的强制转换。

C++中风格是static_cast<type>(content)。C++风格的强制转换其他的好处是，它们能更清晰的表明它们要干什么。程序员只要扫一眼这样的代码，就能立即知道一个强制转换的目的。 

##  1) static_cast

```
int a = 10;
int b = 3;
double result = static_cast<double>(a) / static_cast<double>(b);
```

**它主要有如下几种用法：**
    （1）用于类层次结构中基类和派生类之间指针或引用的转换
      进行上行转换（把派生类的指针或引用转换成基类表示）是安全的
      进行下行转换（把基类的指针或引用转换为派生类表示），由于没有动态类型检查，所以是不安全的
    （2）用于基本数据类型之间的转换，如把int转换成char。这种转换的安全也要开发人员来保证
    （3）把空指针转换成目标类型的空指针
    （4）把任何类型的表达式转换为void类型
    注意：static_cast不能转换掉expression的const、volitale或者__unaligned属性。

如果涉及到类的话，static_cast只能在**有相互联系的类型中进行相互转换,**不一定包含虚函数。



## 2) const_cast

在C语言中，const限定符通常被用来限定变量，用于表示该变量的值不能被修改。

而const_cast则正是用于强制去掉这种不能被修改的常数特性，但需要特别注意的是const_cast不是用于去除变量的常量性，而是去除指向常数对象的指针或引用的常量性，**其去除常量性的对象必须为指针或引用。**

**用法：const_cast<type_id> (expression)**
    该运算符用来修改类型的const或volatile属性。除了const 或volatile修饰之外， type_id和expression的类型是一样的。
    常量指针被转化成非常量指针，并且仍然指向原来的对象；
    常量引用被转换成非常量引用，并且仍然指向原来的对象；常量对象被转换成非常量对象。

[例3]一个错误的例子：

```
const int a = 10;
const int * p = &a;
*p = 20;                  //compile error
int b = const_cast<int>(a);  //compile error
```

**在本例中出现了两个编译错误，第一个编译错误是\*p因为具有常量性，其值是不能被修改的；另一处错误是const_cast强制转换对象必须为指针或引用，而例3中为一个变量，这是不允许的！**

[例4]

```
#include<iostream>
using namespace std;
int main(){
  const int a = 10;
  const int * p = &a; 
  int *q;
  q = const_cast<int*>(p);
  *q = 20;
  //fine
  cout <<a<<" "<<*p<<" "<<*q<<endl;
  cout <<&a<<" "<<p<<" "<<q<<endl;
  return 0;
  }
```

在本例中，我们将变量a声明为常量变量，同时声明了一个const指针指向该变量（此时如果声明一个普通指针指向该常量变量的话是不允许的，Visual Studio 2010编译器会报错）。

 

**之后我们定义了一个普通的指针\*q。将p指针通过const_cast去掉其常量性，并赋给q指针。之后我再修改q指针所指地址的值时，这是不会有问题的。**

**最后将结果打印出来，运行结果如下：**
**10 20 20**
**002CFAF4 002CFAF4 002CFAF4**

例5：

usage:

```
#include<iostream>
using namespace std;
const int * Search( const int * a, int n,  int val);
int main(){
	int a[10] = {0,1,2,3,4,5,6,7,8,9};
	int val = 5;
	int *p;
	p = const_cast<int*>(Search(a, 10, val));   
	if(p == NULL)
		cout<<"Not found the val in array a"<<endl;
	else cout<<"hvae found the val in array a and the val = "<<*p<<endl;
    return 0;
    }
const int * Search(const int * a,  int n,  int val){
	int i;
	for(i=0; i<n; i++){
	if(a[i] == val) return &a[i];
 	}
 	return NULL;
 }
```



## 3) reinterpret_cast

在C++语言中，reinterpret_cast主要有三种强制转换用途：***改变指针或引用的类型、将指针或引用转换为一个足够长度的整形、将整型转换为指针或引用类型***。

**用法：reinterpret_cast<type_id> (expression)**
    type-id必须是一个指针、引用、算术类型、函数指针或者成员指针。
    它可以把一个指针转换成一个整数，也可以把一个整数转换成一个指针（先把一个指针转换成一个整数，在把该整数转换成原类型的指针，还可以得到原先的指针值）。
    **在使用reinterpret_cast强制转换过程仅仅只是比特位的拷贝，因此在使用过程中需要特别谨慎！**

例7：

```
int *a = new int;
double *d = reinterpret_cast<double *>(a);
```

在例7中，将整型指针通过reinterpret_cast强制转换成了双精度浮点型指针。

reinterpret_cast可以将指针或引用转换为一个足够长度的整形，此中的足够长度具体长度需要多少则取决于操作系统，如果是32位的操作系统，就需要4个字节及以上的整型，如果是64位的操作系统则需要8个字节及以上的整型。 



## 4) dynamic_cast

 **用法：dynamic_cast<type_id> (expression)**

**（1）其他三种都是编译时完成的，dynamic_cast是运行时处理的，运行时要进行类型检查。**

**（2）不能用于内置的基本数据类型的强制转换。**

**（3）dynamic_cast转换如果成功的话返回的是指向类的指针或引用，转换失败的话则会返回NULL。**

**（4）使用dynamic_cast进行转换的，基类中一定要有虚函数，否则编译不通过。**

​     

```
#include<iostream>
#include<cstring>
using namespace std;
class A
{
   public:
   virtual void f()
   {
       cout<<"hello"<<endl;
       };
};

class B:public A
{
    public:
    void f()
    {
        cout<<"hello2"<<endl;
        };
  
};

class C
{
  void pp()
  {
      return;
  }
};

int fun()
{
    return 1;
}

int main()
{
    A* a1=new B;//a1是A类型的指针指向一个B类型的对象
    A* a2=new A;//a2是A类型的指针指向一个A类型的对象
    B* b;
    C* c;
    b=dynamic_cast<B*>(a1);//结果为not null，向下转换成功，a1之前指向的就是B类型的对象，所以可以转换成B类型的指针。
    if(b==NULL)
    {
        cout<<"null"<<endl;
    }
 
    else
    {
        cout<<"not null"<<endl;
    }
 
    b=dynamic_cast<B*>(a2);//结果为null，向下转换失败
    if(b==NULL)
    {
        cout<<"null"<<endl;
    }
 
    else
    {
        cout<<"not null"<<endl;
    }
 
    c=dynamic_cast<C*>(a);//结果为null，向下转换失败
    if(c==NULL)
    {
        cout<<"null"<<endl;
    }
 
    else
    {
        cout<<"not null"<<endl;
    }
 
    delete(a);
    return 0;
}
```

 

## difference between * and &

C++primer中对 **对象**的定义：**对象**是指一块能存储数据并具有某种类型的内存空间
一个**对象**a，它有**值**和**地址&a**，运行程序时，计算机会为该对象分配存储空间，来存储该对象的值，我们通过该对象的地址，来访问存储空间中的值

**指针**p也是**对象**，它同样有地址&p和存储的值p，只不过，**p存储的数据类型是数据的地址**。如果我们要以p中存储的数据为地址，来访问对象的值，则要在p前加解引用操作符"*",即*p。

对象有常量（const）和变量之分，既然指针本身是对象，那么指针所存储的地址也有常量和变量之分，指针常量是指，指针这个对象所存储的地址是不可以改变的，而指向常量的指针的意思是，不能通过该指针来改变这个指针所指向的对象。

我们可以把引用理解成变量的别名。定义一个引用的时候，程序把该引用和它的初始值绑定在一起，而不是拷贝它。计算机必须**在声明r的同时就要对它初始化**，并且，**r一经声明，就不可以再和其它对象绑定在一起了。**

实际上，你也可以把引用看做是通过一个常量指针来实现的，它只能绑定到初始化它的对象上。

关于指针和引用的对比，可以参看<<more effective C++>>中的第一条条款，引用的一个优点是它一定不为空，因此相对于指针，它不用检查它所指对象是否为空，这增加了效率


比如下面的代码

```cpp
int a,b,*p,&r=a;//正确
r=3;//正确：等价于a=3
int &rr;//出错：引用必须初始化
p=&a;//正确：p中存储a的地址，即p指向a
*p=4;//正确：p中存的是a的地址，对a所对应的存储空间存入值4
p=&b//正确：p可以多次赋值，p存储b的地址
```





# inline

C++ provides an inline functions to reduce the function call overhead. Inline function is a function that is expanded in line when it is called. When the inline function is called whole code of the inline function gets inserted or substituted at the point of inline function call. This substitution is performed by the C++ compiler at compile time. **Inline function may increase efficiency if it is small.**
The syntax for defining the function inline is:

```
inline return-type function-name(parameters)
{
    // function code
}  
```

**Compiler may not perform inlining in such circumstances like:**

- If a function contains a loop. (for, while, do-while)
- If a function contains static variables.
- If a function is recursive.
- If a function return type is other than void, and the return statement doesn’t exist in function body.
- If a function contains switch or goto statement.



# difference between new and malloc

![1672704258718](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1672704258718.png)



|         特征          |              new/delete              |                       malloc/free                        |
| :-------------------: | :----------------------------------: | :------------------------------------------------------: |
|         属性          |                关键字                |                          库函数                          |
|         使用          | 申请空间需要显式填入申请内存的大小。 | 无需显式填入申请的内存大小，new会根据new的类型分配内存。 |
|       内存位置        |              自由存储区              |                            堆                            |
|   返回类型（成功）    |            对象类型的指针            |                          void *                          |
| 返回类型     （失败） |             程序异常退出             |                           NULL                           |
|         扩张          |                  无                  |                         realloc                          |

**堆** 是C语言和操作系统的术语，堆是操作系统所维护的一块特殊内存，它提供了**动态分配**的功能，当运行程序调用malloc()时就会从中分配，调用free()归还内存。那什么是自由存储区呢？

**自由存储区** 是C++中动态分配和释放对象的一个概念，通过new分配的内存区域可以称为自由存储区，通过delete释放归还内存。自由存储区可以是**堆、全局/静态存储区**等，具体是在哪个区，主要还是要看new的实现以及C++编译器默认new申请的内存是在哪里。但是基本上，很多C++编译器默认使用堆来实现自由存储，运算符new和delete内部默认是使用malloc和free的方式来被实现，说它在堆上也对，说它在自由存储区上也正确。因为在C++中new和delete符号是可以重载的，我们可以重新实现new的实现代码，可以让其分配的内存位置在静态存储区等。而malloc和free是C里的库函数，无法对其进行重载。

# malloc

```int *p = NULL;
#include<malloc.h>

int *p = NULL;
int n = 10;
p = (int *)malloc(sizeof(int)*n);
```



# Q&A 

- **malloc的内存可以用delete释放吗？**

可以，但是一般不这么用。malloc/free是c语言中的函数，c++为了兼容c保留下来这一对函数。简单来说，new 可以理解为，先执行malloc来申请内存，后调用构造函数来初始化对象；delete是先执行析构函数，后使用free来释放内存。

若先new再使用free来释放空间的话，可能会出现一些错误。而先使用malloc，再使用delete的话没有问题。

- **malloc出来20字节内存，为什么free不需要传入20呢，不会产生内存泄漏吗？**

因为不能保证程序员使用free时传入的参数是和malloc一致，从而导致内存泄露等问题。现在free的解决方式是让free函数自己确定要释放多少内存，可以使用的方式是在申请内存时多申请一些空间来存储内存大小，在free时再获取这个大小进行释放。

- **new和delete以及new[]和delete[]一定要配对使用吗**

```cpp
#include <stdlib.h>
#include <iostream>
using namespace std;

int main() {
    int *pint = new int(5);
    delete[] pint;
    int *pinta = new int[4];
    delete pinta;
    cout << "success" << endl;
    return 0;
}
程序输出：
success
```

这段代码即使不配对使用也会正常运行，这是为什么呢，因为int是内置类型，new[]和delete[]在配合int使用时知道int是内置类型，不需要析构函数，所以也就不需要多4个字节来存放数组长度，只需要直接操作内存即可。

### 总结

当类型为int,float等内置类型时，new、delete、new[]、delete[]不需要配对使用，当是自定义类型时，new、delete和new[]、delete[]才需要配对使用，当然我们平时编程过程中，为了代码可读性以及为了养成编程良好习惯最好确保所有情况都配对使用。



# using

In C++11, the `using` keyword when used for `type alias` is identical to `typedef`.

**the difference between `using `and `typedef`:**

The **using** syntax has an advantage when used within templates. If you need the type abstraction, but also need to keep template parameter to be possible to be specified in future. You should write something like this.

```cpp
template <typename T> struct whatever {};

template <typename T> struct rebind
{
  typedef whatever<T> type; // to make it possible to substitue the whatever in future.
};

rebind<int>::type variable;

template <typename U> struct bar {
    typename rebind<U>::type _var_member;
}
```

But **using** syntax simplifies this use case.

```cpp
template <typename T> using my_type = whatever<T>;
my_type<int> variable;
template <typename U> struct baz {
    my_type<U> _var_member;
}
```



# std::back_insert_iterator

`std::back_insert_iterator` is a [*LegacyOutputIterator*](https://en.cppreference.com/w/cpp/named_req/OutputIterator) that appends elements to a container for which it was constructed. The container's `push_back()` member function is called whenever the iterator (whether dereferenced or not) is assigned to. Incrementing the `std::back_insert_iterator` is a no-op.

```
#include <iostream>
#include <iterator>
#include <algorithm>
#include <vector>
 
int main()
{
  std::vector<int> v;
  std::generate_n(
    std::back_insert_iterator<std::vector<int>>(v), 
    // C++17: std::back_insert_iterator(v)
    10, [n=0]() mutable { return ++n; }             
    // or use std::back_inserter helper
  );
 
  for (int n : v)
    std::cout << n << ' ';
  std::cout << '\n';
}
```

Output:

```
1 2 3 4 5 6 7 8 9 10
```



# std::transform

  transform() 可以将函数应用到序列的元素上，并将这个函数返回的值保存到另一个序列中，它返回的迭代器指向输出序列所保存的最后一个元素的下一个位置。

  这个算法有一个版本和 for_each() 相似，可以将一个一元函数应用到元素序列上来改变它们的值，但这里有很大的区别。for_each() 中使用的函数的返回类型必须为 **void**，而且可以通过这个函数的引用参数来修改输入序列中的值；而 transform() 的二元函数必须返回一个**值**，并且也能够将应用函数后得到的结果保存到另一个序列中。

  不仅如此，输出序列中的元素类型可以和输入序列中的元素类型不同。对于 for_each()，函数总是会被应用序列的元素上，但对于 transform()，这一点无法保证。

  第二个版本的 transform() 允许将二元函数应用到两个序列相应的元素上，但先来看一下如何将一元函数应用到序列上。在这个算法的这个版本中，它的前两个参数是定义输入序列的输入迭代器，第 3 个参数是目的位置的第一个元素的输出迭代器，第 4 个参数是一个二元函数。这个函数必须接受来自输入序列的一个元素为参数，并且必须返回一个可以保存在输出序列中的值。

```
std::vector<double> deg_C {21.0, 30.5, 0.0, 3.2, 100.0};
std::vector<double> deg_F(deg_C.size());
std::transform(std::begin(deg_C), std::end(deg_C), std:rbegin(deg_F),[](double temp){ return 32.0 + 9.0*temp/5.0; });
//Result 69.8 86.9 32 37.76 212
```

这个 transform() 算法会将 deg_C 容器中的摄氏温度转换为华氏温度，并将这个结果保存到 deg_F 容器中。为了保存全部结果，生成的 deg_F 需要一定个数的元素。因此第三个参数是 deg_F 的开始迭代器。通过用 back_insert_iterator 作为 transform() 的第三个参数，可以将结果保存到空的容器中：

```
std::vector<double> deg_F; // Empty container
std::transform(std::begin(deg_C), std::end(deg_C),std::back_inserter(deg_F),[](double temp){ return 32.0 + 9.0* temp/5.0; });
// Result 69.8 86.9 32 37.76 212
```

用 back_insert_iterator 在 deg_F 中生成保存了操作结果的元素；结果是相同的。第三个参数可以是指向输入容器的元素的迭代器。例如：

```
纯文本复制
std::vector<double> temps {21.0, 30.5, 0.0, 3.2, 100.0}; // In Centigradestd::transform(std::begin (temps), std::end(temps), std::begin(temps),[](double temp){ return 32.0 + 9.0* temp / 5.0; });// Result 69.8 86.9 32 37.76 212
```



# std::[vector](https://cplusplus.com/reference/vector/vector/)::rend

 Returns a *reverse iterator* pointing to the theoretical element preceding the first element in the [vector](https://cplusplus.com/vector) (which is considered its *reverse end*).

The range between [vector::rbegin](https://cplusplus.com/vector::rbegin) and `vector::rend` contains all the elements of the [vector](https://cplusplus.com/vector) (in reverse order).

```
// vector::rbegin/rend
#include <iostream>
#include <vector>

int main ()
{
  std::vector<int> myvector (5);  // 5 default-constructed ints

  int i=0;

  std::vector<int>::reverse_iterator rit = myvector.rbegin();
  for (; rit!= myvector.rend(); ++rit)
    *rit = ++i;

  std::cout << "myvector contains:";
  for (std::vector<int>::iterator it = myvector.begin(); it != myvector.end(); ++it)
    std::cout << ' ' << *it;
  std::cout << '\n';

  return 0;
}
```

`output: 5 4 3 2 1`



# override **specifier**

The `override` keyword serves two purposes:

1. It shows the reader of the code that "this is a virtual method, that is overriding a virtual method of the base class."
2. The compiler also knows that it's an override, so it can "check" that you are not altering/adding new methods that you think are overrides.

To explain the latter:

```cpp
class base
{
  public:
    virtual int foo(float x) = 0; 
};


class derived: public base
{
   public:
     int foo(float x) override { ... } // OK
};

class derived2: public base
{
   public:
     int foo(int x) override { ... } // ERROR
};
```

In `derived2` the compiler will issue an error for "changing the type". Without `override`, at most the compiler would give a warning for "you are hiding virtual method by same name".