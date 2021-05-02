<br>

<div align="center">
    <img src="logo.jpg" width="200px">
</div>

<br>

- **C和C++的区别？**
C++强调封装，继承和多态。相比于C，它增加了classes, templates以及exceptions这些部分。在标准库上，C只有20多个标准库文件，但C++有87个，事实上，C++的标准库功能比C要复杂的多。但是C也并不是完全没有优点。它编译速度快，容易学习，较少的更新标准，技术栈迭代慢。而且c语言也是可以通过使用struct和宏来近似的实现oop和gp(泛型编程)的。从我自己听的角度来讲，感觉目前c语言的主要应用领域在嵌入式开发，驱动程序开发这些地方。

- **Include file的时候使用<>和””的区别？** 前者是从标准库路径查找，后者则是当前的工作路径。
-  **C++编译过程中的四个阶段**
a)	预处理阶段：我理解的主要是处理一些#开头的程序内容，例如#ifdef, #include,#define等，事实上这个过程之后生成的预编译文件会比较大。主要是include导致的我认为。删除所有的注释，添加行号和文件标识
b)	编译阶段：编译器在这个过程中会对代码进行检查优化，指出语法错误等各种编译错误，之后生成汇编代码
c)	汇编阶段：将上一步产生的代码逐行转换成机器码。
d)	链接阶段：将上一阶段中编译器产生的各种目标文件链接起来，将未定义标识符的引用全部替换成正确的地址。主要包含静态链接和动态链接两种情形。相比较来说动态链接生成的可执行文件小一些，但是会损耗一些性能。
-	**C++中的几个存储区：**
a)	栈：通常内部存储的是局部变量和函数参数等，主要由编译器在需要的时候分配，默认值是1Mb。
b)	堆：主要是new或者malloc这种函数来申请，由程序段控制。
c)	全局区（静态区）：存储函数体外的变量，以及任意位置带static关键字的变量。
d)	常量区：里面存放的是常量，不允许修改。
-	**堆和栈的区别**
a)	管理方式不同：栈是由编译器自动管理有专门的机器指令支持压栈和出栈操作，因此速度更快。而堆内存的申请和释放由程序员控制，可能会出错。
b)	空间大小不同：一般栈空间比较小，小于1MB。
c)	相比较于栈，堆由于大量使用new和delete很容易产生大量的内存碎片。而栈不会产生碎片空间连续。
d)	堆是链表，栈是连续的内存区域。它向低地址扩展（向下扩展），堆向上扩展。
-	**深拷贝和浅拷贝的区别**
浅拷贝指仅仅是指向被复制的内存的地址，如果原地址中对象被改变，那么浅复制出来的对象也会相应的改变。
而深复制指的是在计算机中开辟出一块新的内存地址用于存放复制的对象。
-	**C++哪些成员函数不能被继承？**
a)	构造函数（Copy构造函数）：对于子类来说并不会继承父类的构造函数，如果子类缺省构造函数，唯一的结果是会去调用父类的无参构造函数。当然如果子类定义了构造函数，仍旧会先去调用父类的无参构造函数。如果父类没有定义无参构造函数，子类也没有显式的去调用父类的有参构造函数则会导致出错。
b)	析构函数：析构函数也不会被继承，只是子类的析构函数中会调用父类的析构函数。
c)	赋值运算符重载函数也不会被继承。只是会被调用。
-	**哪些函数不能被声明为虚函数**
a)	非成员函数：只能被重载，不能被继承。虚函数主要还是用在继承中实现多态，非成员函数在编译期间就定了
b)	构造函数：要想使用虚函数必须具备虚函数表，但是虚函数表要在对象实例化之后才能够调用。在构造函数运行期间，还没有为虚函数分配空间，因此是无法调用虚函数的。
c)	静态成员函数：对每个类只有一份，所有对象共享一份代码，虚函数必须根据对象来选择调用虚函数。
d)	内联成员函数：它在代码中直接展开来减少花费的代价。它在编译的时候就会被展开，因此无法支持运行时多态
e)	友元函数：C++不支持友元函数的继承。实质上友元函数并不属于类的成员函数。
-	**Define和const的区别**
a)	Define定义的常量不包含类型，而const定义的常量有类型。
b)	Define定义的宏变量会在预处理阶段进行替换，可能会有多个拷贝，const在编译的时候就确定其数值，只有一个拷贝。
c)	Define定义的常量不能用指针指向，但是const定义的常量可以用指针去指向。
d)	Define可以定义简单的函数。但是一般应该使用inline去替换它
-	**union和struct的区别：**
a)	结构体中的每个成员都有自己独立的地址。他们同时存在，共同体所有的成员占同一段内存，不能同时存在。
b)	结构体的sizeof是所有成员长度的综合，union是最大值。
-	**指针与数组**
a)	指针与数组之间是有关联性的，例如一个指针可以指向数组，其实就是指向了首地址。可以通过指针访问任意维度数组中的数据。通过指针的几次解引用。例如*(*(p＋1)＋2)表示取a[1][2]的内容；
b)	指针与数组之间的区别更大，数组中存放实际的值，指针存放的是地址数值。Sizeof大小不同。指针固定是4.但是数组作为参数传递到函数中的时候会退化成为指针。

