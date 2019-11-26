### 单个源文件生成可执行程序
____
下面是一个保存在*helloworld.cpp*中的一个简单的<kbd>C++</kbd>程序的代码：
```C++
/* helloworld.cpp */
#include<iostream>
using namespace std;
int main(int argc, char* argv[]){
	cout<<"hello, world!"<<endl;
	return 0;
}
```
程序使用定义在*iostream*头文件中的*cout*，向标准输出写入一个简单的字符串。该代码可以用以下命令编译为可执行文件：
```bash
$ g++ helloworld.cpp
```
编译器<kbd>g++</kbd>通过检查命令行中指定的文件的后缀名可以识别其为<kbd>C++</kbd>源文件代码。编译器默认的动作：**编译源代码文件生成对象文件（object file），链接对象文件和** ***libstdc++*** **库中的函数得到可执行程序。然后删除对象文件**。由于命令行中未指定可执行文件的文件名，编译器采用默认的 *a.out*。程序可以这样来运行：
```bash
$ ./a.out
hello, world!
```
更普遍的做法是通过 `-o`选项来指定可执行文件的文件名，下面的命令将产生名为*helloworld*的可执行文件：
```bash
$ g++ helloworld.cpp -o helloworld
```
在命令行中输入程序名可使之运行：
```bash
$ ./helloworld
hello, world!
```
*程序g++是将gcc默认语言设为C++的一个特殊版本，链接时它自动使用C++标准库而不用C标准库。*
通过遵循源码的命名规范并指定对应库的名字，用*gcc*来编译链接<kbd>C++</kbd>程序是可行的，如下例所示：
```bash
$ gcc helloworld.cpp -lstdc++ -o helloworld
```
选项 `-l(ell)` 通过自行添加前缀 `lib` 和后缀 `.a`，将跟随它的名字`stdc++`变换为库的名字`libstdc++.a`。而后它将在标准库路径中查找该库。gcc的编译过程和输出文件与g++是完全相同的。
在大多数系统中，*GCC*安装时会安装一个名为`C++`的程序。如果被安装，它和`g++`是等同的。如下例所示，用法也是一致的：
```bash
$ c++ helloworld.cpp -o helloworld
 ```
 ### 多个源文件生成可执行文件
 ---
 如果有多余一个的源码文件在`g++`命令中指定，它们都将被编译并被链接成一个单一的可执行文件。下面是一个名为*speak.h*的头文件；它包含一个仅含有一个函数的类的定义：
 ```C++
 #include <iostream>
 class Speak{
 	public:
 		void sayHello(const char*);
 }
 ```
 下面列出的是文件*speak.cpp*的内容，包含`sayhello()`函数的函数体：
 ```C++
 #include "speak.h"
 void speak::sayHello(const char *str){
 	std::cout<<"Hello "<<std<<"\n";
 }
 ```
 文件hellospaek.cpp内是一个使用Speak类的程序：
 ```C++
 #include "speak.h"
int main(int argc,char *argv[]){
	Speak speak;
	speak.sayHello("world");
	return 0;
}
```
下面这条命令将上述两个源码文件编译链接成一个单一的可执行程序：
```bash
$ g++ hellospeak.cpp speak.cpp -o hellospeak
```
PS: 这里说一下为什么在命令里没有提到“`spoeak.h`”该文件(原因是：在“`speak.cpp`中包含有“ `#include "speak.h"`”这句代码，他的意思是在搜索系统头文件目录之前将先在当前目录中搜索文件“`speak.h`”。而“`speak.h`”正在该目录中，并不用在在命令中指定了)。
### 源文件生成对象文件
---
选项 `-c` 用来告诉编译器编译源代码但是不要执行链接，输出结果为对象文件。文件默认名与源码文件名相同，只是将其后缀变为 `.o`。例如，下面的命令将编译源码文件 `hellospeak.cpp` 并生成对象文件 `hellospeak.o`：
```bash
$ g++ -c hellospeak.cpp
```
命令g++也能识别`.o`文件并将其作为输入文件传递给链接器。下面的命令将编译源码文件为对象文件，并将其链接成单一的可执行程序：
```bash
$ g++ -c hellospeak.cpp 
$ g++ -c speak.cpp
$ g++ hellospeak.o speak.o -o hellospeak
```
选项`-o`不仅仅能用来命名可执行文件。它也可以用来明明编译器输出的其他文件。例如：除了中间的对象文件有不同的名字外，下列命令将生成和上面完全相同的可执行文件：
```bash
$ g++ -c hellospeak.cpp -o hspk1.o
$ g++ -c speak.cpp -o hspk2.0
$ g++ hspk1.o hspk2.o -o hellospeak
```
编译预处理
---
选项`-E`使`g++`将源代码用编译器预处理器处理后不再执行其他动作。下面的命令预处理源码文件*helloworld.cpp*并将结果显示在标准输出中：
```bash
$ g++ -E helloworld.cpp
```
本文前面所列出的*helloworld.cpp*的源代码，仅仅有六行，而且该程序除了显示一行文字之外什么都不做，但是，预处理后的版本将超过1200行。这主要是因为头文件*iostream*被包含了进来，而且它又包含了其他的头文件，除此之外，还有若干处理输入和输出的类的定义。
预处理过的文件的GCC后缀为`.ii`,它可以通过`-o` 选项来生成，例如：
```bash
gcc -E helloworld.cpp -o helloworld.ii
```
### 生成汇编代码
---
选项`-S` 指示编译器将程序编译成汇编语言，输出汇编语言代码而后结束。下面的命令将由`C++`源码文件生成汇编语言文件 *helloworld.s*：
```bash
$ g++ -S helloworld.cpp
```
生成的汇编语言依赖于编译器的目标平台。
### 创建静态库
---
静态库是编译器生成的一系列对象文件(.o)的集合。链接一个程序时用库中的对象文件还是目录中的对象文件都是一样的。库中的成员包括普通函数、类定义、类的对象实例等等。静态库的另一个名字叫归档文件（archive），管理这种归档文件的工具叫`ar`。
在下面的例子中，我们先创建两个对象模块，然后利用其生成静态库。
头文件`say.h`包含函数`sayhello()`的原型和类`Say`的定义：
```C++
/* say.h */
#include <iostream>
void sayhello(void);
chass Say{
	private:
		char *string;
	public:
		Say(char * str){
			string= str;
		}
		void sayThis(const char *str){
			std::cout<<str<<"from a static library\n";
		}
		void sayString(void);
}
```
下面的文件`say.cpp`是我们要加入静态库中的两个对象文件之一的源码。它包含Say类中`sayString()`函数的定义体；类Say的一个实例 librarysay 的声明也包含在内：
```C++
/* say.cpp */
#include "say.h"
void Say::sayString(){
	std:cout<<string<<endl;
}
Say librarysay("Library instance of Say");
```
源码文件*sayhello.cpp*是我们要加入静态库中的第二个对象文件的源码。它包含函数`sayhello()`的定义：
```C++
#include "say.h"
void sayhello(){
    std::cout<<"hello from a static library\n";
}
```
下面的命令序列将源码文件编译成对象文件，命令`ar`将其存进库中：
```bash
$ g++ -c sayhello.cpp
$ g++ -c say.cpp
$ ar -r libsay.a sayhello.o say.o
```
程序`ar` 配合参数`-r` 创建一个新库`libsay.a`并将命令行中列出的对象文件插入。采用这种方法，如果库不存在的话，参数`-r`将创建一个新的库，而如果库存在的话，将用新的模块替换原来的模块。
下面是主程序 `saymain.cpp`,它调用库`libsay.a`中的代码：
```C++
#include "say.h"
int main(int argc,char *argv[]){
	extern Say librarysay;
	Say localsay =Say("Local instance of Say");
	sayhello();
	librarysay.sayThis("howdy");
	librarysay.sayString();
	localsay.sayString();
	return 0;
}
```
该程序可以用下面的命令来编译和链接：
```bash
$ g++ saymain.cpp libsay.a -o saymain
```
程序运行时，产生下面的输出：
>hello from a static library
howdy from a static library
Library instance of Say
Local instance of Say

ps：如果一个文件夹下有多个cpp文件需要编译的话，除了采用makefile的方式之外，还可以使用“g++ *.cpp -o hello”,“hello为编译生成的可执行文件的名字”，编译时要确保cpp文件和他们各自所引用的头文件在同一个目录下。
