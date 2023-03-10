遇到过异常吗，如何处理？

```
捕获异常
将业务代码包裹在try块内部，当业务代码中发生任何异常时，系统都会为此异常创建一个异常对象。创建异常对象之后，JVM会在try块之后寻找可以处理它的catch块，并将异常对象交给这个catch块处理。
处理异常
在catch块中处理异常时，应该先记录日志，便于以后追溯这个异常。然后根据异常的类型、结合当前的业务情况，进行相应的处理。比如，给变量赋予一个默认值、直接返回空值、向外抛出一个新的业务异常交给调用者处理，等等。
回收资源
如果业务代码打开了某个资源，比如数据库连接、网络连接、磁盘文件等，则需要在这段业务代码执行完毕后关闭这项资源。并且，无论是否发生异常，都要尝试关闭这项资源。将关闭资源的代码写在finally块内，可以满足这种需求，即无论是否发生异常，finally块内的代码总会被执行。
```

说一说你对static关键字的理解？

```
在Java类里只能包含成员变量、方法、构造器、初始化块、内部类（包括接口、枚举）5种成员，而static可以修饰成员变量、方法、初始化块、内部类（包括接口、枚举），以static修饰的成员就是类成员。类成员属于整个类，而不属于单个对象。

对static关键字而言，有一条非常重要的规则：类成员（包括成员变量、方法、初始化块、内部类和内部枚举）不能访问实例成员（包括成员变量、方法、初始化块、内部类和内部枚举）。因为类成员是属于类的，类成员的作用域比实例成员的作用域更大，完全可能出现类成员已经初始化完成，但实例成员还不曾初始化的情况，如果允许类成员访问实例成员将会引起大量错误。

static修饰的类可以被继承。
```

说一说对泛型的理解？

```
Java集合有个缺点—把一个对象“丢进”集合里之后，集合就会“忘记”这个对象的数据类型，当再次取出该对象时，该对象的编译类型就变成了Object类型（其运行时类型没变）。

Java集合之所以被设计成这样，是因为集合的设计者不知道我们会用集合来保存什么类型的对象，所以他们把集合设计成能保存任何类型的对象，只要求具有很好的通用性。但这样做带来如下两个问题：

集合对元素类型没有任何限制，这样可能引发一些问题。例如，想创建一个只能保存Dog对象的集合，但程序也可以轻易地将Cat对象“丢”进去，所以可能引发异常。

由于把对象“丢进”集合时，集合丢失了对象的状态信息，只知道它盛装的是Object，因此取出集合元素后通常还需要进行强制类型转换。这种强制类型转换既增加了编程的复杂度，也可能引发ClassCastException异常。

从Java 5开始，Java引入了“参数化类型”的概念，允许程序在创建集合时指定集合元素的类型，Java的参数化类型被称为泛型（Generic）。例如 List<String>，表明该List只能保存字符串类型的对象。

有了泛型以后，程序再也不能“不小心”地把其他对象“丢进”集合中。而且程序更加简洁，集合自动记住所有集合元素的数据类型，从而无须对集合元素进行强制类型转换。
```

泛型擦除？

```
当把一个具有泛型信息的对象赋给另一个没有泛型信息的变量时，所有在尖括号之间的类型信息都将被扔掉。比如一个 List<String> 类型被转换为List，则该List对集合元素的类型检查变成了泛型参数的上限（即Object）。

List<String> list1 = ...; List list2 = list1; // list2将元素当做Object处理

泛型转换：
List list1 = ...; List<String> list2 = list1; // 编译时警告“未经检查的转换”


```

反射机制的理解和应用场景？

```
Java程序中的对象在运行时可以表现为两种类型，即编译时类型和运行时类型。例如 Person p = new Student(); ，这行代码将会生成一个p变量，该变量的编译时类型为Person，运行时类型为Student。

有时，程序在运行时接收到外部传入的一个对象，该对象的编译时类型是Object，但程序又需要调用该对象的运行时类型的方法。这就要求程序需要在运行时发现对象和类的真实信息，而解决这个问题有以下两种做法：

第一种做法是假设在编译时和运行时都完全知道类型的具体信息，在这种情况下，可以先使用instanceof运算符进行判断，再利用强制类型转换将其转换成其运行时类型的变量即可。

第二种做法是编译时根本无法预知该对象和类可能属于哪些类，程序只依靠运行时信息来发现该对象和类的真实信息，这就必须使用反射。

具体来说，通过反射机制，我们可以实现如下的操作：

程序运行时，可以通过反射获得任意一个类的Class对象，并通过这个对象查看这个类的信息；

程序运行时，可以通过反射创建任意一个类的实例，并访问该实例的成员；

程序运行时，可以通过反射机制生成一个类的动态代理类或动态代理对象。


Java的反射机制在实际项目中应用广泛，常见的应用场景有：

使用JDBC时，如果要创建数据库的连接，则需要先通过反射机制加载数据库的驱动程序；

多数框架都支持注解/XML配置，从配置中解析出来的类是字符串，需要利用反射机制实例化；

面向切面编程（AOP）的实现方案，是在程序运行时创建目标对象的代理类，这必须由反射机制来实现。
```

Java中的四种引用方式？

```
Java对象的四种引用方式分别是强引用、软引用、弱引用、虚引用，具体含义如下：

强引用：这是Java程序中最常见的引用方式，即程序创建一个对象，并把这个对象赋给一个引用变量，程序通过该引用变量来操作实际的对象。当一个对象被一个或一个以上的引用变量所引用时，它处于可达状态，不可能被系统垃圾回收机制回收。

软引用：当一个对象只有软引用时，它有可能被垃圾回收机制回收。对于只有软引用的对象而言，当系统内存空间足够时，它不会被系统回收，程序也可使用该对象。当系统内存空间不足时，系统可能会回收它。软引用通常用于对内存敏感的程序中。

弱引用：弱引用和软引用很像，但弱引用的引用级别更低。对于只有弱引用的对象而言，当系统垃圾回收机制运行时，不管系统内存是否足够，总会回收该对象所占用的内存。当然，并不是说当一个对象只有弱引用时，它就会立即被回收，正如那些失去引用的对象一样，必须等到系统垃圾回收机制运行时才会被回收。

虚引用：虚引用完全类似于没有引用。虚引用对对象本身没有太大影响，对象甚至感觉不到虚引用的存在。如果一个对象只有一个虚引用时，那么它和没有引用的效果大致相同。虚引用主要用于跟踪对象被垃圾回收的状态，虚引用不能单独使用，虚引用必须和引用队列联合使用。
```