-       **解释一下extern C在c++代码中的作用**
一般extern这个关键字是在本文件中要使用其他文件中的变量的时候使用Extern这个变量声明一下。之所以要使用extern C是因为，作为面向对象的语言C++中包含函数重载功能，这也就意味着c++可能会对函数名做修改，而面向过程的语言C中并不包含重载，以及名称改变。为了解决这样的名字匹配问题，c++中可以使用extern C加{}的形式来实现c++和c的混合编程。
-	**C++中的ifndef/define/endif作用**是预编译头文件保护符，它保证即使文件被多次包含也只会被定义一次。
-	**指针和引用的区别**
二者都提供了对数据的间接访问，但是二者之间有比较大的差别。主要体现在，指针定义的时候可以不进行初始化，但是引用则必须初始化，也就是必须和一个对象绑定。他们之间赋值的意义是不同的，对于指针的赋值代表指针指向其他对象，但是对于引用的赋值行为则会表示为引用对象数值的变化。指针之间存在类型转换，是比较常见的场景，尤其是void*指针和其他指针之间，const类型转换主要是const_cast取消const。

- **空指针与悬垂指针之间的区别**
空指针指的是赋值为null的指针，悬垂指针指的是指向曾经存在过对象的指针，但是当前该对象已经不存在了。对二者的使用都会导致程序的不稳定和崩溃。但是相比较于悬垂指针的崩溃，空指针是一种可预料的崩溃。
-	**malloc,free和new delete的区别**
malloc和free是标准库函数，但是new 和delete是操作符，是可以被重定义的，他们都可以用于动态申请和释放堆内存空间。对于内置数据类型而言，二者之间的区别不大。但是对于类类型而言，二者之间区别很大，new会调用对应的构造函数，delete会调用析构函数。由于malloc和free是库函数，它不在编译器的控制之内，因此无法执行类的初始化或者析构方法。
malloc中(lock(),malloc_internal(size),unlock) 
free中lock(),free_intertal(“free”,header)
这个地方比较疑惑的是为什么free的时候不必指定Free大小，而malloc就必须指明大小，于是看了下源码，malloc的时候size会+一个size of(struct allocation_header)，而free的时候会先get这个header,计算大小释放
- **面向对象的基本概念是什么,三个基本特征是什么？**
面向对象的基本概念是，类，对象和继承。三个基本特征是，封装继承和多态。封装主要是将低层次的元素组合起来形成新的，更高级别抽象实体的技术。继承主要包括实现继承，可视继承和接口继承三类。多态指的是子类类型指针赋值给父类类型的指针。
- **C++默认类中包括哪些成员函数** 构造，析构，copy构造以及copy assignment。
- **为什么基类的析构函数要是虚函数？**
主要是为了避免在实现多态的时候，在基类操作派生类的时候，避免析构只析构基类却不析构派生类的情况发生。如果不将析构函数定义为虚函数，那么会导致只调用基类的析构函数，而无法调用派生类的析构函数的情况，进而导致资源泄漏。
- **重载与覆盖的概念与区别**
覆盖指的是派生类中重新定义基类虚函数，重载指的是在相同作用域中存在多个同名的函数，这些函数的参数表不同。重载的概念不属于面向对象编程。编译器会根据不同形参表对同名函数的名称做修饰，然后这些同名函数就成了不同的函数。重载在编译时确定，而覆盖会在运行时确定。
- **C++如何阻止一个类被实例化** 
将类定义为抽象类，或者将构造函数放到private中，它的作用是进制在类外部创建类对象，只允许类内创建对象。
- **Main函数执行之前会执行什么**
全局对象的构造函数会在main函数之前执行。事实上可以用_onexit注册一个函数来在main函数之后执行
- **Static关键字的作用？**
static修饰的变量位于静态区，该变量内存只会被分配一次，因此值在下次调用的时候仍然维持上次的值。Static可以被用来修饰函数内的局部变量，它不会随函数生命期结束而消亡。下次调用的时候仍旧维持原数值。Static修饰的函数由于不接受this指针，因此只能访问static成员变量。Static成员变量只能被该模块内其他函数调用，不能被外部调用。事实上static很大的一个作用是限制作用域。
- **delete和delete []的区别？**
delete只会调用一次析构函数，而delete[]会调用每个成员的析构函数。当delete操作符用于数组的时候，它为每个数组元素调用一次析构函数。事实上他们的主要区别在于类类型上，也就是说对于内置类型来说,delete[]和delete没什么区别，主要是内部数据类型没有析构函数。
- **C++多态的实现原理** 
每一个类都有一个虚表，这个表由虚函数指针指着，这个虚表是可以被继承的，虚表中的项取决于虚函数的数量，几类的虚表会被子类所继承，如果重写的话，虚表对应项的地址会被改变成子类函数地址。
- **函数调用的过程**
 参数入栈，函数跳转，保护现场，恢复现场。
