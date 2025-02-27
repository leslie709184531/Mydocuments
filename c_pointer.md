```c
int i;
int *pi = &i;
char c;
char *pc = &c;
```

这里的&是取地址运算符（Address Operator），&i表示取变量i的地址，int *pi = &i;表示定义一个指向int型的指针变量pi，并用i的地址来初始化pi。我们讲过全局变量只能用常量表达
式初始化，如果定义int p = i;就错了，因为i不是常量表达式，然而用i的地址来初始化一个
指针却没有错，因为i的地址是在编译链接时能确定的，而不需要到运行时才知道，&i是常量表
达式。后面两行代码定义了一个字符型变量c和一个指向c的字符型指针pc，注意pi和pc虽然是
不同类型的指针变量，但它们的内存单元都占4个字节，因为要保存32位的虚拟地址，同理，
在64位平台上指针变量都占8个字节。

这里的 *号是指针间接寻址运算符（Indirection Operator），
*pi表示取指针pi所指向的变量的
值，也称为Dereference操作，指针有时称为变量的引用（Reference），所以根据指针找到变
量称为Dereference。
&运算符的操作数必须是左值，因为只有左值才表示一个内存单元，才会有地址，运算结果是指
针类型。
*运算符的操作数必须是指针类型，运算结果可以做左值。所以，如果表达式E可以做
左值，*&E和E等价，如果表达式E是指针类型，&*E和E等价。
指针之间可以相互赋值，也可以用一个指针初始化另一个指针，例如：

```c
int *ptri = pi;
```
或者：
```c
int *ptri;
ptri = pi;
```
表示pi指向哪就让ptri也指向哪，本质上就是把变量pi所保存的地址值赋给变量ptri。
用一个指针给另一个指针赋值时要注意，两个指针必须是同一类型的。在我们的例子
中，pi是int *型的，pc是char *型的，pi = pc;这样赋值就是错误的。但是可以先强制类型转
换然后赋值：
```fc
pi = (int *)pc;
```



### 指针与结构体 ###
首先定义一个结构体类型，然后定义这种类型的变量和指针：

```c
struct unit {
 char c;
 int num;
};
struct unit u;
struct unit *p = &u;
```
要通过指针p访问结构体成员可以写成 (\*p).c和 (\*p).num，为了书写方便，C语言提供了->运算
符，也可以写成 **p->c和p->num **

