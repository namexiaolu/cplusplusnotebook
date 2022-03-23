# 这是ceshi分支

# QT:

## 信号与槽实现原理？

moc源编译器，编译c++程序时，类中存在QOBJECT宏的话，就会生成moc开头的一些cpp文件。
里边包含信号和槽函数实现所需要的变量以及函数定义。

触发信号的是emit 

moc查找头文件中的signals，slots，标记出信号和槽
将信号槽信息存储到类静态变量staticMetaObject中，并且按声明顺序进行存放，建立索引。
当发现有connect连接时，将信号槽的索引信息放到一个map中，彼此配对。
当调用emit时，调用信号函数，并且传递发送信号的对象指针，元对象指针，信号索引，参数列表到active函数
通过active函数找到在map中找到所有与信号对应的槽索引
根据槽索引找到槽函数，执行槽函数。

    https://zhuanlan.zhihu.com/p/347456731

## 信号与槽传参参数区别？

Qt规定信号和槽的参数类型要对应，信号可以比槽的参数多
<<<<<<< HEAD
   1. 当信号的参数和槽函数的参数个数一致时，参数类型需要严格一致。
      connect(this, SIGNAL(iSignal(int)), this, SLOT(iSlot(int)));
      发射信号：emit iSignal(5);
   
   2. 信号和槽函数保护的参数数量不同，只能是信号的参数多于槽函数，前边的类型必须一致，多余的会被忽略。
=======

      1. 当信号的参数和槽函数的参数个数一致时，参数类型需要严格一致。
         connect(this, SIGNAL(iSignal(int)), this, SLOT(iSlot(int)));
         发射信号：emit iSignal(5);

      2. 信号和槽函数保护的参数数量不同，只能是信号的参数多于槽函数，前边的类型必须一致，多余的会被忽略。
>>>>>>> db0fcfd4c181e1e27b706149e73e23331d30f5c8

    connect(this, SIGNAL(iSignal(int, float)), this, SLOT(iSlot(int)));
    发送信号：emit iSignal(5, 0.3); 只会接受5；

## 自己实现一个类支持信号与槽，需要注意什么？

引入qobject宏


## QT的表格怎么删除？

先设置选中一行的模式，然后点击某行，获取这一行的行号，然后删除即可

tableWidget->setSelectionBehavior ( QAbstractItemView::SelectRows); //设置选择行为，以行为单位
tableWidget->setSelectionMode ( QAbstractItemView::SingleSelection); //设置选择模式，选择单行
 tableWidget->removeRow(rowIndex); 删除选择的整行



# C++：

## const

const关键的作用:
(1) const定义常量
const floatpi= 3.14; :其值不能被改变
(2) const与指针。
常量指针和指针常量
(3) const与函数
const int 、func(const int: &a )const;
a.修饰形参时，形参不能被修改
b.修饰成员函数时，函数体内不能修改成员变量的值
(4) const对象const. Point p;常量对象
const对象只能调用const成员函数，不能调用普通成员函数
普通对象既可以调用const成员函数也可以调用普通成员函数

## explicit？

避免隐式转换

explicit关键字只能用于类内部的构造函数声明上，而不能用在类外部的函数定义上。尽量要使用explict，可以避免隐式转换。
    https://www.cnblogs.com/likebeta/archive/2012/07/31/explicit.html

## strlen和sizeof区别？

    sizeof与strlen是有着本质的区别，sizeof是求数据类型所占的空间大小,而strlen是求字符串的长度，字符串以/0结尾。区别如下:
    (1) sizeof是一个C语言中的一个单目运算符，而strlen是一个函数，用来计算字符串的长度。
    (2)sizeof求的是数据类型所占空间的大小，而strlen是求字符串的长度

## define和const区别？

宏定义是字符替换，没有数据类型的区别，同时这种替换没有类型安全检查，可能产生意想不到的结果；
const常量是常量的声明，有类型区别，需要在编译阶段进行类型检查
    https://www.runoob.com/note/12963

## const和static有什么作用？

类中的操作
const 定义的常量在超出其作用域之后其空间会被释放，而 static 定义的静态常量在函数执行后不会释放其存储空间。
    https://blog.csdn.net/shihuboke/article/details/79286669

## static修饰类成员方法时有什么用？

static关键字最基本的用法是：

被static修饰的变量属于类变量，可以通过类名.变量名直接引用，而不需要new出一个类来
被static修饰的方法属于类方法，可以通过类名.方法名直接引用，而不需要new出一个类来
被static修饰的变量，被static修饰的方法是类的静态资源，是类实例间共享的，也就是说，一处变，处处变。
    https://blog.csdn.net/zhizhengguan/article/details/81183602#:~:text=2.%20%E5%9C%A8%20C,%E8%80%83%E8%99%91%E4%BD%BF%E7%94%A8%20static%EF%BC%89

## 类中有多少默认的方法？8种

默认构造函数
默认拷贝构造函数
默认拷贝赋值运算符
默认移动构造函数
默认移动赋值运算符
析构函数
    https://blog.csdn.net/JMW1407/article/details/108785842

## 继承

公有继承

私有继承

保护继承

## 构造函数的初始化顺序？