- **C++编译器常见的优化**
a)	常量替换，例如int a=2; int b=1;return b可能会直接变为return 2
b)	无用代码消除
c)	表达式预计算和子表达式提取常量的乘法会在编译阶段就计算完毕，相同的子表达式也会被合并
d)	为了避免拷贝消耗，可能返回值会被优化成为一个引用并放到函数参数里例如RVO, NRVO
- **mangling:** 指的是编译器给函数名，函数变量等添加很多的描述信息到名称上来传递更多的消息，例如函数重载的时候就会用到这个技术
- **成员函数指针与void*指针**
显然是不能互换的，void*指针与成员对象指针大小未必相同。在C++标准中，规定void*指针与普通函数指针，类静态成员函数指针大小相同，所以他们可以转换，但是成员函数不是的，我理解的，成员函数起码得操纵对象，但是对象还不知道在哪，一个指针没什么作用
- **静态链接与动态链接的实现思路？**
静态库：任意个.o文件的集合，程序link的时候，被复制到output文件，这个静态库文件是静态编译出来的，索引和实现都在其中，可以直接加载到内存里执行。
动态库：包含一个或多个已经被编译，链接并与使用他们的进程分开存储的函数，在编译的时候并不会直接连接到目标代码中，而是程序运行时才被载入，不同程序调用相同的库，那么内存里只要有一份该共享库的实例。
静态链接：静态连接就是将多个目标文件组合在一起形成一个可执行文件。主要包含两个部分，一个是空间与地址的分配，二是符号解析和重定位：
		空间与地址的分配：扫描所有输入目标文件，获取各个段的长度属性和位置，并将所有目标文件中的符号定义和引用收集起来，统一构造一个全局符号表，方便后续的合并，之后会建立映射关系。映射关系就是可执行文件与进程虚拟地址空间之间的映射
动态链接：基本分为三步，启动动态链接器，装在所有需要共享的对象，最后重定位和初始化。

- **内部链接与外部链接**
内部链接：如果一个名称对于它的编译单元是局部的，并且在链接的时候不会与其他编译单元中同样的名字起冲突那这个名称就是内部链接。
外部链接：一个多文件程序中，一个实体可以在链接的时候与其他编译单元交互，那么这个实体就有外部链接，也就是说如果一个.cpp文件中向其他编译单元.cpp提供定义，让其使用的函数或者变量就拥有外部链接。
- **模板与模板的特性？**
模板主要分为函数模板和类模板，其根本目的是将类型“参数化”，实现编译时的“动态化”，避免代码重写。
一般写模板不会拆分为.h和.cpp，而是全部放在头文件里面，都否则会发生编译错误，因为模板函数所在的cpp不能直接编译为相应的二进制代码，因为它无法得知模板参数是什么，它需要一个实例化的过程，也就是树哦，如果cpp里面没有显式的调用模板函数的语句，就不会生成真正拥有确切类型的类定义，也就不会生成二进制代码。
- **移动语义与完美转发：**
我理解的移动语义主要是为了避免或者减少复制构造的，主要是在没有必要的时候避免复制。使用移动构造函数，使用右值的方式来减少开支。不必在内存中创建副本再消除。左值转右值可以用move，无条件转，但会导致move的对象不能再做修改。
完美转发主要是调用forward<T>来实现右值的传递，它可以保留参数的左右值类型。
	
-  **函数调用**
a)	每个函数都有一个自己的栈帧，我理解的就是栈中的一截空间
b)	函数的调用与几个寄存器有关，主要是ebp(指向栈帧底部)，esp(指向栈帧顶部)，eax(保存函数返回值)
函数的调用分为入栈和出栈两步：
a)	入栈：将调用者函数的ebp入栈，将调用函数的栈顶指针赋值给被调用函数的ebp，按照从右到左的顺序将被调用函数的参数入栈，按照声明的顺序将被调用函数的局部变量入栈，将调用函数的下一个指令地址作为返回地址入栈，将被调用函数的第一条指令地址赋值给eip寄存器，开始执行被调用函数指令
b)	出栈：将函数返回值存入eax存储器，执行leave指令，将ebp赋值给esp，将esp所指向的栈顶，上一层函数的Esp赋值给ebp，执行ret指令，修改程序计数器，跳回返回地址继续执行