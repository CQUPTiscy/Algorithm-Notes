为什么Java代码可以实现一次编写、到处运行？

```
JVM（Java虚拟机）是Java跨平台的关键。

在程序运行前，Java源代码（.java）需要经过编译器编译成字节码（.class）。在程序运行时，JVM负责将字节码翻译成特定平台下的机器码并运行，也就是说，只要在不同的平台上安装对应的JVM，就可以运行字节码文件。
```

说一说你对Java访问权限的了解？

```
在修饰成员变量/成员方法时，该成员的四种访问权限的含义如下：

private：该成员可以被该类内部成员访问；

default：该成员可以被该类内部成员访问，也可以被同一包下其他的类访问；

protected：该成员可以被该类内部成员访问，也可以被同一包下其他的类访问，还可以被它的子类访问；

public：该成员可以被任意包下，任意类的成员进行访问。

在修饰类时，该类只有两种访问权限，对应的访问权限的含义如下：

default：该类可以被同一包下其他的类访问；

public：该类可以被任意包下，任意的类所访问。
```

介绍一下Java的数据类型？

```
基本数据类型有8个，可以分为4个小类，分别是整数类型（byte/short/int/long）、浮点类型（float/double）、字符类型（char）、布尔类型（boolean）。其中，4个整数类型中，int类型最为常用。2个浮点类型中，double最为常用。另外，在这8个基本类型当中，除了布尔类型之外的其他7个类型，都可以看做是数字类型，它们相互之间可以进行类型转换。

引用类型就是对一个对象的引用，根据引用对象类型的不同，可以将引用类型分为3类，即数组、类、接口类型。引用类型本质上就是通过指针，指向堆中对象所持有的内存空间，只是Java语言不再沿用指针这个说法而已。
```

包装类的意义以及自动装箱、拆箱的场景

```
Java语言是面向对象的语言，其设计理念是“一切皆对象”。但8种基本数据类型却出现了例外，它们不具备对象的特性。正是为了解决这个问题，Java为每个基本数据类型都定义了一个对应的引用类型，这就是包装类。
自动装箱：可以把一个基本类型的数据直接赋值给对应的包装类型；
自动拆箱：可以把一个包装类型的对象直接赋值给对应的基本类型；
通过自动装箱、自动拆箱功能，可以大大简化基本类型变量和包装类对象之间的转换过程。比如，某个方法的参数类型为包装类型，调用时我们所持有的数据却是基本类型的值，则可以不做任何特殊的处理，直接将这个基本类型的值传入给方法即可。

```

如何对Integer和Double类型判断相等？

```
可以将Integer、Double先转为转换为相同的基本数据类型（如double），然后使用==进行比较。
Integer i = 100;
Double d = 100.00;
System.out.println(i.doubleValue() == d.doubleValue());
```