1. 首先构造虚拟基类，任何虚拟基类的构造函数按照它们被继承的顺序构造；
2. 其次构造非虚拟基类，任何非虚拟基类的构造函数按照它们被继承的顺序构造；
3. 接着构造成员对象，任何成员对象的构造函数按照它们声明的顺序调用；
4. 最后调用类自身的构造函数；
   https://blog.csdn.net/qq_30835655/article/details/66971183

### 为什么引入虚函数

为了实现一种接口的效果。

很多情况下由基类生成对象是不合理的。

含有纯虚函数的类称为抽象类。步能被实例化。如果子类没有实现纯虚函数，他也是一个抽象类。

## 虚函数和纯虚函数怎么理解？

虚函数在基类中可以有定义。在子函数中重写。
纯虚函数在基类中没有定义 必须在子函数中重写。
https://www.runoob.com/w3cnote/cpp-virtual-functions.html

### 构造函数为啥不能写成虚函数

1. 创建一个对象需要确定对象的类型，而虚函数是在运行是确定其类型的，而在构造一个对象时候，对象还未创建成功，编译器无法知道对象的实际类型。

2. 虚函数会生成虚函数表放在内存空间中，如果构造函数设置未虚函数，对象还没有创建，没有内存空间，更没有虚函数表地址用来调用虚函数。

### 什么时候定义虚析构

1. 每个析构函数只负责清除自己的成员。
2. 可能有基类指针，指向的却是派生类成员的情况，如果不定义析构函数他就不知道怎么办了。



## 虚函数表保存的是什么。保存在哪儿？

虚表存放的位置应该实在模块的常量段中；

## 怎么理解多态

”一个接口多种实现“
编译时的多态性。编译时的多态性是通过重载来实现的。
运行时的多态性。运行时的多态性是通过虚成员实现的。 子类调用父类的虚函数，来实现自己的功能。每个子类调用这个函数所实现的功能都不相同。


## 虚函数是如何实现多态的？

    https://juejin.cn/post/6885225427158499342
    https://blog.csdn.net/i_chaoren/article/details/77281785

## 空指针理解？

如果仅仅声明一个指针，而没有任何赋值，那么这个指针是野指针，可能会引起段错误。
如果将0赋给一个指针，绝对不能使用该指针指向的内容！！！相当于null。
    https://blog.csdn.net/hustyangju/article/details/25691165

## c++设计模式了解哪些？

    https://zhuanlan.zhihu.com/p/111492986

## 智能指针？

    https://juejin.cn/post/6844903993055920141

## 智能指针怎么实现的？

    https://zhuanlan.zhihu.com/p/64543967#:~:text=%E7%A8%8B%E5%BA%8F%E8%87%AA%E5%8A%A8%E5%AE%8C%E6%88%90%E3%80%82-,%E5%A6%82%E4%BD%95%E5%AE%9E%E7%8E%B0%E6%99%BA%E8%83%BD%E6%8C%87%E9%92%88,-%E5%9C%A8%E4%BB%8B%E7%BB%8D%E6%99%BA%E8%83%BD

## c++多态了解多少？用过哪些？

    https://blog.csdn.net/YF_Li123/article/details/74276459
    https://blog.csdn.net/ypt523/article/details/79598289

## malloc和new区别？

    https://blog.csdn.net/nie19940803/article/details/76358673

## 怎么给二维数组分配内存？

    https://blog.csdn.net/lavorange/article/details/42879605

## 多线程join和detach区别？

    https://blog.csdn.net/xibeichengf/article/details/71173543

## c++抽象类？

    https://www.runoob.com/cplusplus/cpp-interfaces.html

# STL:

## vector是怎么实现的？

    https://segmentfault.com/a/1190000040103598

## vector存大量数据是怎么解决的？

    没查到

## vector最大存储量？

    https://blog.csdn.net/iceboy314159/article/details/80329979

## stl中有用到树结构的容器？

    https://blog.csdn.net/weixin_42237990/article/details/98185379

## map有序无序？

    https://blog.csdn.net/weixin_39733805/article/details/111532047

## 把一个自定义的类对象作为map的key时类中有哪些必须要声明的函数？

    https://blog.csdn.net/weixin_41459547/article/details/88421677

# 内存：

## 内存机制？

    https://zhuanlan.zhihu.com/p/344377490

## 堆和栈区别？

    https://www.cnblogs.com/wuaihua/p/7256872.html

## 堆是怎么实现的？

    https://www.jianshu.com/p/a207707c4974

## 多线程：

### 为啥要用多线程：（2个原因）

- **关注点分离**：通过将相关的代码放在一起并将无关的代码分开，可以使你的程序更容易理解和测试，从而减少出错的可能性。你可以使用并发来分隔不同的功能区域，即使在这些不同功能区域的操作需要在同一时刻发生的情况下；若不显式地使用并发，你要么被迫编写任务切换框架，要么在操作中主动地调用不相关的一段代码。
- **更高效的性能**：为了充分发挥多核心处理器的优势，使用并发将单个任务分成几部分且各自并行运行，从而降低总运行时间。根据任务分割方式的不同，又可以将其分为两大类：一类是对同样的数据应用不同的处理算法（任务并行）；另一类是用同样的处理算法共同处理数据的几部分（数据并行）。



多进程之间的通信：管道、信号、文件、套接字

