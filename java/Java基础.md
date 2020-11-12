## Typora常用快捷键

- 插入图片： `Ctrl + Shift + I`
- 一级标题： `Ctrl + 1` -- 以此类推
- 加粗： `Ctrl + B`
- 标题： `Ctrl + H`
- 插入代码  ` ``` ` -- 插入多行代码输入3个反引号（） + 回车
- 文字高亮 ` 文件==》编好设置==》Markdown ==》勾选高亮 ` ` 例： ==高亮文字==`
- 无序列表 `使用 * + - 都可以创建一个无序列表`-- 必须有空格
- 有序列表 ` 使用 1. 2. 3. 创建有序列表` -- 必须有空格
- 请看段落



## B站播放速度

```java
document.querySelector('video').playbackRate=15//15倍 
```

## java入门

### [1.Java语言的特点]()

1. 简单易学；
2. 面向对象（封装，继承，多态）；
3. 平台无关性（ Java 虚拟机实现平台无关性）；
4. 可靠性；
5. 安全性；

### [2.关于 JVM JDK 和 JRE 最详细通俗的解答]()

#### [JVM]()

Java 虚拟机（JVM）是运行 Java 字节码的虚拟机。JVM 有针对不同系统的特定实现（Windows，Linux，macOS），目的是使用相同的字节码，它们都会给出相同的结果。

#### **[什么是字节码?采用字节码的好处是什么?]()**

> 在 Java 中，JVM 可以理解的代码就叫做`字节码`（即扩展名为 `.class` 的文件），它不面向任何特定的处理器，只面向虚拟机。Java 语言通过字节码的方式，在一定程度上解决了传统解释型语言执行效率低的问题，同时又保留了解释型语言可移植的特点。所以 Java 程序运行时比较高效，而且，由于字节码并不针对一种特定的机器，因此，Java 程序无须重新编译便可在多种不同操作系统的计算机上运行。

#### **[Java 程序从源代码到运行一般有下面 3 步：]()**

![Java程序运行过程](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/Java%20%E7%A8%8B%E5%BA%8F%E8%BF%90%E8%A1%8C%E8%BF%87%E7%A8%8B.png)



我们需要格外注意的是 .class->机器码 这一步。在这一步 JVM 类加载器首先加载字节码文件，然后通过解释器逐行解释执行，这种方式的执行速度会相对比较慢。而且，有些方法和代码块是经常需要被调用的(也就是所谓的热点代码)，所以后面引进了 JIT 编译器，而 JIT 属于运行时编译。当 JIT 编译器完成第一次编译后，其会将字节码对应的机器码保存下来，下次可以直接使用。而我们知道，机器码的运行效率肯定是高于 Java 解释器的。这也解释了我们为什么经常会说 Java 是编译与解释共存的语言。

> HotSpot 采用了惰性评估(Lazy Evaluation)的做法，根据二八定律，消耗大部分系统资源的只有那一小部分的代码（热点代码），而这也就是 JIT 所需要编译的部分。JVM 会根据代码每次被执行的情况收集信息并相应地做出一些优化，因此执行的次数越多，它的速度就越快。JDK 9 引入了一种新的编译模式 AOT(Ahead of Time Compilation)，它是直接将字节码编译成机器码，这样就避免了 JIT 预热等各方面的开销。JDK 支持分层编译和 AOT 协作使用。但是 ，AOT 编译器的编译质量是肯定比不上 JIT 编译器的。

**[总结：]()**

Java 虚拟机（JVM）是运行 Java 字节码的虚拟机。JVM 有针对不同系统的特定实现（Windows，Linux，macOS），目的是使用相同的字节码，它们都会给出相同的结果。字节码和不同系统的 JVM 实现是 Java 语言“一次编译，随处可以运行”的关键所在。

#### [JDK 和 JRE]()

JDK 是 Java Development Kit 缩写，它是功能齐全的 Java SDK。它拥有 JRE 所拥有的一切，还有编译器（javac）和工具（如 javadoc 和 jdb）。它能够创建和编译程序。

JRE 是 Java 运行时环境。它是运行已编译 Java 程序所需的所有内容的集合，包括 Java 虚拟机（JVM），Java 类库，java 命令和其他的一些基础构件。但是，它不能用于创建新程序。

如果你只是为了运行一下 Java 程序的话，那么你只需要安装 JRE 就可以了。如果你需要进行一些 Java 编程方面的工作，那么你就需要安装 JDK 了。但是，这不是绝对的。有时，即使您不打算在计算机上进行任何 Java 开发，仍然需要安装 JDK。例如，如果要使用 JSP 部署 Web 应用程序，那么从技术上讲，您只是在应用程序服务器中运行 Java 程序。那你为什么需要 JDK 呢？因为应用程序服务器会将 JSP 转换为 Java servlet，并且需要使用 JDK 来编译 servlet。

#### [Oracle JDK 和 OpenJDK 的对比]()

可能在看这个问题之前很多人和我一样并没有接触和使用过 OpenJDK 。那么 Oracle 和 OpenJDK 之间是否存在重大差异？下面我通过收集到的一些资料，为你解答这个被很多人忽视的问题。

对于 Java 7，没什么关键的地方。OpenJDK 项目主要基于 Sun 捐赠的 HotSpot 源代码。此外，OpenJDK 被选为 Java 7 的参考实现，由 Oracle 工程师维护。关于 JVM，JDK，JRE 和 OpenJDK 之间的区别，Oracle 博客帖子在 2012 年有一个更详细的答案：

> 问：OpenJDK 存储库中的源代码与用于构建 Oracle JDK 的代码之间有什么区别？
>
> 答：非常接近 - 我们的 Oracle JDK 版本构建过程基于 OpenJDK 7 构建，只添加了几个部分，例如部署代码，其中包括 Oracle 的 Java 插件和 Java WebStart 的实现，以及一些封闭的源代码派对组件，如图形光栅化器，一些开源的第三方组件，如 Rhino，以及一些零碎的东西，如附加文档或第三方字体。展望未来，我们的目的是开源 Oracle JDK 的所有部分，除了我们考虑商业功能的部分。

**[总结：]()**

1. Oracle JDK 大概每 6 个月发一次主要版本，而 OpenJDK 版本大概每三个月发布一次。但这不是固定的，我觉得了解这个没啥用处。详情参见：https://blogs.oracle.com/java-platform-group/update-and-faq-on-the-java-se-release-cadence 。
2. OpenJDK 是一个参考模型并且是完全开源的，而 Oracle JDK 是 OpenJDK 的一个实现，并不是完全开源的；
3. Oracle JDK 比 OpenJDK 更稳定。OpenJDK 和 Oracle JDK 的代码几乎相同，但 Oracle JDK 有更多的类和一些错误修复。因此，如果您想开发企业/商业软件，我建议您选择 Oracle JDK，因为它经过了彻底的测试和稳定。某些情况下，有些人提到在使用 OpenJDK 可能会遇到了许多应用程序崩溃的问题，但是，只需切换到 Oracle JDK 就可以解决问题；
4. 在响应性和 JVM 性能方面，Oracle JDK 与 OpenJDK 相比提供了更好的性能；
5. Oracle JDK 不会为即将发布的版本提供长期支持，用户每次都必须通过更新到最新版本获得支持来获取最新版本；
6. Oracle JDK 根据二进制代码许可协议获得许可，而 OpenJDK 根据 GPL v2 许可获得许可。

#### [Java 和 C++的区别?]()

我知道很多人没学过 C++，但是面试官就是没事喜欢拿咱们 Java 和 C++ 比呀！没办法！！！就算没学过 C++，也要记下来！

- 都是面向对象的语言，都支持封装、继承和多态
- Java 不提供指针来直接访问内存，程序内存更加安全
- Java 的类是单继承的，C++ 支持多重继承；虽然 Java 的类不可以多继承，但是接口可以多继承。
- Java 有自动内存管理垃圾回收机制(GC)，不需要程序员手动释放无用内存
- **在 C 语言中，字符串或字符数组最后都会有一个额外的字符`'\0'`来表示结束。但是，Java 语言中没有结束符这一概念。** 这是一个值得深度思考的问题，具体原因推荐看这篇文章： https://blog.csdn.net/sszgg2006/article/details/49148189

#### [什么是 Java 程序的主类 应用程序和小程序的主类有何不同?]()

一个程序中可以有多个类，但只能有一个类是主类。在 Java 应用程序中，这个主类是指包含 `main()` 方法的类。而在 Java 小程序中，这个主类是一个继承自系统类 JApplet 或 Applet 的子类。应用程序的主类不一定要求是 public 类，但小程序的主类要求必须是 public 类。主类是 Java 程序执行的入口点。

#### [ Java 应用程序与小程序之间有哪些差别?]()

简单说应用程序是从主线程启动(也就是 `main()` 方法)。applet 小程序没有 `main()` 方法，主要是嵌在浏览器页面上运行(调用`init()`或者`run()`来启动)，嵌入浏览器这点跟 flash 的小游戏类似。

#### [import java 和 javax 有什么区别？]()

刚开始的时候 JavaAPI 所必需的包是 java 开头的包，javax 当时只是扩展 API 包来使用。然而随着时间的推移，javax 逐渐地扩展成为 Java API 的组成部分。但是，将扩展从 javax 包移动到 java 包确实太麻烦了，最终会破坏一堆现有的代码。因此，最终决定 javax 包将成为标准 API 的一部分。

所以，实际上 java 和 javax 没有区别。这都是一个名字。

#### [为什么说 Java 语言“编译与解释并存”？]()

高级编程语言按照程序的执行方式分为编译型和解释型两种。简单来说，编译型语言是指编译器针对特定的操作系统将源代码一次性翻译成可被该平台执行的机器码；解释型语言是指解释器对源程序逐行解释成特定平台的机器码并立即执行。比如，你想阅读一本英文名著，你可以找一个英文翻译人员帮助你阅读， 有两种选择方式，你可以先等翻译人员将全本的英文名著（也就是源码）都翻译成汉语，再去阅读，也可以让翻译人员翻译一段，你在旁边阅读一段，慢慢把书读完。

Java 语言既具有编译型语言的特征，也具有解释型语言的特征，因为 Java 程序要经过先编译，后解释两个步骤，由 Java 编写的程序需要先经过编译步骤，生成字节码（*.class 文件），这种字节码必须由 Java 解释器来解释执行。因此，我们可以认为 Java 语言编译与解释并存。

## Java语法

### [1.注释]()

+ ==平时写代码一定要注意规范，写注释是个非常好的习惯==

1. 单行注释

   ```
   //后面写注释
   ```

2. 多行注释

   ```java 
   /* 里面写注释*/
   ```

3. 文档注释

   ```java
   /**回车*/
   ```

   idea设置注释颜色

![](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200916093210939.png)





#### [标识符和关键字的区别是什么？]()

在我们编写程序的时候，需要大量地为程序、类、变量、方法等取名字，于是就有了标识符，简单来说，标识符就是一个名字。但是有一些标识符，Java 语言已经赋予了其特殊的含义，只能用于特定的地方，这种特殊的标识符就是关键字。因此，关键字是被赋予特殊含义的标识符。比如，在我们的日常生活中 ，“警察局”这个名字已经被赋予了特殊的含义，所以如果你开一家店，店的名字不能叫“警察局”，“警察局”就是我们日常生活中的关键字。

### [2.关键字]()

| 访问控制             | private  | protected  | public   |              |            |           |        |
| -------------------- | -------- | ---------- | -------- | ------------ | ---------- | --------- | ------ |
| 类，方法和变量修饰符 | abstract | class      | extends  | final        | implements | interface | native |
|                      | new      | static     | strictfp | synchronized | transient  | volatile  |        |
| 程序控制             | break    | continue   | return   | do           | while      | if        | else   |
|                      | for      | instanceof | switch   | case         | default    |           |        |
| 错误处理             | try      | catch      | throw    | throws       | finally    |           |        |
| 包相关               | import   | package    |          |              |            |           |        |
| 基本类型             | boolean  | byte       | char     | double       | float      | int       | long   |
|                      | short    | null       | true     | false        |            |           |        |
| 变量引用             | super    | this       | void     |              |            |           |        |
| 保留字               | goto     | const      |          |              |            |           |        |

abstract：表明类或类中的方法是抽象的；

• boolean：基本数据类型之一，布尔类型；

• break：提前跳出一个块；

• byte：基本数据类型之一，字节类型；

• case：在switch语句中，表明其中的一个分支；

• catch：用于处理例外情况，用来捕捉异常；

• char：基本数据类型之一，字符类型；

• class：类；

• continue：回到一个块的开始处；

• default：用在 switch语句中，表明一个默认的分支；

• do：用在"do while"循环结构中；

• double：基本数据类型之一，双精度浮点数类型；

• else：在条件语句中，表明当条件不成立时的分支；

• extends：用来表明一个类是另一个类的子类；

• final：用来表明一个类不能派生出子类，或类中的方法不能被覆盖，或声明一个变量是常量；

• finally：用于处理异常情况，用来声明一个肯定会被执行到的块；

• float：基本数据类型之一，单精度浮点数类型；

• for：一种循环结构的引导词；

• if：条件语句的引导词；

• implements：表明一个类实现了给定的接口；

• import：表明要访问指定的类或包；

• instanceof：用来测试一个对象是否是一个指定类的实例；

• int：基本数据类型之一，整数类型；

• interface：接口；

• long：基本数据类型之一，长整数类型；

• native： 用来声明一个方法是由与机器相关的语言(如C/C++/FORTRAN语言)实现的； 

• new：用来申请新对象；

• package：包；

• private：一种访问方式：私有模式；

• protected：一种访问方式：保护模式；

• public：一种访问方式：公共模式；

• return：从方法中返回值；

• short：基本数据类型之一，短整数类型；

• static：表明域或方法是静态的，即该域或方法是属于类的；

• strictfp：用来声明FP-strict(双精度或单精度浮点数)表达式，参见 IEEE 754 算术规范；

• super：当前对象的父类对象的引用；

• switch：分支结构的引导词；

• synchronized：表明一段代码的执行需要同步；

• this：当前对象的引用；

• throw：抛出一个异常；

• throws：声明方法中抛出的所有异常；

• transient：声明不用序列化的域；

• try：尝试一个可能抛出异常的程序块

• void：表明方法不返回值；

• volatile：表明两个或多个变量必须同步地发生变化；

• while：用在循环结构中；

• assert：声明断言；

• enum：声明枚举类型；



#### [字符型常量和字符串常量的区别?]()

1. 形式上: 字符常量是单引号引起的一个字符; 字符串常量是双引号引起的0个或若干个字符

2. 含义上: 字符常量相当于一个整型值( ASCII 值),可以参加表达式运算; 字符串常量代表一个地址值(该字符串在内存中存放位置)

3. 占内存大小 字符常量只占 2 个字节; 字符串常量占若干个字节 (

   注意： char 在 Java 中占两个字节

   ),

   > 字符封装类 `Character` 有一个成员常量 `Character.SIZE` 值为16,单位是`bits`,该值除以8(`1byte=8bits`)后就可以得到2个字节

![img](http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-9-15/86735519.jpg)



#### [自增自减运算符]()

在写代码的过程中，常见的一种情况是需要某个整数类型变量增加 1 或减少 1，Java 提供了一种特殊的运算符，用于这种表达式，叫做自增运算符（++)和自减运算符（--）。

++和--运算符可以放在变量之前，也可以放在变量之后，当运算符放在变量之前时(前缀)，先自增/减，再赋值；当运算符放在变量之后时(后缀)，先赋值，再自增/减。例如，当 `b = ++a` 时，先自增（自己增加 1），再赋值（赋值给 b）；当 `b = a++` 时，先赋值(赋值给 b)，再自增（自己增加 1）。也就是，++a 输出的是 a+1 的值，a++输出的是 a 值。用一句口诀就是：“符号在前就先加/减，符号在后就后加/减”。

#### [continue、break、和return的区别是什么？]()

在循环结构中，当循环条件不满足或者循环次数达到要求时，循环会正常结束。但是，有时候可能需要在循环的过程中，当发生了某种条件之后 ，提前终止循环，这就需要用到下面几个关键词：

1. continue ：指跳出当前的这一次循环，继续下一次循环。
2. break ：指跳出整个循环体，继续执行循环下面的语句。

return 用于跳出所在方法，结束该方法的运行。return 一般有两种用法：

1. `return;` ：直接使用 return 结束方法执行，用于没有返回值函数的方法
2. `return value;` ：return 一个特定值，用于有返回值函数的方法

#### [ Java泛型了解么？什么是类型擦除？介绍一下常用的通配符？]()

Java 泛型（generics）是 JDK 5 中引入的一个新特性, 泛型提供了编译时类型安全检测机制，该机制允许程序员在编译时检测到非法的类型。泛型的本质是参数化类型，也就是说所操作的数据类型被指定为一个参数。

**Java的泛型是伪泛型，这是因为Java在编译期间，所有的泛型信息都会被擦掉，这也就是通常所说类型擦除 。** 更多关于类型擦除的问题，可以查看这篇文章：[《Java泛型类型擦除以及类型擦除带来的问题》](https://www.cnblogs.com/wuqinglong/p/9456193.html) 。



```java
List<Integer> list = new ArrayList<>();

list.add(12);
//这里直接添加会报错 上面List<Integer>不是Sting类型
list.add("a");
Class<? extends List> clazz = list.getClass();
Method add = clazz.getDeclaredMethod("add", Object.class);
//但是通过反射添加，是可以的
add.invoke(list, "kl");

System.out.println(list)
```

泛型一般有三种使用方式:泛型类、泛型接口、泛型方法。

**1.泛型类**：

```java
//此处T可以随便写为任意标识，常见的如T、E、K、V等形式的参数常用于表示泛型
//在实例化泛型类时，必须指定T的具体类型
public class Generic<T>{ 

    private T key;

    public Generic(T key) { 
        this.key = key;
    }

    public T getKey(){ 
        return key;
    }
}
```

如何实例化泛型类：

```java
Generic<Integer> genericInteger = new Generic<Integer>(123456);
```

**2.泛型接口** ：

```java
public interface Generator<T> {
    public T method();
}
```

实现泛型接口，不指定类型：

```java
class GeneratorImpl<T> implements Generator<T>{
    @Override
    public T method() {
        return null;
    }
}
```

实现泛型接口，指定类型：

```java
class GeneratorImpl<T> implements Generator<String>{
    @Override
    public String method() {
        return "hello";
    }
}
```

**3.泛型方法** ：

```java
   public static < E > void printArray( E[] inputArray )
   {         
         for ( E element : inputArray ){        
            System.out.printf( "%s ", element );
         }
         System.out.println();
    }
```

使用：

```java
// 创建不同类型数组： Integer, Double 和 Character
Integer[] intArray = { 1, 2, 3 };
String[] stringArray = { "Hello", "World" };
printArray( intArray  ); 
printArray( stringArray  ); 
```

**常用的通配符为： T，E，K，V，？**

- ？ 表示不确定的 java 类型
- T (type) 表示具体的一个java类型
- K V (key value) 分别代表java键值中的Key Value
- E (element) 代表Element

更多关于Java 泛型中的通配符可以查看这篇文章：[《聊一聊-JAVA 泛型中的通配符 T，E，K，V，？》](https://juejin.im/post/5d5789d26fb9a06ad0056bd9)

#### [==和equals的区别]()

**`==`** : 它的作用是判断两个对象的地址是不是相等。即判断两个对象是不是同一个对象。(**基本数据类型==比较的是值，引用数据类型==比较的是内存地址**)

> 因为 Java 只有值传递，所以，对于 == 来说，不管是比较基本数据类型，还是引用数据类型的变量，其本质比较的都是值，只是引用类型变量存的值是对象的地址。

**`equals()`** : 它的作用也是判断两个对象是否相等，它不能用于比较基本数据类型的变量。`equals()`方法存在于`Object`类中，而`Object`类是所有类的直接或间接父类。

`Object`类`equals()`方法：

```java
public boolean equals(Object obj) {
     return (this == obj);
}
```

`equals()` 方法存在两种使用情况：

- 情况 1：类没有覆盖 `equals()`方法。则通过` equals()`比较该类的两个对象时，等价于通过“==”比较这两个对象。使用的默认是 `Object`类`equals()`方法。
- 情况 2：类覆盖了 `equals()`方法。一般，我们都覆盖 `equals()`方法来两个对象的内容相等；若它们的内容相等，则返回 true(即，认为这两个对象相等)。

**举个例子：**

```java
public class test1 {
    public static void main(String[] args) {
        String a = new String("ab"); // a 为一个引用
        String b = new String("ab"); // b为另一个引用,对象的内容一样
        String aa = "ab"; // 放在常量池中
        String bb = "ab"; // 从常量池中查找
        if (aa == bb) // true
            System.out.println("aa==bb");
        if (a == b) // false，非同一对象
            System.out.println("a==b");
        if (a.equals(b)) // true
            System.out.println("aEQb");
        if (42 == 42.0) { // true
            System.out.println("true");
        }
    }
}
```

**说明：**

- `String` 中的 `equals` 方法是被重写过的，因为 `Object` 的 `equals` 方法是比较的对象的内存地址，而 `String` 的 `equals` 方法比较的是对象的值。
- 当创建 `String` 类型的对象时，虚拟机会在常量池中查找有没有已经存在的值和要创建的值相同的对象，如果有就把它赋给当前引用。如果没有就在常量池中重新创建一个 `String` 对象。

`String`类`equals()`方法：

```java
public boolean equals(Object anObject) {
    if (this == anObject) {
        return true;
    }
    if (anObject instanceof String) {
        String anotherString = (String)anObject;
        int n = value.length;
        if (n == anotherString.value.length) {
            char v1[] = value;
            char v2[] = anotherString.value;
            int i = 0;
            while (n-- != 0) {
                if (v1[i] != v2[i])
                    return false;
                i++;
            }
            return true;
        }
    }
    return false;
}
```

#### [hashCode()与 equals()]()

面试官可能会问你：“你重写过 `hashcode` 和 `equals `么，为什么重写 `equals` 时必须重写 `hashCode` 方法？”

**1)hashCode()介绍:**

`hashCode()` 的作用是获取哈希码，也称为散列码；它实际上是返回一个 int 整数。这个哈希码的作用是确定该对象在哈希表中的索引位置。`hashCode() `定义在 JDK 的 `Object` 类中，这就意味着 Java 中的任何类都包含有 `hashCode()` 函数。另外需要注意的是： `Object` 的 hashcode 方法是本地方法，也就是用 c 语言或 c++ 实现的，该方法通常用来将对象的 内存地址 转换为整数之后返回。

```java
public native int hashCode();
```

散列表存储的是键值对(key-value)，它的特点是：能根据“键”快速的检索出对应的“值”。这其中就利用到了散列码！（可以快速找到所需要的对象）

**2)为什么要有 hashCode？**

我们以“`HashSet` 如何检查重复”为例子来说明为什么要有 hashCode？

当你把对象加入 `HashSet` 时，`HashSet` 会先计算对象的 hashcode 值来判断对象加入的位置，同时也会与其他已经加入的对象的 hashcode 值作比较，如果没有相符的 hashcode，`HashSet` 会假设对象没有重复出现。但是如果发现有相同 hashcode 值的对象，这时会调用 `equals()` 方法来检查 hashcode 相等的对象是否真的相同。如果两者相同，`HashSet` 就不会让其加入操作成功。如果不同的话，就会重新散列到其他位置。（摘自我的 Java 启蒙书《Head First Java》第二版）。这样我们就大大减少了 equals 的次数，相应就大大提高了执行速度。

**3)为什么重写 `equals` 时必须重写 `hashCode` 方法？**

如果两个对象相等，则 hashcode 一定也是相同的。两个对象相等,对两个对象分别调用 equals 方法都返回 true。但是，两个对象有相同的 hashcode 值，它们也不一定是相等的 。**因此，equals 方法被覆盖过，则 `hashCode` 方法也必须被覆盖。**

> `hashCode()`的默认行为是对堆上的对象产生独特值。如果没有重写 `hashCode()`，则该 class 的两个对象无论如何都不会相等（即使这两个对象指向相同的数据）

**4)为什么两个对象有相同的 hashcode 值，它们也不一定是相等的？**

在这里解释一位小伙伴的问题。以下内容摘自《Head Fisrt Java》。

因为 `hashCode()` 所使用的杂凑算法也许刚好会让多个对象传回相同的杂凑值。越糟糕的杂凑算法越容易碰撞，但这也与数据值域分布的特性有关（所谓碰撞也就是指的是不同的对象得到相同的 `hashCode`。

我们刚刚也提到了 `HashSet`,如果 `HashSet` 在对比的时候，同样的 hashcode 有多个对象，它会使用 `equals()` 来判断是否真的相同。也就是说 `hashcode` 只是用来缩小查找成本。

更多关于 `hashcode()` 和 `equals()` 的内容可以查看：[Java hashCode() 和 equals()的若干问题解答](https://www.cnblogs.com/skywang12345/p/3324958.html)

## 基本数据类型

#### [Java中的几种基本数据类型是什么？对应的包装类型是什么？各自占用多少字节呢？]()

Java**中**有8种基本数据类型，分别为：

1. 6种数字类型 ：byte、short、int、long、float、double
2. 1种字符类型：char
3. 1种布尔型：boolean。

这八种基本类型都有对应的包装类分别为：Byte、Short、Integer、Long、Float、Double、Character、Boolean

| 基本类型 | 位数 | 字节 | 默认值  |
| -------- | ---- | ---- | ------- |
| int      | 32   | 4    | 0       |
| short    | 16   | 2    | 0       |
| long     | 64   | 8    | 0L      |
| byte     | 8    | 1    | 0       |
| char     | 16   | 2    | 'u0000' |
| float    | 32   | 4    | 0f      |
| double   | 64   | 8    | 0d      |
| boolean  | 1    |      | false   |

对于boolean，官方文档未明确定义，它依赖于 JVM 厂商的具体实现。逻辑上理解是占用 1位，但是实际中会考虑计算机高效存储因素。

注意：

1. Java 里使用 long 类型的数据一定要在数值后面加上 **L**，否则将作为整型解析：
2. `char a = 'h'`char :单引号，`String a = "hello"` :双引号

#### [自动装箱与拆箱]()

- **装箱**：将基本类型用它们对应的引用类型包装起来；
- **拆箱**：将包装类型转换为基本数据类型；

更多内容见：[深入剖析 Java 中的装箱和拆箱](https://www.cnblogs.com/dolphin0520/p/3780005.html)

#### [种基本类型的包装类和常量池]()

**Java 基本类型的包装类的大部分都实现了常量池技术，即 Byte,Short,Integer,Long,Character,Boolean；前面 4 种包装类默认创建了数值[-128，127] 的相应类型的缓存数据，Character创建了数值在[0,127]范围的缓存数据，Boolean 直接返回True Or False。如果超出对应范围仍然会去创建新的对象。** 为啥把缓存设置为[-128，127]区间？（[参见issue/461](https://github.com/Snailclimb/JavaGuide/issues/461)）性能和资源之间的权衡。

```java
public static Boolean valueOf(boolean b) {
    return (b ? TRUE : FALSE);
}
private static class CharacterCache {         
    private CharacterCache(){}

    static final Character cache[] = new Character[127 + 1];          
    static {             
        for (int i = 0; i < cache.length; i++)                 
            cache[i] = new Character((char)i);         
    }   
}
```

两种浮点数类型的包装类 Float,Double 并没有实现常量池技术。**

```java
        Integer i1 = 33;
        Integer i2 = 33;
        System.out.println(i1 == i2);// 输出 true
        Integer i11 = 333;
        Integer i22 = 333;
        System.out.println(i11 == i22);// 输出 false
        Double i3 = 1.2;
        Double i4 = 1.2;
        System.out.println(i3 == i4);// 输出 false
```

**Integer 缓存源代码：**

```java
/**
*此方法将始终缓存-128 到 127（包括端点）范围内的值，并可以缓存此范围之外的其他值。
*/
    public static Integer valueOf(int i) {
        if (i >= IntegerCache.low && i <= IntegerCache.high)
            return IntegerCache.cache[i + (-IntegerCache.low)];
        return new Integer(i);
    }
```

**应用场景：**

1. Integer i1=40；Java 在编译的时候会直接将代码封装成 Integer i1=Integer.valueOf(40);，从而使用常量池中的对象。
2. Integer i1 = new Integer(40);这种情况下会创建新的对象。

```java
  Integer i1 = 40;
  Integer i2 = new Integer(40);
  System.out.println(i1 == i2);//输出 false
```

**Integer 比较更丰富的一个例子:**

```java
  Integer i1 = 40;
  Integer i2 = 40;
  Integer i3 = 0;
  Integer i4 = new Integer(40);
  Integer i5 = new Integer(40);
  Integer i6 = new Integer(0);

  System.out.println("i1=i2   " + (i1 == i2));
  System.out.println("i1=i2+i3   " + (i1 == i2 + i3));
  System.out.println("i1=i4   " + (i1 == i4));
  System.out.println("i4=i5   " + (i4 == i5));
  System.out.println("i4=i5+i6   " + (i4 == i5 + i6));   
  System.out.println("40=i5+i6   " + (40 == i5 + i6));     
```

结果：

```java
i1=i2   true
i1=i2+i3   true
i1=i4   false
i4=i5   false
i4=i5+i6   true
40=i5+i6   true
```

解释：

语句 i4 == i5 + i6，因为+这个操作符不适用于 Integer 对象，首先 i5 和 i6 进行自动拆箱操作，进行数值相加，即 i4 == 40。然后 Integer 对象无法与数值进行直接比较，所以 i4 自动拆箱转为 int 值 40，最终这条语句转为 40 == 40 进行数值比较。

## 运算符

### [算术运算符]()

算术运算符的操作对象必须是数值类型，不能为boolean类型使用算术运算符，但是可以为char类型使用算术运算符。因为在Java中，char类型在本质上是int的子集。

| 运算符 |         含义         |
| :----: | :------------------: |
|   +    | 加法（也是一元加号） |
|   -    | 减法（也是一元减号） |
|   *    |         乘法         |
|   /    |         除法         |
|   %    |         求模         |
|   ++   |         自增         |
|  \- -  |         自减         |
|   +=   |       加并赋值       |
|   -=   |       减并赋值       |
|   *=   |       乘并赋值       |
|   /=   |       除并赋值       |
|   %=   |      求模并赋值      |

### [位运算符]()

- Java定义了几个位运算符，可用于整数类型——long，int，short，char和byte。

  | 运算符  |       含义       |
  | :-----: | :--------------: |
  |    ~    |   按位一元取反   |
  |    &    |      按位与      |
  | &#124;  |      按位或      |
  |    ^    |     按位异或     |
  |   \>>   |       右移       |
  |  \>>>   |    右移零填充    |
  |   <<    |       左移       |
  |   &=    |   按位与并赋值   |
  | &#124;= |   按位或并赋值   |
  |   ^=    |  按位异或并赋值  |
  |  \>>=   |    右移并赋值    |
  |  \>>>=  | 右移零填充并赋值 |
  |   <<=   |    左移并赋值    |

- 在Java中，所有整数类型都由宽度可变的二进制数字表示，除char类型外都是有符号整数，这意味着它们即可表示正数，也可以表示负数。

- Java中使用“2的补码”进行编码，即负数的表示方法为：首先反转数值中的所有位（1变为0，0变为1），然后再将结果加1。例如，-42的表示方法为：通过反转42中的所有位（00101010），得到11010101，然后再加1，得到11010110，即-42。
  为了解码负数，首先反转所有位，然后加1。例如，反转-42（11010110），得到00101001，即41，再加一则得到42。

#### 左移

- 左移运算符“<<”可以将数值中的所有位向左移动指定的次数，格式为

  ```java
  value << num
  ```

  - num指定了将value中的值向左移动的次数，对于高阶位，每次左移都被移出并丢失，右边的位用0补充。这意味着左移int类型操作数时，如果某些位一旦超出31位，那么这些位将丢失。如果操作数是long类型，那么超出位63的位会丢失。
  - 当左移byte和short型数据时，Java的自动类型提升会导致意外的结果。当对表达式进行求值时，byte和short型数值会被提升为int类型，且表达式的结果也是int型。
  - 这意味着对byte和short型数值进行左移操作的结果为int型，若移动的位数不超出位31，则移动的位不会丢失。此外，当将负的byte和short型数值提升为int型时，会进行符号扩展，因此高阶位将使用1填充。
  - 例如，如果左移byte型数值，会先将该数值提升为int型，然后左移。这意味着如果想要的结果是移位后的byte型数值，就必须丢弃结果的前三个字节，可以通过将结果强制转换为byte类型来完成位数截取。

- 举个例子：

  ```java
  public static void main(String[] args) {
  	public static void main(String[] args) {
  		//0011 1100
  		byte a = 60;
  		// a首先被提升为int类型，即（0000 0000 0000 0000 0000 0000 0011 1100）
  		// 左移两位，结果为（0000 0000 0000 0000 0000 0000 1111 0000），即240
  		int i = a << 2;
  		// 先左移两位，结果为（0000 0000 0000 0000 0000 0011 1100 0000）
  		// 舍弃前三个字节，得到（1100 0000），即-64
  		byte b = (byte) (i << 2);
  		System.out.println("i等于:" + i);
  		System.out.println("b等于:" + b);
  	}
  }
  ```

  - 输出结果是：

  ```java
  i等于:240
  b等于:-64
  ```

  - 因为每次左移都相当于将原始值乘2，所以可以将之作为乘法的搞笑替代方法。但是如果将二进制1移进高阶位，结果将会变成负数。



####  右移

- 右移的规则与左移类似，实例代码如下：

  ```java
  public static void main(String[] args) {
  	//0011 1100
  	byte a = 60;  
  	// a首先被提升为int类型，即（0000 0000 0000 0000 0000 0000 0011 1100）
  	// 右移两位，结果为（0000 0000 0000 0000 0000 0000 0000 1111），即15
  	int i = a >> 2;
  	// 先右移两位，结果为（0000 0000 0000 0000 0000 0000 0000 0011）
  	// 舍弃前三个字节，得到（0000 0011），即3
  	byte b = (byte) (i >> 2);
  	System.out.println("i等于:" + i);
  	System.out.println("b等于:" + b);
  }
  ```

  - 执行结果

  ```java
  i等于:15
  b等于:3
  ```

- 每次右移一位，相当于将该值除以2，并舍弃所有余数。可以利用这一特性实现高效的除法操作。

  - 当进行右移操作时，右移后的顶部（最左边）位使用右移前顶部为使用的值填充，这称为符号扩展。当对负数进行右移操作时，该特性可以保留负数的符号。

  ```java
  public static void main(String[] args) {
  	byte a=(byte) 0b11111000;
  	System.out.println("a等于："+a);
  	int b=a>>1;
  	System.out.println("b等于："+b);
  }
  ```

  - 执行结果

  ```java
  a等于：-8
  b等于：-4
  ```



#### 无符号右移

- 每次移位时，“>>”运算符自动使用原来的内容填充高阶位，这个特性可以保持数值的正负性。但是，有时候对那些非数值的内容进行移位操作，并不关心高阶位初始值是多少，只希望用0来填充高阶位，这就是无符号右移。

  - 为了完成无符号右移，需要使用Java的无符号右移运算符“>>>”，该运算符总是将0移进高阶位。

  ```java
  public static void main(String[] args) {
  	//二进制表示（11111111 11111111 11111111 11111111）
  	int a=-1;
  	System.out.println(a);
  	//右移二十四位（00000000 00000000 00000000 11111111）
  	a=a>>>24;
  	//输出结果是 255
  	System.out.println(a); 
  }
  ```



### [关系运算符]()

- 关系运算符用于判定一个操作数与另一个操作数之间的关系。

  | 运算符 |   结果   |
  | :----: | :------: |
  |   ==   |   等于   |
  |   !=   |  不等于  |
  |   >    |   大于   |
  |   <    |   小于   |
  |  \>=   | 大于等于 |
  |   <=   | 小于等于 |




### [逻辑运算符]()

- 关系运算符用于判定一个操作数与另一个操作数之间的关系。

  |    运算符    |      结果      |
  | :----------: | :------------: |
  |      &       |     逻辑与     |
  |    &#124;    |     逻辑或     |
  |      ^       |    逻辑异或    |
  | &#124;&#124; |     短路或     |
  |      &&      |     短路与     |
  |      !       |   逻辑一元非   |
  |      &=      |  逻辑与并赋值  |
  |   &#124;=    |  逻辑或并赋值  |
  |      ^=      | 逻辑异或并赋值 |
  |      ==      |      等于      |
  |      !=      |     不等于     |
  |      ?:      |   三元运算符   |

###[三元运算符]()

[Java](http://c.biancheng.net/java/) 提供了一个特别的三元运算符（也叫三目运算符）经常用于取代某个类型的 if-then-else 语句。条件运算符的符号表示为“?:”，使用该运算符时需要有三个操作数，因此称其为三目运算符。使用条件运算符的一般语法结构为：

```
result = <expression> ? <statement1> : <statement3>;
```

其中，expression 是一个布尔表达式。当 expression 为真时，执行 statement1， 否则就执行 statement3。此三元运算符要求返回一个结果，因此要实现简单的二分支程序，即可使用该条件运算符。

下面是一个使用条件运算符的示例。

```java
int x,y,z;
x = 6,y = 2;
z = x>y ? x-y : x+y;
```



在这里要计算 z 的值，首先要判断 x>y 表达的值，如果为 true，z 的值为 x-y；否则 z 的值为 x+y。很明显 x>y 表达式结果为 true，所以 z 的值为 4。

技巧：可以将条件运算符理解为 if-else 语句的简化形式，在使用较为简单的表达式时，使用该运算符能够简化程序代码，使程序更加易读。

在使用条件运算符时，还应该注意优先级问题，例如下面的表达式：

```java
x>y ? x-=y : x+=y;
```

在编译时会出现语法错误，因为条件运算符优先于赋值运算符，上面的语句实际等价于：

```java
(x>y ? x-=y : x)+=y;
```

而运算符“+=”是赋值运算符，该运算符要求左操作数应该是一个变量，因此出现错误。为了避免这类错误，可以使用括号“0”来加以区分。例如，下面是正确的表达式。

```java
(x>y) ? (x-=y): (x+=y);
```

#### 例 1

在程序中声明 3 个变量 x、y、z，并由用户从键盘输入 x 的值，然后使用条件运算符向变量 y 和变量 z 赋值。 实现代码如下：

```java
public class Test9 {
    public static void main(String[] args) {
        int x, y, z; // 声明三个变量
        System.out.print("请输入一个数：");
        Scanner input = new Scanner(System.in);
        x = input.nextInt(); // 由用户输入x的值
        // 判断x的值是否大于5，如果是y=x，否则y=-x
        y = x > 5 ? x : -x;
        // 判断y的值是否大于x，如果是z=y，否则z=5
        z = y > x ? y : 5;
        System.out.printf("x=%d \n", x);
        System.out.printf("y=%d \n", y);
        System.out.printf("z=%d \n", z);
    }
}
```



保存程序并运行，运行效果如图 1 和图 2 所示：



![键盘输入58](http://c.biancheng.net/uploads/allimg/190910/5-1Z9101JZ3933.png)
图 1 键盘输入58

![键盘输入4](http://c.biancheng.net/uploads/allimg/190910/5-1Z9101J934391.png)
图 2 键盘输入4


在该程序中，首先输入 x 的值为 58，然后判断 x 的值是否大于 5，显然条件是成立，则 y 的值为 x，即 y=58。接着判断 y 的值是否大于 x，因为 y 的值和 x 的值都为 58，所以该条件是不成立的，则 z=5。再次输入 x 的值为 4，然后判断 x 的值是否大于 5，不成立，则 y=-4；接着判断 y 的值是否大于 x，不成立，则 z=5。

## 方法

### [什么是方法的返回值?返回值在类的方法里的作用是什么?]()

方法的返回值是指我们获取到的某个方法体中的代码执行后产生的结果！（前提是该方法可能产生结果）。返回值的作用是接收出结果，使得它可以用于其他的操作！

### [为什么 Java 中只有值传递？]()

首先回顾一下在程序设计语言中有关将参数传递给方法（或函数）的一些专业术语。**按值调用(call by value)表示方法接收的是调用者提供的值，而按引用调用（call by reference)表示方法接收的是调用者提供的变量地址。一个方法可以修改传递引用所对应的变量值，而不能修改传递值调用所对应的变量值。** 它用来描述各种程序设计语言（不只是 Java)中方法参数传递方式。

**Java 程序设计语言总是采用按值调用。也就是说，方法得到的是所有参数值的一个拷贝，也就是说，方法不能修改传递给它的任何参数变量的内容。**

**下面通过 3 个例子来给大家说明**

> **example 1**

```java
public static void main(String[] args) {
    int num1 = 10;
    int num2 = 20;

    swap(num1, num2);

    System.out.println("num1 = " + num1);
    System.out.println("num2 = " + num2);
}

public static void swap(int a, int b) {
    int temp = a;
    a = b;
    b = temp;

    System.out.println("a = " + a);
    System.out.println("b = " + b);
}
```

**结果：**

```
a = 20
b = 10
num1 = 10
num2 = 20
```

**解析：**

![example 1 ](http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-9-27/22191348.jpg)

在 swap 方法中，a、b 的值进行交换，并不会影响到 num1、num2。因为，a、b 中的值，只是从 num1、num2 的复制过来的。也就是说，a、b 相当于 num1、num2 的副本，副本的内容无论怎么修改，都不会影响到原件本身。

**通过上面例子，我们已经知道了一个方法不能修改一个基本数据类型的参数，而对象引用作为参数就不一样，请看 example2.**

> **example 2**

```java
    public static void main(String[] args) {
        int[] arr = { 1, 2, 3, 4, 5 };
        System.out.println(arr[0]);
        change(arr);
        System.out.println(arr[0]);
    }

    public static void change(int[] array) {
        // 将数组的第一个元素变为0
        array[0] = 0;
    }
```

**结果：**

```Java
1
```

**解析：**

![example 2](http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-9-27/3825204.jpg)

array 被初始化 arr 的拷贝也就是一个对象的引用，也就是说 array 和 arr 指向的是同一个数组对象。 因此，外部对引用对象的改变会反映到所对应的对象上。

**通过 example2 我们已经看到，实现一个改变对象参数状态的方法并不是一件难事。理由很简单，方法得到的是对象引用的拷贝，对象引用及其他的拷贝同时引用同一个对象。**

**很多程序设计语言（特别是，C++和 Pascal)提供了两种参数传递的方式：值调用和引用调用。有些程序员（甚至本书的作者）认为 Java 程序设计语言对对象采用的是引用调用，实际上，这种理解是不对的。由于这种误解具有一定的普遍性，所以下面给出一个反例来详细地阐述一下这个问题。**

> **example 3**

```java
public class Test {

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        Student s1 = new Student("小张");
        Student s2 = new Student("小李");
        Test.swap(s1, s2);
        System.out.println("s1:" + s1.getName());
        System.out.println("s2:" + s2.getName());
    }

    public static void swap(Student x, Student y) {
        Student temp = x;
        x = y;
        y = temp;
        System.out.println("x:" + x.getName());
        System.out.println("y:" + y.getName());
    }
}
```

**结果：**

```java
x:小李
y:小张
s1:小张
s2:小李
```

**解析：**

交换之前：

![img](http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-9-27/88729818.jpg)

交换之后：

![img](http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-9-27/34384414.jpg)

通过上面两张图可以很清晰的看出： **方法并没有改变存储在变量 s1 和 s2 中的对象引用。swap 方法的参数 x 和 y 被初始化为两个对象引用的拷贝，这个方法交换的是这两个拷贝**

> **总结**

Java 程序设计语言对对象采用的不是引用调用，实际上，对象引用是按 值传递的。

下面再总结一下 Java 中方法参数的使用情况：

- 一个方法不能修改一个基本数据类型的参数（即数值型或布尔型）。
- 一个方法可以改变一个对象参数的状态。
- 一个方法不能让对象参数引用一个新的对象。

### [重载和重写的区别]()

> 重载就是同样的一个方法能够根据输入数据的不同，做出不同的处理
>
> 重写就是当子类继承自父类的相同方法，输入数据一样，但要做出有别于父类的响应时，你就要覆盖父类方法

#### [重载]()

发生在同一个类中，方法名必须相同，参数类型不同、个数不同、顺序不同，方法返回值和访问修饰符可以不同。

下面是《Java 核心技术》对重载这个概念的介绍：

![img](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/bg/desktopjava%E6%A0%B8%E5%BF%83%E6%8A%80%E6%9C%AF-%E9%87%8D%E8%BD%BD.jpg)

**综上：重载就是同一个类中多个同名方法根据不同的传参来执行不同的逻辑处理。**

####[重写]()

重写发生在运行期，是子类对父类的允许访问的方法的实现过程进行重新编写。

1. 返回值类型、方法名、参数列表必须相同，抛出的异常范围小于等于父类，访问修饰符范围大于等于父类。
2. 如果父类方法访问修饰符为 `private/final/static` 则子类就不能重写该方法，但是被 static 修饰的方法能够被再次声明。
3. 构造方法无法被重写

**综上：重写就是子类对父类方法的重新改造，外部样子不能改变，内部逻辑可以改变**

**暖心的 Guide 哥最后再来个图表总结一下！**

| 区别点     | 重载方法 | 重写方法                                                     |
| ---------- | -------- | ------------------------------------------------------------ |
| 发生范围   | 同一个类 | 子类                                                         |
| 参数列表   | 必须修改 | 一定不能修改                                                 |
| 返回类型   | 可修改   | 子类方法返回值类型应比父类方法返回值类型更小或相等           |
| 异常       | 可修改   | 子类方法声明抛出的异常类应比父类方法声明抛出的异常类更小或相等； |
| 访问修饰符 | 可修改   | 一定不能做更严格的限制（可以降低限制）                       |
| 发生阶段   | 编译期   | 运行期                                                       |

**方法的重写要遵循“两同两小一大”**（以下内容摘录自《疯狂 Java 讲义》,[issue#892](https://github.com/Snailclimb/JavaGuide/issues/892) ）：

- “两同”即方法名相同、形参列表相同；
- “两小”指的是子类方法返回值类型应比父类方法返回值类型更小或相等，子类方法声明抛出的异常类应比父类方法声明抛出的异常类更小或相等；
- “一大”指的是子类方法的访问权限应比父类方法的访问权限更大或相等。

### [深拷贝 vs 浅拷贝]()

1. **浅拷贝**：对基本数据类型进行值传递，对引用数据类型进行引用传递般的拷贝，此为浅拷贝。
2. **深拷贝**：对基本数据类型进行值传递，对引用数据类型，创建一个新的对象，并复制其内容，此为深拷贝。

![deep and shallow copy](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-7/java-deep-and-shallow-copy.jpg)

### [方法的四种类型]()

1、无参数无返回值的方法

```java
// 无参数无返回值的方法(如果方法没有返回值，不能不写，必须写void，表示没有返回值)
public void f1() {
    System.out.println("无参数无返回值的方法");
}
```

2、有参数无返回值的方法

```java
/**
* 有参数无返回值的方法
* 参数列表由零组到多组“参数类型+形参名”组合而成，多组参数之间以英文逗号（,）隔开，形参类型和形参名之间以英文空格隔开
*/
public void f2(int a, String b, int c) {
    System.out.println(a + "-->" + b + "-->" + c);
}
```

3、有返回值无参数的方法

```java
// 有返回值无参数的方法（返回值可以是任意的类型,在函数里面必须有return关键字返回对应的类型）
public int f3() {
    System.out.println("有返回值无参数的方法");
    return 2;
}
```

4、有返回值有参数的方法

```java
// 有返回值有参数的方法
public int f4(int a, int b) {
    return a * b;
}
```

5、return 在无返回值方法的特殊使用

```java
// return在无返回值方法的特殊使用
public void f5(int a) {
    if (a > 10) {
        return;//表示结束所在方法 （f5方法）的执行,下方的输出语句不会执行
    }
    System.out.println(a);
}
```

## Java面向对象

### [类和对象]()

#### [面向对象和面向过程的区别]()

- **面向过程** ：**面向过程性能比面向对象高。** 因为类调用时需要实例化，开销比较大，比较消耗资源，所以当性能是最重要的考量因素的时候，比如单片机、嵌入式开发、Linux/Unix 等一般采用面向过程开发。但是，**面向过程没有面向对象易维护、易复用、易扩展。**
- **面向对象** ：**面向对象易维护、易复用、易扩展。** 因为面向对象有封装、继承、多态性的特性，所以可以设计出低耦合的系统，使系统更加灵活、更加易于维护。但是，**面向对象性能比面向过程低**。

参见 issue : [面向过程 ：面向过程性能比面向对象高？？](https://github.com/Snailclimb/JavaGuide/issues/431)

> 这个并不是根本原因，面向过程也需要分配内存，计算内存偏移量，Java 性能差的主要原因并不是因为它是面向对象语言，而是 Java 是半编译语言，最终的执行代码并不是可以直接被 CPU 执行的二进制机械码。
>
> 而面向过程语言大多都是直接编译成机械码在电脑上执行，并且其它一些面向过程的脚本语言性能也并不一定比 Java 好。

#### [构造器 Constructor 是否可被 override?]()

Constructor 不能被 override（重写）,但是可以 overload（重载）,所以你可以看到一个类中有多个构造函数的情况。

#### [在 Java 中定义一个不做事且没有参数的构造方法的作用]()

Java 程序在执行子类的构造方法之前，如果没有用 `super()`来调用父类特定的构造方法，则会调用父类中“没有参数的构造方法”。因此，如果父类中只定义了有参数的构造方法，而在子类的构造方法中又没有用 `super()`来调用父类中特定的构造方法，则编译时将发生错误，因为 Java 程序在父类中找不到没有参数的构造方法可供执行。解决办法是在父类里加上一个不做事且没有参数的构造方法。



#### [成员变量与局部变量的区别有哪些？]()

1. 从语法形式上看:成员变量是属于类的，而局部变量是在代码块或方法中定义的变量或是方法的参数；成员变量可以被 public,private,static 等修饰符所修饰，而局部变量不能被访问控制修饰符及 static 所修饰；但是，成员变量和局部变量都能被 final 所修饰。
2. 从变量在内存中的存储方式来看:如果成员变量是使用`static`修饰的，那么这个成员变量是属于类的，如果没有使用`static`修饰，这个成员变量是属于实例的。而对象存在于堆内存，局部变量则存在于栈内存。
3. 从变量在内存中的生存时间上看:成员变量是对象的一部分，它随着对象的创建而存在，而局部变量随着方法的调用而自动消失。
4. 成员变量如果没有被赋初值:则会自动以类型的默认值而赋值（一种情况例外:被 final 修饰的成员变量也必须显式地赋值），而局部变量则不会自动赋值。

#### [创建一个对象用什么运算符?对象实体与对象引用有何不同?]()

new 运算符，new 创建对象实例（对象实例在堆内存中），对象引用指向对象实例（对象引用存放在栈内存中）。一个对象引用可以指向 0 个或 1 个对象（一根绳子可以不系气球，也可以系一个气球）;一个对象可以有 n 个引用指向它（可以用 n 条绳子系住一个气球）。

#### [一个类的构造方法的作用是什么? 若一个类没有声明构造方法，该程序能正确执行吗? 为什么?]()

主要作用是完成对类对象的初始化工作。可以执行。因为一个类即使没有声明构造方法也会有默认的不带参数的构造方法。如果我们自己添加了类的构造方法（无论是否有参），Java 就不会再添加默认的无参数的构造方法了，这时候，就不能直接 new 一个对象而不传递参数了，所以我们一直在不知不觉地使用构造方法，这也是为什么我们在创建对象的时候后面要加一个括号（因为要调用无参的构造方法）。如果我们重载了有参的构造方法，记得都要把无参的构造方法也写出来（无论是否用到），因为这可以帮助我们在创建对象的时候少踩坑。

#### [构造方法有哪些特性？]()

1. 名字与类名相同。
2. 没有返回值，但不能用 void 声明构造函数。
3. 生成类的对象时自动执行，无需调用。

#### [ 在调用子类构造方法之前会先调用父类没有参数的构造方法,其目的是?]()

帮助子类做初始化工作。

#### [对象的相等与指向他们的引用相等,两者有什么不同?]()

对象的相等，比的是内存中存放的内容是否相等。而引用相等，比较的是他们指向的内存地址是否相等。

###[面向对象的三大特征]()

`封装，多态，继承面向对象的三大特征`

#### [封装]()

`封装的原则：`

+ 将不需要对外提供的内容都隐藏起来。
+ 把属性隐藏，提供公共方法对其访问。

封装是指把一个对象的状态信息（也就是属性）隐藏在对象内部，不允许外部对象直接访问对象的内部信息。但是可以提供一些可以被外界访问的方法来操作属性。就好像我们看不到挂在墙上的空调的内部的零件信息（也就是属性），但是可以通过遥控器（方法）来控制空调。如果属性不想被外界访问，我们大可不必提供方法给外界访问。但是如果一个类没有提供给外界访问的方法，那么这个类也没有什么意义了。就好像如果没有空调遥控器，那么我们就无法操控空凋制冷，空调本身就没有意义了（当然现在还有很多其他方法 ，这里只是为了举例子）。

```java
public class Student {
    private int id;//id属性私有化
    private String name;//name属性私有化

    //获取id的方法
    public int getId() {
        return id;
    }

    //设置id的方法
    public void setId(int id) {
        this.id = id;
    }

    //获取name的方法
    public String getName() {
        return name;
    }

    //设置name的方法
    public void setName(String name) {
        this.name = name;
    }
}
```

#### [继承]()

##### 1.继承简单概述

- 多个类中存在相同属性和行为时，将这些内容抽取到单独一个类中，那么多个类无需再定义这些属性和行为，只要继承那个类即可。

##### 02.继承格式

* 通过extends关键字可以实现类与类的继承
* class 子类名 extends 父类名 {} 
* 单独的这个类称为父类，基类或者超类；这多个类可以称为子类或者派生类

##### 03.继承好处和弊端

- **继承的好处**
  * a:提高了代码的复用性
  * b:提高了代码的维护性
  * c:让类与类之间产生了关系，是多态的前提
- **继承的弊端**
  * 类的耦合性增强了。
  * 开发的原则：高内聚，低耦合。
  * 耦合：类与类的关系
  * 内聚：就是自己完成某件事情的能力

##### 04.继承的注意事项

- **继承的注意事项**
  * a:子类只能继承父类所有非私有的成员(成员方法和成员变量)
  * b:子类不能继承父类的构造方法，但是可以通过super(待会儿讲)关键字去访问父类构造方法。
  * c:不要为了部分功能而去继承
- **继承中构造方法的注意事项**
  * 父类没有无参构造方法,子类怎么办?
    * a: 在父类中添加一个无参的构造方法
    * b:子类通过super去显示调用父类其他的带参的构造方法
    * c:子类通过this去调用本类的其他构造方法
    * 本类其他构造也必须首先访问了父类构造
  * B:注意事项
    * super(…)或者this(….)必须出现在第一条语句上

#####05.继承中成员变量的关系

- 继承中成员变量的关系
  * A:子类中的成员变量和父类中的成员变量名称不一样
  * B:子类中的成员变量和父类中的成员变量名称一样
  * 在子类中访问一个变量的查找顺序("就近原则")
    * a: 在子类的方法的局部范围找,有就使用
    * b: 在子类的成员范围找,有就使用
    * c: 在父类的成员范围找,有就使用
      * d:如果还找不到,就报错

#####06.不支持多继承影响

- Java 不支持多继承影响
  - Java 相比于其他面向对象语言，如 C++，设计上有一些基本区别，比如Java 不支持多继承。这种限制，在规范了代码实现的同时，也产生了一些局限性，影响着程序设计结构。Java 类可以实现多个接口，因为接口是抽象方法的集合，所以这是声明性的，但不能通过扩展多个抽象类来重用逻辑。
  - 在一些情况下存在特定场景，需要抽象出与具体实现、实例化无关的通用逻辑，或者纯调用关系的逻辑，但是使用传统的抽象类会陷入到单继承的窘境。
- 为什么是单继承而不能多继承呢？
  - 若为多继承，那么当多个父类中有重复的属性或者方法时，子类的调用结果会含糊不清，因此用了单继承。
  - 多继承虽然能使子类同时拥有多个父类的特征，但是其缺点也是很显著的，主要有两方面：
    - 如果在一个子类继承的多个父类中拥有相同名字的实例变量，子类在引用该变量时将产生歧义，无法判断应该使用哪个父类的变量。
    - 如果在一个子类继承的多个父类中拥有相同方法，子类中有没有覆盖该方法，那么调用该方法时将产生歧义，无法判断应该调用哪个父类的方法。
  - Java是从C++语言上优化而来，而C++也是面向对象的，为什么它却可以多继承的呢？首先，C++语言是1983年在C语言的基础上推出的，Java语言是1995年推出的。其次，在C++被设计出来后，就会经常掉入多继承这个陷阱，虽然它也提出了相应的解决办法，但Java语言本着简单的原则舍弃了C++中的多继承，这样也会使程序更具安全性。
- 为什么是多实现呢？
  - 通过实现接口拓展了类的功能，若实现的多个接口中有重复的方法也没关系，因为实现类中必须重写接口中的方法，所以调用时还是调用的实现类中重写的方法。

#### [多态]()

##### 1.什么是多态

多态是指程序中定义的引用变量所指向的具体类型和通过该引用变量发出的方法调用在编程时并不确定，而是在程序运行期间才确定，即一个引用变量倒底会指向哪个类的实例对象，该引用变量发出的方法调用到底是哪个类中实现的方法，必须在由程序运行期间才能决定。因为在程序运行时才确定具体的类，这样，不用修改源程序代码，就可以让引用变量绑定到各种不同的类实现上，从而导致该引用调用的具体方法随之改变，即不修改程序代码就可以改变程序运行时所绑定的具体代码，让程序可以选择多个运行状态，这就是多态性。

##### 2.多态的实现条件

- Java实现多态有三个必要条件：继承、重写、向上转型。
- 继承：在多态中必须存在有继承关系的子类和父类。
- 重写：子类对父类中某些方法进行重新定义，在调用这些方法时就会调用子类的方法。
- 向上转型：在多态中需要将子类的引用赋给父类对象，只有这样该引用才能够具备技能调用父类的方法和子类的方法。

##### 3.多态实现方式

多态作用：多态性就是相同的消息使得不同的类做出不同的响应。

第一种实现方式：基于继承实现的多态

- 基于继承的实现机制主要表现在父类和继承该父类的一个或多个子类对某些方法的重写，多个子类对同一方法的重写可以表现出不同的行为。多态的表现就是不同的对象可以执行相同的行为，但是他们都需要通过自己的实现方式来执行，这就要得益于向上转型了。

```java
public class MainJava {
    public static void main(String[] args) {
        //定义父类数组
        Wine[] wines = new Wine[2];
        //定义两个子类
        Test1 test1 = new Test1();
        Test2 test2 = new Test2();
        Wine win e = new Wine();
        //父类引用子类对象
        wines[0] = test1;
        wines[1] = test2;
        for(int i = 0 ; i < 2 ; i++){
            System.out.println(wines[i].toString() + "--" + wines[i].drink());
        }
        System.out.println("-------------------------------");
        System.out.println(test1.toString() + "--" + test1.drink());
        System.out.println(test2.toString() + "--" + test2.drink());
    }
    public static class Wine {
        private String name;
        public String getName() {
            return name;
        }
        public void setName(String name) {
            this.name = name;
        }
        public String drink(){
            return "喝的是 " + getName();
        }
        public String toString(){
            return null;
        }
    }

    public static class Test1 extends Wine{
        public Test1(){
            setName("Test1");
        }
        public String drink(){
            return "喝的是 " + getName();
        }
        public String toString(){
            return "Wine : " + getName();
        }
    }

    public static class Test2 extends Wine{
        public Test2(){
            setName("Test2");
        }
        public String drink(){
            return "喝的是 " + getName();
        }
        public String toString(){
            return "Wine : " + getName();
        }
    }
}
```

第二种实现多态的方式：基于接口实现的多态

- 继承是通过重写父类的同一方法的几个不同子类来体现的，那么就可就是通过实现接口并覆盖接口中同一方法的几不同的类体现的。
- 在接口的多态中，指向接口的引用必须是指定这实现了该接口的一个类的实例程序，在运行时，根据对象引用的实际类型来执行对应的方法。
- 继承都是单继承，只能为一组相关的类提供一致的服务接口。但是接口可以是多继承多实现，它能够利用一组相关或者不相关的接口进行组合与扩充，能够对外提供一致的服务接口。所以它相对于继承来说有更好的灵活性。

##### 4.多态的好处和弊端

###### 4.1多态的好处

A:提高了代码的维护性(继承保证)

B:提高了代码的扩展性(由多态保证)

4.2多态的弊端

转型的话，不能使用子类特有的属性和行为

```java
class Demo_SuperMan {
    public static void main(String[]args){
        Person p=new SuperMan();//父类引用指向子类对象。超人提升为了人
                                //父类引用指向子类对象，就是向上转型
        System.out.println(p.name);
        p.Tsy();
        //p.Fly();//找不到该方法
        SuperMan sm=(SuperMan)p;//向下转型,看到整个对象的内容
        sm.Fly();
    }
}
 
class Person{
    String name="John";
    public void Tsy(){
        System.out.println("Tsy");
    }
}
 
class SuperMan extends Person{
    String name="SuperName";
    @Override
    public void Tsy(){
        System.out.println("子类Tsy");
    }
 
    public void Fly(){
        System.out.println("飞出去救人");
    }
}
```

#### 接口

#####01.什么是接口

- 接口（Interface）在Java语言中是一个抽象类型，是服务提供者和服务使用者之间的一个协议，在JDK1.8之前一直是抽象方法的集合，一个类通过实现接口从而来实现两者间的协议
- 接口可以定义字段和方法。在JDK1.8之前，接口中所有的方法都是抽象的，从JDK1.8开始，也可以在接口中编写默认的和静态的方法。除非显式指定，否则接口方法都是抽象的

#####02.接口特点

- 从 Java 8 开始，接口也可以拥有默认的方法实现，这是因为不支持默认方法的接口的维护成本太高了。在 Java 8 之前，如果一个接口想要添加新的方法，那么要修改所有实现了该接口的类。
- 接口的特点有哪些呢？
  - 接口没有构造方法
  - 接口不能用于实例化对象
  - 接口中的字段必须初始化，并且隐式地设置为公有的、静态的和final的。因此，为了符合规范，接口中的字段名要全部大写
  - 接口不是被类继承，而是要被类实现
  - 接口中每一个方法默认是公有和抽象的，即接口中的方法会被隐式的指定为 **public abstract**。从JDK 1.8开始，可以在接口中编写默认的和静态的方法。声明默认方法需要使用关键字**default**。并且不允许定义为 private 或者 protected。
  - 当类实现接口时，类要实现接口中所有的方法。否则，类必须声明为抽象的
  - 接口支持多重继承，即可以继承多个接口

##### 03看一个接口案例代码

```java
public interface Name {
    
    //接口中的变量其实就是常量，默认被final修饰
    int age = 10;

	String getName();
	// 等价于以下三种形式
	// public String getName();
	// public abstract String getName();
	// abstract String getName();

	// 静态方法，可以省略public声明，因为在接口中的静态方法默认就是公有的
	public static void setName(String name) {
		// 实现具体业务
	}
	
	// 默认方法
    default void defaultMethod(){
		// 实现具体业务
		System.out.println("defaultMethod");
	}

}
```



#####04Marker Interface

- 接口的职责也不仅仅限于抽象方法的集合，其实有各种不同的实践。
- 有一类没有任何方法的接口，通常叫作 Marker Interface，顾名思义，它的目的就是为了声明某些东西，比如我们熟知的 Cloneable、Serializable 等。这种用法，也存在于业界其他的 Java 产品代码中。

#####05.java 8接口变化

- 从 Java 8 开始，interface 增加了对 default method 的支持。Java 9 以后，甚至可以定义 private default method。Default method 提供了一种二进制兼容的扩展已有接口的办法。比如，我们熟知的 java.util.Collection，它是 collection 体系的 root interface，在 Java 8 中添加了一系列 default method，主要是增加 Lambda、Stream 相关的功能。

```java
public interface Collection<E> extends Iterable<E> {
     default Stream<E> stream() {
         return StreamSupport.stream(spliterator(), false);
     }
}
```



#### Java抽象类

#####01.为何需要抽象类

- 在面向对象的概念中，所有的对象都是通过类来描绘的。但并不是所有的类都是用来描绘对象的，如果一个类中没有包含足够的信息来描绘一个具体的对象，这样的类就是抽象类（Abstract）。

#####02.抽象类特点

- 抽象类除了不能实例化对象之外，类的其它功能依然存在，成员变量、成员方法和构造方法的访问方式和普通类一样。

  - 抽象类和抽象方法都使用 abstract 关键字进行声明。抽象类一般会包含抽象方法，抽象方法一定位于抽象类中。
  - 抽象类和普通类最大的区别是，抽象类不能被实例化，需要继承抽象类才能实例化其子类。其目的主要是代码重用。
  - 抽象类大多用于抽取相关 Java 类的共用方法实现或者是共同成员变量，然后通过继承的方式达到代码复用的目的。

  ```java
  public abstract class AbstractClassExample {
  
      protected int x;
      private int y;
  
      public abstract void func1();
  
      public void func2() {
          System.out.println("func2");
      }
  }
  
  public class AbstractExtendClassExample extends AbstractClassExample {
      @Override
      public void func1() {
          System.out.println("func1");
      }
  }
  ```



#####03.抽象类可以new吗

- 注意抽象类是不能被实例化的，也就是不能new出来的！
  - 如果执意需要new，则会提示
  - ![image](https://upload-images.jianshu.io/upload_images/4432347-7519b80e53e22ea6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#####04.抽象类设计注意要点

- 如果想要设计这样一个类，该类包含一个特别的成员方法，方法的具体实现由它的子类确定，那么可以在父类中声明该方法为抽象方法
- Abstract关键字同样可以用来声明抽象方法，抽象方法只包含一个方法名，而没有方法体。声明抽象方法会造成以下两个结果：
  - 如果一个类包含抽象方法，则该类必须声明为抽象类
  - 子类必须重写父类的抽象方法，否则自身也必须声明为抽象类

#####05.抽象类名作为形参

- 案例

  ```java
  /*抽象类作为参数的时候如何进行调用*/
  abstract class Animal {
      // 定义一个抽象方法
      public abstract void eat() ;
  }
  
  // 定义一个类
  class Cat extends Animal {
      public void eat(){
          System.out.println("吃.................") ;
      }
  }
  
  
  // 定义一个类
  class AnimalDemo {
      public void method(Animal a) {
          a.eat() ;
      }
  }
  
  // 测试类
  class ArgsDemo2  {
      public static void main(String[] args) {
          // 创建AnimalDemo的对象
          AnimalDemo ad = new AnimalDemo() ;
          // 对Animal进行间接实例化
          // Animal a = new Cat() ;
          Cat a = new Cat() ;
          // 调用method方法
          ad.method(a) ;
      }
  }
  ```

####内部类

#####01 Java中的内部类共分为四种：

- 静态内部类static inner class (also called nested class)
- 成员内部类member inner class
- 局部内部类local inner class
- 匿名内部类anonymous inner class

#####02.内部类概述和访问特点

- A:内部类概述:   
  * 把类定义在其他类的内部，这个类就被称为内部类。
  * 举例：在类A中定义了一个类B，类B就是内部类。
- B:内部类访问特点
  * a:内部类可以直接访问外部类的成员，包括私有。
  * b:外部类要访问内部类的成员，必须创建对象。
- C：内部类作用
  - 内部类作用主要实现功能的隐藏、减少内存开销，提高程序的运行速度

######2.1 内部类分类及成员内部类的直接使用

* A:按照内部类位置分类
  * 成员位置:在成员位置定义的类，被称为成员内部类。   
  * 局部位置:在局部位置定义的类，被称为局部内部类。
* B:成员内部类
  * 如何在测试类中直接访问内部类的成员。
  * 格式:     外部类名.内部类名 对象名 = 外部类对象.内部类对象;

######2.2 成员内部类的常见修饰符及应用

* A:成员内部类的修饰符：
  * private     为了保证数据的安全性
  * static         为了方便访问数据
  * 注意事项: 
    * a:静态内部类访问的外部类数据必须用静态修饰。
    * b: 成员方法可以是静态的也可以是非静态的
* B:成员内部类被静态修饰后的访问方式是:
  * 格式:    外部类名.内部类名 对象名 = new 外部类名.内部类名();

######2.3局部内部类访问局部变量的问题

* A: 可以直接访问外部类的成员
* B: 可以创建内部类对象，通过对象调用内部类方法，来使用局部内部类功能
* C:局部内部类访问局部变量必须用final修饰
  * 为什么呢?
    * 因为局部变量会随着方法的调用完毕而消失，这个时候，局部对象并没有立马从堆内存中消失，还要使用那个变量。 为了让数据还能继续被使用，就用fianl修饰，这样，在堆内存里面存储的其实是一个常量值。
    * 当我们添加了final其实就是延长了生命周期 , 其实就是一个常量 , 常量在常量池中 , 在方法区中

#####03.内部类和外部类联系

- 内部类和外部类联系：
  - 内部类可以访问外部类所有的方法和属性，如果内部类和外部类有相同的成员方法和成员属性，内部类的成员方法调用要优先于外部类即内部类的优先级比较高（只限于类内部，在主方法内，内部类对象不能访问外部类的成员方法和成员属性），外部类只能访问内部类的静态常量或者通过创建内部类来访问内部类的成员属性和方法

#####04匿名内部类

######4.1 匿名内部类的格式和理解

* A:匿名内部类:    就是局部内部类的简化写法。

* B:前提：            存在一个类或者接口;这里的类可以是具体类也可以是抽象类。

* C:格式：

  ```java
  new 类名或者接口名(){
       重写方法;
  } ;
  ```

######4.2 本质是什么呢?

* 是一个继承了该类或者实现了该接口的子类匿名对象。

* 匿名内部类的面试题

  * A:面试题

    ```java
    按照要求，补齐代码
    interface Inter { void show(); }
    class Outer { //补齐代码 }
    class OuterDemo {
    public static void main(String[] args) {
            Outer.method().show();
        }
    }
    要求在控制台输出”HelloWorld”
    
    - 答案
    //补齐代码
    public static Inter method() {
        //匿名内部类
        return new Inter() {
            public void show(){
                System.out.println("HelloWorld") ;
            } ;
        }
    }
    ```

#####05.成员内部类介绍

- 要创建一个成员内部类的实例，需要拥有其外部类的一个实例的引用。假设外部类为A，成员内部类为B，则创建一个B类的实例的语法规则如下：

  ```java
  A a = new A();
  A.B b = a.new B();
  ```

- 那么实际案例代码如下所示

  ```java
  public class Outer {
  
      private int value = 10;
      
      private static int staticValue=11;
      
      protected  class Nested {
      	public int getValue() {
      		// 可以访问外部类的非静态、静态、私有成员
      		return value+staticValue;
      	}
      }
  }
  
  public static void main(String[] args) {
  	Outer outer=new Outer();
  	Outer.Nested nested=outer.new Nested();
  	System.out.println(nested.getValue());
  }
  ```

#####06.局部内部类介绍

- 局部内部类可以简称为局部类，局部类可以在任何代码块中声明，并且其作用域位于代码块之中。例如，可以在一个方法快、一个if语句块、一个while语句块中声明一个局部类

- 如果类的实例只在作用域内使用的话，使用局部类可以说是一个好办法

  ```java
  public interface Logger {
  	void log(String message);
  }
  
  public class Outer {
  
  	String time = LocalDateTime.now().format(DateTimeFormatter.ofLocalizedDateTime(FormatStyle.MEDIUM));
  
  	public Logger getLogger() {
  		class LoggerImpl implements Logger {
  			@Override
  			public void log(String message) {
  				System.out.println(time + " : " + message);
  			}
  		}
  		return new LoggerImpl();
  	}
  }
  
  
  public static void main(String[] args) {
  	Outer outer=new Outer();
  	Logger logger=outer.getLogger();
  	logger.log("Hi");
  }
  ```



## 枚举

### 01什么是枚举

枚举（Enum）是在Java 5中添加的新的类型

- 从技术上来讲，由于enum是一个类，一个enum可以有构造方法和方法。如果有构造方法，那必须是私有的。如果一个enum定义了枚举值之外的其他内容，枚举值必须在其他内容之前定义，并且最后的枚举值用一个分号结束

### 02枚举简单实用

#### 2.1枚举的创建

- 创建枚举需要使用到关键字 enum ，如下所示：

  ```java
  enum Letter{
  	A,B,C,D
  }
  ```

  - 标识符 A、B、C、D 等被称为枚举常量，每个枚举常量被隐式声明为Letter的公有静态final成员。每个枚举常量的类型是声明它们的枚举的类型。

#### 2.2枚举的使用

- 定义了枚举后，可以创建枚举类型的变量，但是不能使用new关键字来实例化枚举，而是通过与基本类型类似的方式声明，例如：

  ```java
  Letter letter1=Letter.A;
  Letter letter2=Letter.B;
  ```

- 可以使用关系运算符“==”来比较两个枚举变量的相等性，例如：

  ```java
  if (letter1 == letter2) {
  	System.out.println("相等");
  } else {
  	System.out.println("不相等");
  }
  ```

- 枚举值也可以用于控制switch语句，例如：

  ```java
  switch (letter1) {
      case A:
      	System.out.println("A");
      	break;
      case B:
      	System.out.println("B");
      	break;
  }
  ```

  - 在case语句中，枚举常量的名称没有使用枚举类型的名称进行限定，即使用的是 A 而不是 Letter.A ，这是因为 switch 表达式中的枚举类型已经隐式指定了case常量的枚举类型，所以在case语句中不需要使用枚举类型的名称对常量进行限定，如果试图这么做，会造成编译时错误

- 遍历打印枚举如下所示

```java
public enum Color {
	RED, GREEN, BLANK, YELLOW
}
// 遍历输出
for (Color color : Color.values()) {
	System.out.println(color);
}
```

- 输出结果为

  ```java 
  RED
  GREEN
  BLANK
  YELLOW
  ```

### 03.枚举是类类型

- Java中枚举是类类型，虽然不能使用new关键字来实例化枚举，但是枚举却有和其他类相同的功能，可以为枚举提供构造函数、实例变量和方法，甚至可以实现接口
  - 需要理解的是：每个枚举变量都是所属枚举类型的对象。因此，如果为枚举定义了构造函数，那么当创建每个枚举常量时都会调用该构造函数
  - 为枚举 Letter 提供一个实例变量 index、一个返回index值的方法、两个不同的构造函数。
  - 对于每一个枚举常量，指定要调用的构造函数的方法是通过每个常量后面的圆括号中来加以指定
- 看一下下面的案例代码

```java
public enum Letter {

	KK(), A(1), B(2), C(3), D(5);

	private int index;

	Letter(int index) {
		this.index = index;
	}

	Letter() {
		this.index = 0;
	}
	
	public int getIndex() {
		return index;
	}
}

public static void main(String[] args) {
	Letter letter = Letter.KK;
	//输出值为：0
	System.out.println("索引：" + letter.getIndex());
	 letter = Letter.B;
	 //输出值为：2
	System.out.println("索引：" + letter.getIndex());
}
```

- 此外，枚举有两条限制：
  - 1.枚举不能继承其他类。但是所有枚举都隐式自动继承超类 java.lang.Enum
  - 2.枚举不能是超类。即枚举不能进行扩展

### 04.枚举的一些方法

#### 4.1 values() 

- values() 方法返回一个包含枚举常量列表的数组，例如：

  ```java
  enum Letter {
  	A, B, C, D
  }
  
  public static void main(String[] args) {
  	Letter[] values = Letter.values();
  	for (Letter letter : values) {
  		System.out.println(letter);
  	}
  }
  ```


#### 4.2 valueOf(String) 

- valueOf(String) 方法返回与传递的字符串参数相对应的枚举常量，例如：

  ```java
  enum Letter {
  	A, B, C, D
  }
  
  public static void main(String[] args) {
  	String str = "A";
  	Letter le=Letter.valueOf(str);
  	//输出值为：A
  	System.out.println(le);
  }
  ```


#### 4.3 ordinal()

- ordinal() 方法返回枚举常量在常量列表中位置的值，这称为枚举常量的序数值，例如：

  ```java
  enum Letter {
  	A, B, C, D
  }
  
  public static void main(String[] args) {
  	Letter letter = Letter.A;
  	//输出值为：0
  	System.out.println("序数值：" + letter.ordinal());
  	letter = Letter.B;
  	//输出值为：1
  	System.out.println("序数值：" + letter.ordinal());
  }
  ```



#### 4.4 compareTo(Enum)

- compareTo(Enum) 方法用于比较相同类型的两个枚举常量的序数值，例如：

  ```java
  enum Letter {
  	A, B, C, D
  }
  
  public static void main(String[] args) {
  	Letter letter1 = Letter.A;
  	Letter letter2 = Letter.B;
  	Letter letter3 = Letter.C;
  	compare(letter1, letter2);
  	compare(letter1, letter3);
  	compare(letter2, letter3);
  	// 输出值为：
  	// A小于B
  	// A小于C
  	// B小于C
  }
  
  public static void compare(Letter letter1, Letter letter2) {
  	if (letter1.compareTo(letter2) > 0) {
  		System.out.println(letter1.name() + "大于" + letter2.name());
  	} else if (letter1.compareTo(letter2) < 0) {
  		System.out.println(letter1.name() + "小于" + letter2.name());
  	} else {
  		System.out.println(letter1.name() + "等于" + letter2.name());
  	}
  }
  ```



#### 5.5 equals(Enum)

- equals(Enum)用于比较两个对象的相等性，只有两个对象都引用同一个枚举中相同的常量时，返回值才为 true

  ```java
  enum Letter {
  	A, B, C, D
  }
  
  public static void main(String[] args) {
  	Letter letter1 = Letter.A;
  	Letter letter2 = Letter.B;
  	Letter letter3 = Letter.A;
  	//输出值：不相等
  	if (letter1.equals(letter2)) {
  		System.out.println("相等");
  	} else {
  		System.out.println("不相等");
  	}
  	//输出值：相等
  	if (letter1.equals(letter3)) {
  		System.out.println("相等");
  	} else {
  		System.out.println("不相等");
  	}
  }
  ```



### 05.枚举实现接口

- 枚举实现接口的案例如下所示

  ```java
  public interface Command {
  	void execute();
  }
  public enum Color implements Command {
  	RED, GREEN, BLUE;
  
  	@Override
  	public void execute() {
  		switch (this) {
  		case RED:
  			System.out.println("选中的是红色");
  			break;
  		case GREEN:
  			System.out.println("选中的是绿色");
  			break;
  		case BLUE:
  			System.out.println("选中的是蓝色");
  			break;
  		}
  	}
  }
  ```

- 枚举实现了Command接口，在不同枚举值下执行不同的行为

  ```java 
  public static void main(String[] args) {
  	select(Color.BLUE);
  	select(Color.RED);
  }
  
  public static void select(Color color){
  	color.execute();
  }
  ```

  - 运行结果如下

  ```java
  选中的是蓝色
  选中的是红色
  ```

- 而枚举Color也可以以另一种形式来实现Command接口，使用效果也完全相同

  ```java
  public enum Color implements Command {
  	
  	RED {
  		public void execute() {
  			System.out.println("选中的是红色");
  		}
  	},
  	GREEN {
  		public void execute() {
  			System.out.println("选中的是绿色");
  		}
  	},
  	BLUE {
  		public void execute() {
  			System.out.println("选中的是蓝色");
  		}
  	};
  }
  ```



## 类加载

### 01类加载器



#### 类加载器的概述

- 负责将.class文件加载到内存中，并为之生成对应的Class对象。那么有人会问.class文件是哪里来的，它是由javac编译器将java文件编译成.class文件的。

#### 类加载器的分类

![img](https://user-gold-cdn.xitu.io/2019/6/10/16b3fec35ad931fb?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

- Bootstrap ClassLoader 根类加载器(引导类加载器)
- Extension ClassLoader 扩展类加载器
- System ClassLoader    系统类加载器
- Application ClassLoader   应用程序类加载器

#### 类加载器的作用

-  Bootstrap ClassLoader 根类加载器

  - 也被称为引导类加载器，负责Java核心类的加载；比如System,String等。在JDK中JRE的lib目录下rt.jar文件中
  - 由C++语言实现（针对HotSpot）,负责将存放在<JAVA_HOME>\lib目录或-Xbootclasspath参数指定的路径中的类库加载到内存中，即负责加载Java的核心类。

  - Extension ClassLoader 扩展类加载器

    - 负责JRE的扩展目录中jar包的加载。在JDK中JRE的lib目录下ext目录

  - Sysetm ClassLoader 系统类加载器

    - 负责在JVM启动时加载来自java命令的class文件，以及classpath环境变量所指定的jar包和类路径

  - Application ClassLoader

    - 负责加载用户类路径（classpath）上的指定类库，我们可以直接使用这个类加载器，通过ClassLoader.getSystemClassLoader()方法直接获取。一般情况，如果我们没有自定义类加载器默认就是用这个加载器。

  - 自定义ClassLoader

    通常情况下，我们都是直接使用系统类加载器。但是，有的时候，我们也需要自定义类加载器。比如应用是通过网络来传输 Java类的字节码，为保证安全性，这些字节码经过了加密处理，这时系统类加载器就无法对其进行加载，这样则需要自定义类加载器来实现。自定义类加载器一般都是继承自`ClassLoader`类，从上面对`loadClass`方法来分析来看，我们只需要重写 findClass 方法即可。下面我们通过一个示例来演示自定义类加载器的流程：

    ```java
    package com.neo.classloader;
    import java.io.*;
    
    public class MyClassLoader extends ClassLoader {
        private String root;
    
        protected Class<?> findClass(String name) throws ClassNotFoundException {
            byte[] classData = loadClassData(name);
            if (classData == null) {
                throw new ClassNotFoundException();
            } else {
                return defineClass(name, classData, 0, classData.length);
            }
        }
    
        private byte[] loadClassData(String className) {
            String fileName = root + File.separatorChar
                    + className.replace('.', File.separatorChar) + ".class";
            try {
                InputStream ins = new FileInputStream(fileName);
                ByteArrayOutputStream baos = new ByteArrayOutputStream();
                int bufferSize = 1024;
                byte[] buffer = new byte[bufferSize];
                int length = 0;
                while ((length = ins.read(buffer)) != -1) {
                    baos.write(buffer, 0, length);
                }
                return baos.toByteArray();
            } catch (IOException e) {
                e.printStackTrace();
            }
            return null;
        }
    
        public String getRoot() {
            return root;
        }
    
        public void setRoot(String root) {
            this.root = root;
        }
    
        public static void main(String[] args)  {
    
            MyClassLoader classLoader = new MyClassLoader();
            classLoader.setRoot("E:\\temp");
    
            Class<?> testClass = null;
            try {
                testClass = classLoader.loadClass("com.neo.classloader.Test2");
                Object object = testClass.newInstance();
                System.out.println(object.getClass().getClassLoader());
            } catch (ClassNotFoundException e) {
                e.printStackTrace();
            } catch (InstantiationException e) {
                e.printStackTrace();
            } catch (IllegalAccessException e) {
                e.printStackTrace();
            }
        }
    }
    
    ```

    自定义类加载器的核心在于对字节码文件的获取，如果是加密的字节码则需要在该类中对文件进行解密。由于这里只是演示，我并未对class文件进行加密，因此没有解密的过程。这里有几点需要注意：

    - 1、这里传递的文件名需要是类的全限定性名称，即`com.paddx.test.classloading.Test`格式的，因为 defineClass 方法是按这种格式进行处理的。
    - 2、最好不要重写loadClass方法，因为这样容易破坏双亲委托模式。
    - 3、这类Test 类本身可以被 `AppClassLoader`类加载，因此我们不能把`com/paddx/test/classloading/Test.class`放在类路径下。否则，由于双亲委托机制的存在，会直接导致该类由`AppClassLoader`加载，而不会通过我们自定义类加载器来加载。

####类的加载定义

- 当程序要使用某个类时，如果该类还未被加载到内存中，则系统会通过加载，连接，初始化三步来实现对这个类进行初始化。
- 更加详细一点说，类的加载指的是将类的.class文件中的二进制数据读入到内存中，将其放在运行时数据区的方法区内，然后在堆区创建一个java.lang.Class对象，用来封装类在方法区内的数据结构。类的加载的最终产品是位于堆区中的Class对象，Class对象封装了类在方法区内的数据结构，并且向Java程序员提供了访问方法区内的数据结构的接口。
- 在Java语言里，类型的加载、连接和初始化过程都是在程序运行期间完成的，这种策略虽然会令类加载时稍微增加一些性能开销，但是会为Java应用程序提供高度的灵活性，Java里天生可以动态扩展的语言特性就是依赖运行期动态加载和动态连接这个特点来实现的。

###02类加载机制

####触发类加载条件

- ①.遇到new,getstatic,putstatic或invokestatic这4条字节码指令时，如果类没有进行过初始化，则需要先触发初始化。生成这4条指令的最常见的Java代码场景是：使用new关键字实例化对象的时候，读取或设置一个类的静态字段的时候（被final修饰，已在编译期把结果放入常量池的静态字段除外），以及调用一个类的静态方法的时候。
  - 调用一个类型的静态方法时（即在字节码中执行invokestatic指令）
  - 调用一个类型或接口的静态字段，或者对这些静态字段执行赋值操作时（即在字节码中，执行getstatic或者putstatic指令），不过用final修饰的静态字段除外，它被初始化为一个编译时常量表达式
- ②.使用java.lang.reflect包的方法对类进行反射调用的时候。
- ③.当初始化一个类的时候，发现其父类还没有进行过初始化，则需要先出发父类的初始化。
- ④.当虚拟机启动时，用户需要指定一个要执行的主类（包含main()方法的那个类），虚拟机会先初始化这个主类。
- ⑤.当使用JDK1.7的动态语言支持时，如果一个`java.lang.invoke.MethodHandle`实例最后的解析结果`REF_getStatic,REF_putStatic,REF_invokeStatic`的方法句柄，并且这个方法句柄所对应的类没有进行初始化，则需要先出发初始化。

### 03类的加载

类加载有三种方式：

- 1、命令行启动应用时候由JVM初始化加载
- 2、通过Class.forName()方法动态加载
- 3、通过ClassLoader.loadClass()方法动态加载

例子：

```java
package com.neo.classloader;
public class loaderTest { 
        public static void main(String[] args) throws ClassNotFoundException { 
                ClassLoader loader = HelloWorld.class.getClassLoader(); 
                System.out.println(loader); 
                //使用ClassLoader.loadClass()来加载类，不会执行初始化块 
                loader.loadClass("Test2"); 
                //使用Class.forName()来加载类，默认会执行初始化块 
                //Class.forName("Test2"); 
                //使用Class.forName()来加载类，并指定ClassLoader，初始化时不执行静态块 
                //Class.forName("Test2", false, loader); 
        } 
}


```

demo类

```java
public class Test2 { 
        static { 
                System.out.println("静态初始化块执行了！"); 
        } 
}


```

分别切换加载方式，会有不同的输出结果。

**Class.forName()和ClassLoader.loadClass()区别**

- `Class.forName()`：将类的.class文件加载到jvm中之外，还会对类进行解释，执行类中的static块；
- `ClassLoader.loadClass()`：只干一件事情，就是将.class文件加载到jvm中，不会执行static中的内容,只有在newInstance才会去执行static块。
- `Class.forName(name, initialize, loader)`带参函数也可控制是否加载static块。并且只有调用了newInstance()方法采用调用构造函数，创建类的对象 。




###04类的生命周期

![](http://upload-images.jianshu.io/upload_images/3985563-0108cc612a217322.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

其中类加载的过程包括了加载、验证、准备、解析、初始化五个阶段。在这五个阶段中，加载、验证、准备和初始化这四个阶段发生的顺序是确定的，而解析阶段则不一定，它在某些情况下可以在初始化阶段之后开始，这是为了支持Java语言的运行时绑定（也成为动态绑定或晚期绑定）。另外注意这里的几个阶段是按顺序开始，而不是按顺序进行或完成，因为这些阶段通常都是互相交叉地混合进行的，通常在一个阶段执行的过程中调用或激活另一个阶段。

####加载

查找并加载类的二进制数据加载时类加载过程的第一个阶段，在加载阶段，虚拟机需要完成以下三件事情：

- 通过一个类的全限定名来获取其定义的二进制字节流。
- 将这个字节流所代表的静态存储结构转化为方法区的运行时数据结构。
- 在Java堆中生成一个代表这个类的`java.lang.Class`对象，作为对方法区中这些数据的访问入口。

相对于类加载的其他阶段而言，加载阶段（准确地说，是加载阶段获取类的二进制字节流的动作）是可控性最强的阶段，因为开发人员既可以使用系统提供的类加载器来完成加载，也可以自定义自己的类加载器来完成加载。

加载阶段完成后，虚拟机外部的二进制字节流就按照虚拟机所需的格式存储在方法区之中，而且在Java堆中也创建一个`java.lang.Class`类的对象，这样便可以通过该对象访问方法区中的这些数据。

####连接

####**验证：确保被加载的类的正确性**

验证是连接阶段的第一步，这一阶段的目的是为了确保Class文件的字节流中包含的信息符合当前虚拟机的要求，并且不会危害虚拟机自身的安全。验证阶段大致会完成4个阶段的检验动作：

- **文件格式验证**：验证字节流是否符合Class文件格式的规范；例如：是否以`0xCAFEBABE`开头、主次版本号是否在当前虚拟机的处理范围之内、常量池中的常量是否有不被支持的类型。
- **元数据验证**：对字节码描述的信息进行语义分析（注意：对比javac编译阶段的语义分析），以保证其描述的信息符合Java语言规范的要求；例如：这个类是否有父类，除了`java.lang.Object`之外。
- **字节码验证**：通过数据流和控制流分析，确定程序语义是合法的、符合逻辑的。
- **符号引用验证**：确保解析动作能正确执行。

验证阶段是非常重要的，但不是必须的，它对程序运行期没有影响，如果所引用的类经过反复验证，那么可以考虑采用`-Xverifynone`参数来关闭大部分的类验证措施，以缩短虚拟机类加载的时间。

####**准备：为类的`静态变量分`配内存，并将其初始化为默认值**

准备阶段是正式为类变量分配内存并设置类变量初始值的阶段，这些内存都将在方法区中分配。对于该阶段有以下几点需要注意：

- 1、这时候进行内存分配的仅包括类变量（static），而不包括实例变量，实例变量会在对象实例化时随着对象一块分配在Java堆中。
- 2、这里所设置的初始值通常情况下是数据类型默认的零值（如0、0L、null、false等），而不是被在Java代码中被显式地赋予的值。

假设一个类变量的定义为：`public static int value = 3`；

那么变量value在准备阶段过后的初始值为0，而不是3，因为这时候尚未开始执行任何Java方法，而把value赋值为3的`public static`指令是在程序编译后，存放于类构造器`<clinit>（）`方法之中的，所以把value赋值为3的动作将在初始化阶段才会执行。

> 这里还需要注意如下几点：
>
> - 对基本数据类型来说，对于类变量（static）和全局变量，如果不显式地对其赋值而直接使用，则系统会为其赋予默认的零值，而对于局部变量来说，在使用前必须显式地为其赋值，否则编译时不通过。
> - 对于同时被static和final修饰的常量，必须在声明的时候就为其显式地赋值，否则编译时不通过；而只被final修饰的常量则既可以在声明时显式地为其赋值，也可以在类初始化时显式地为其赋值，总之，在使用前必须为其显式地赋值，系统不会为其赋予默认零值。
> - 对于引用数据类型reference来说，如数组引用、对象引用等，如果没有对其进行显式地赋值而直接使用，系统都会为其赋予默认的零值，即null。
> - 如果在数组初始化时没有对数组中的各元素赋值，那么其中的元素将根据对应的数据类型而被赋予默认的零值。

- 3、如果类字段的字段属性表中存在`ConstantValue`属性，即同时被final和static修饰，那么在准备阶段变量value就会被初始化为ConstValue属性所指定的值。

假设上面的类变量value被定义为： `public static final int value = 3`；

编译时Javac将会为value生成ConstantValue属性，在准备阶段虚拟机就会根据`ConstantValue`的设置将value赋值为3。我们可以理解为static final常量在编译期就将其结果放入了调用它的类的常量池中

####**解析：把类中的符号引用转换为直接引用**

解析阶段是虚拟机将常量池内的符号引用替换为直接引用的过程，解析动作主要针对类或接口、字段、类方法、接口方法、方法类型、方法句柄和调用点限定符7类符号引用进行。*符号引用*就是一组符号来描述目标，可以是任何字面量。

*直接引用*就是直接指向目标的指针、相对偏移量或一个间接定位到目标的句柄。

####**初始化**

初始化，为类的静态变量赋予正确的初始值，JVM负责对类进行初始化，主要对类变量进行初始化。在Java中对类变量进行初始值设定有两种方式：

- ①声明类变量是指定初始值
- ②使用静态代码块为类变量指定初始值

JVM初始化步骤

- 1、假如这个类还没有被加载和连接，则程序先加载并连接该类
- 2、假如该类的直接父类还没有被初始化，则先初始化其直接父类
- 3、假如类中有初始化语句，则系统依次执行这些初始化语句

类初始化时机：只有当对类的主动使用的时候才会导致类的初始化，类的主动使用包括以下六种：

- 创建类的实例，也就是new的方式
- 访问某个类或接口的静态变量，或者对该静态变量赋值
- 调用类的静态方法
- 反射（如`Class.forName(“com.shengsiyuan.Test”)`）
- 初始化某个类的子类，则其父类也会被初始化
- Java虚拟机启动时被标明为启动类的类（`Java Test`），直接使用`java.exe`命令来运行某个主类

####**结束生命周期**

在如下几种情况下，Java虚拟机将结束生命周期

- 执行了`System.exit()`方法
- 程序正常执行结束
- 程序在执行过程中遇到了异常或错误而异常终止
- 由于操作系统出现错误而导致Java虚拟机进程终止

### 05双亲委派模型

双亲委派模型的工作流程是：如果一个类加载器收到了类加载的请求，它首先不会自己去尝试加载这个类，而是把请求委托给父加载器去完成，依次向上，因此，所有的类加载请求最终都应该被传递到顶层的启动类加载器中，只有当父加载器在它的搜索范围中没有找到所需的类时，即无法完成该加载，子加载器才会尝试自己去加载该类。

双亲委派机制:

- 1、当`AppClassLoader`加载一个class时，它首先不会自己去尝试加载这个类，而是把类加载请求委派给父类加载器`ExtClassLoader`去完成。
- 2、当`ExtClassLoader`加载一个class时，它首先也不会自己去尝试加载这个类，而是把类加载请求委派给BootStrapClassLoader```去完成。
- 3、如果`BootStrapClassLoader`加载失败（例如在`$JAVA_HOME/jre/lib`里未查找到该class），会使用`ExtClassLoader`来尝试加载；
- 4、若ExtClassLoader也加载失败，则会使用`AppClassLoader`来加载，如果`AppClassLoader`也加载失败，则会报出异常`ClassNotFoundException`。

ClassLoader源码分析：

```java
public Class<?> loadClass(String name)throws ClassNotFoundException {
        return loadClass(name, false);
}

protected synchronized Class<?> loadClass(String name, boolean resolve)throws ClassNotFoundException {
        // 首先判断该类型是否已经被加载
        Class c = findLoadedClass(name);
        if (c == null) {
            //如果没有被加载，就委托给父类加载或者委派给启动类加载器加载
            try {
                if (parent != null) {
                     //如果存在父类加载器，就委派给父类加载器加载
                    c = parent.loadClass(name, false);
                } else {
                //如果不存在父类加载器，就检查是否是由启动类加载器加载的类，通过调用本地方法native Class findBootstrapClass(String name)
                    c = findBootstrapClass0(name);
                }
            } catch (ClassNotFoundException e) {
             // 如果父类加载器和启动类加载器都不能完成加载任务，才调用自身的加载功能
                c = findClass(name);
            }
        }
        if (resolve) {
            resolveClass(c);
        }
        return c;
    }


```

双亲委派模型意义：

- 系统类防止内存中出现多份同样的字节码
- 保证Java程序安全稳定运行




## 反射

### 01反射机制介绍

####Java反射机制原理

- 反射的原理是什么？
  - 反射是为了能够动态的加载一个类，动态的调用一个方法，动态的访问一个属性等动态要求而设计的。它的出发点就在于JVM会为每个类创建一个java.lang.Class类的实例，通过该对象可以获取这个类的信息，然后通过使用java.lang.reflect包下得API以达到各种动态需求。
  - 反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法和属性，这种动态获取的信息以及动态调用对象的方法的功能称为java语言的反射机制。

####Java反射机制的功能

- Java反射机制的功能有哪些？
  - 1.在运行时判断任意一个对象所属的类。
  - 2.在运行时构造任意一个类的对象。
  - 3.在运行时判断任意一个类所具有的成员变量和方法。
  - 4.在运行时调用任意一个对象的方法。
  - 5.生成动态代理。
- 反射的组成
  - 由于反射最终也必须有类参与，因此反射的组成一般有下面几个方面组成:
    - 1.java.lang.Class.java：类对象；
    - 2.java.lang.reflect.Constructor.java：类的构造器对象；
    - 3.java.lang.reflect.Method.java：类的方法对象；
    - 4.java.lang.reflect.Field.java：类的属性对象；
  - 反射中类的加载过程
    - 根据虚拟机的工作原理,一般情况下，类需要经过:加载->验证->准备->解析->初始化->使用->卸载这个过程，如果需要反射的类没有在内存中，那么首先会经过加载这个过程，并在在内存中生成一个class对象，有了这个class对象的引用，就可以发挥开发者的想象力，做自己想做的事情了

####Java反射的应用

- Java反射的应用
  - 1.逆向代码 ，例如反编译
  - 2.与注解相结合的框架 例如Retrofit
  - 3.单纯的反射机制应用框架 例如EventBus
  - 4.动态生成类框架 例如Gson
- 反射的作用有哪些
  - 前面只是说了反射是一种具有与Java类进行动态交互能力的一种机制，在Java和Android开发中，一般情况下下面几种场景会用到反射机制.
    - 需要访问隐藏属性或者调用方法改变程序原来的逻辑，这个在开发中很常见的，由于一些原因，系统并没有开放一些接口出来，这个时候利用反射是一个有效的解决方法
    - 自定义注解，注解就是在运行时利用反射机制来获取的。
    - 在开发中动态加载类，比如在Android中的动态加载解决65k问题等等，模块化和插件化都离不开反射，离开了反射寸步难行。
- 反射的用途
  - 官方解释：反射被广泛地用于那些需要在运行时检测或修改程序行为的程序中。这是一个相对高级的特性，只有那些语言基础非常扎实的开发者才应该使用它。如果能把这句警示时刻放在心里，那么反射机制就会成为一项强大的技术，可以让应用程序做一些几乎不可能做到的事情。

####.Class与.class文档

- ava 在真正需要某个类时才会加载对应的.class文档，而非在程序启动时就加载所有类，因为大部分时候我们只需要用到应用程序部分资源，有选择地加载可以节省系统资源
- java.lang.Class 的实例代表 Java 应用程序运行时加载的 .class 文档，类、接口、Enum等编译过后，都会生成 .class 文档，所以 Class可以用来包含类、接口、Enum等信息
- Class 类没有公开的构造函数，实例是由 JVM 自动产生，每个 .class 文档加载时， JVM 会自动生成对应的 Class 对象
  - 可以通过 Object 的 getClass() 方法或者通过 .class 常量取得每个对象对应的 Class 对象。如果是基本类型，可以使用对象的包装类加载 .TYPE 取得 Class 对象
  - 例如，使用 Integer.TYPE 可取得代表 int 基本类型的 Class，通过 Integer.class 取得代表 Integer.class 文档的 Class
  - 在取得 Class 对象后，就可以操作 Class 对象的公开方法取得类基本信息

```java
package com.yc.demo;
public class Student {
	public static void main(String[] args) {
		Class cl = Student.class;
		System.out.println("类名称:"+cl.getName());
		System.out.println("简单类名称:"+cl.getSimpleName());
		System.out.println("包名:"+cl.getPackage());
		System.out.println("是否为接口:"+cl.isInterface());
		System.out.println("是否为基本类型:"+cl.isPrimitive());
		System.out.println("是否为数组对象:"+cl.isArray());
		System.out.println("父类名称:"+cl.getSuperclass().getName());
	}
}
```

输出结果为

```java
类名称:com.yc.demo.Student
简单类名称:Student
包名:package com.yc.demo
是否为接口:false
是否为基本类型:false
是否为数组对象:false
父类名称:java.lang.Object
```

- Java 在真正需要类时才会加载.class文档，即在生成对象时才会加载.class文档。如果只是使用类声明了一个变量，此时并不会加载.class文档，而只是让编译程序检查对应的 .class 文档是否存在。[博客](https://github.com/yangchong211/YCBlogs)

  - 例如，在 Stduent 类中定义了 static 静态区域块，在首次加载 .class 文档时会被执行（这是默认情况下，也可以指定不执行）

  ```java
  public class Student {
  	static {
  		System.out.println("载入了 Student.class 文档");
  	}
  }
  ```

  - 再来测试加载顺序

  ```java
  package com.yc.demo;
  
  public class Main {
  	public static void main(String[] args) {
  		Student student;
  		System.out.println("声明了 Student 变量");
  		student=new Student();
  		System.out.println("生成了 Student 实例");
  	}
  }
  ```

  - 输出结果为

  ```java
  声明了 Student 变量
  载入了 Student.class 文档
  生成了 Student 实例
  ```

####反射之动态交互

反射是一种具有与类进行动态交互能力的一种机制，为什么要强调动态交互呢

- 动态加载，也就是在运行的时候才会加载，而不是在编译的时候，在需要的时候才进行加载获取，或者说你可以在任何时候加载一个不存在的类到内存中，然后进行各种交互,或者获取一个没有公开的类的所有信息，换句话说，开发者可以随时随意的利用反射的这种机制动态进行一些特殊的事情。

####使用反射的初衷

使用反射的初衷是什么

- 反射的初衷不是方便你去创建一个对象,而是让你在写代码的时候可以更加灵活,降低耦合,提高代码的自适应能力。

### 02反射查看类信息

####Java反射查看类信息

- 在取得 Class 对象后，就可以操作 Class 对象的公开方法取得类基本信息

  ```java
  private void method1() {
      Class<?> cl = Student.class;
      LogUtils.i("类名称:"+cl.getName());
      LogUtils.i("类名称:"+cl.getName());
      LogUtils.i("简单类名称:"+cl.getSimpleName());
      LogUtils.i("包名:"+cl.getPackage());
      LogUtils.i("是否为接口:"+cl.isInterface());
      LogUtils.i("是否为基本类型:"+cl.isPrimitive());
      LogUtils.i("是否为数组对象:"+cl.isArray());
      LogUtils.i("父类名称:"+cl.getSuperclass().getName());
  }
  ```

- 输出结果为

  ```java
  2019-06-11 15:56:59.490 2446-2446/com.ycbjie.other I/yc: 类名称:com.ycbjie.other.ui.activity.Student
  2019-06-11 15:56:59.490 2446-2446/com.ycbjie.other I/yc: 类名称:com.ycbjie.other.ui.activity.Student
  2019-06-11 15:56:59.490 2446-2446/com.ycbjie.other I/yc: 简单类名称:Student
  2019-06-11 15:56:59.490 2446-2446/com.ycbjie.other I/yc: 包名:package com.ycbjie.other.ui.activity
  2019-06-11 15:56:59.490 2446-2446/com.ycbjie.other I/yc: 是否为接口:false
  2019-06-11 15:56:59.490 2446-2446/com.ycbjie.other I/yc: 是否为基本类型:false
  2019-06-11 15:56:59.490 2446-2446/com.ycbjie.other I/yc: 是否为数组对象:false
  2019-06-11 15:56:59.490 2446-2446/com.ycbjie.other I/yc: 父类名称:java.lang.Object
  ```

####获得Class对象

- 每个类被加载之后，系统就会为该类生成一个对应的Class对象。通过该Class对象就可以访问到JVM中的这个类。

- 在Java程序中获得Class对象通常有如下三种方式：

  - 1.使用Class类的forName\(String clazzName\)静态方法。该方法需要传入字符串参数，该字符串参数的值是某个类的全限定名（必须添加完整包名）。
  - 2.调用某个类的class属性来获取该类对应的Class对象。
  - 3.调用某个对象的getClass\(\)方法。该方法是java.lang.Object类中的一个方法。

  ```java
  //第一种方式 通过Class类的静态方法——forName()来实现
  class1 = Class.forName("com.lvr.reflection.Person");
  //第二种方式 通过类的class属性
  class1 = Person.class;
  //第三种方式 通过对象getClass方法
  Person person = new Person();
  Class<?> class1 = person.getClass();
  ```


####  Class.forName()

- 1.通过JVM查找并加载指定的类(上面的代码指定加载了com.fanshe包中的Person类)

- 2.调用newInstance()方法让加载完的类在内存中创建对应的实例,并把实例赋值给p

  - 注意：如果找不到时，它会抛出 ClassNotFoundException 这个异常，这个很好理解，因为如果查找的类没有在 JVM 中加载的话，自然要告诉开发者。

  ```java
  Class<?> cls=Class.forName("com.yc.Person"); //forName(包名.类名)
  Person p= (Person) cls.newInstance();
  ```



#### 类.class

- 1.获取指定类型的Class对象,这里是Person

- 2.调用newInstance()方法在让Class对象在内存中创建对应的实例,并且让p引用实例的内存地址

  ```java
  Class<?> cls = Person.class;
  Person p=(Person)cls.newInstance();
  ```


#### 对象.getClass()

- 1.在内存中新建一个Person的实例,对象p对这个内存地址进行引用

- 2.对象p调用getClass()返回对象p所对应的Class对

- 3.调用newInstance()方法让Class对象在内存中创建对应的实例,并且让p2引用实例的内存地址

  ```java
  Person p = new Person();
  Class<?> cls= p.getClass();
  Person p2=(Person)cls.newInstance();
  ```

####获取Class父类对象

- 先看一下代码

  ```java
  //在AppBarLayout类中
  public static class Behavior extends AppBarLayout.BaseBehavior<AppBarLayout>
  //BaseBehavior的父类
  protected static class BaseBehavior<T extends AppBarLayout> extends HeaderBehavior<T>
  ```

- 反射获取父类

  ```java
  Class<?> superclass = AppBarLayout.Behavior.class.getSuperclass();
  ```

- 反射获取父类的父类

  ```java
  Class<?> superclass = AppBarLayout.Behavior.class.getSuperclass();
  headerBehaviorType = superclass.getSuperclass();
  ```

### 03获取对象信息

####获取class对象的信息

- 由于反射最终也必须有类参与，因此反射的组成一般有下面几个方面组成:

  - 1.java.lang.Class.java：类对象；
  - 2.java.lang.reflect.Constructor.java：类的构造器对象；
  - 3.java.lang.reflect.Method.java：类的方法对象；
  - 4.java.lang.reflect.Field.java：类的属性对象；

- 这个就比较多了……

  ```java
  boolean isPrimitive = class1.isPrimitive();//判断是否是基础类型
  boolean isArray = class1.isArray();//判断是否是集合类
  boolean isAnnotation = class1.isAnnotation();//判断是否是注解类
  boolean isInterface = class1.isInterface();//判断是否是接口类
  boolean isEnum = class1.isEnum();//判断是否是枚举类
  boolean isAnonymousClass = class1.isAnonymousClass();//判断是否是匿名内部类
  boolean isAnnotationPresent = class1.isAnnotationPresent(Deprecated.class);//判断是否被某个注解类修饰
  String className = class1.getName();//获取class名字 包含包名路径
  Package aPackage = class1.getPackage();//获取class的包信息
  String simpleName = class1.getSimpleName();//获取class类名
  int modifiers = class1.getModifiers();//获取class访问权限
  Class<?>[] declaredClasses = class1.getDeclaredClasses();//内部类
  Class<?> declaringClass = class1.getDeclaringClass();//外部类
  ```

- A:获取所有构造方法

  - public Constructor<?>[] getConstructors()
  - public Constructor<?>[] getDeclaredConstructors()    获取所有的构造方法

- B:获取单个构造方法

  - public Constructor<T> getConstructor(Class<?>... parameterTypes)
  - public Constructor<T> getDeclaredConstructor(Class<?>... parameterTypes)

- C：方法关键字 

  - getDeclareMethods() 	获取所有的方法
  - getReturnType() 	获取方法的返回值类型
  - getParameterTypes() 	获取方法的传入参数类型
  - getDeclareMethod("方法名,参数类型.class,....") 	获得特定的方法

- D：成员变量 

  - getDeclaredFields 	获取所有成员变量
  - getDeclaredField(参数类型.class,....) 	获取特定的成员变量

- E：父类和父接口 

  - getSuperclass() 	获取某类的父类
  - getInterfaces() 	获取某类实现的接口

####获取对象的变量

- 获取class对象的成员变量

  ```java
  Field[] allFields = class1.getDeclaredFields();//获取class对象的所有属性
  Field[] publicFields = class1.getFields();//获取class对象的public属性
  Field ageField = class1.getDeclaredField("age");//获取class指定属性
  Field desField = class1.getField("des");//获取class指定的public属性
  ```

- 实际案例代码

  ```java
  private void method4() {
      Student student = new Student();
      Class<? extends Student> cl = student.getClass();
  
      Field[] fields = cl.getFields();
      for (int i=0 ; i<fields.length ; i++){
          Field met = fields[i];
          String name = met.getName();
          Annotation[] declaredAnnotations = met.getDeclaredAnnotations();
          int modifiers = met.getModifiers();
          LogUtils.i("获取class对象的public属性:"+name+"----"+declaredAnnotations.length);
      }
  
      Field[] declaredFields = cl.getDeclaredFields();
      for (int i=0 ; i<declaredFields.length ; i++){
          Field met = declaredFields[i];
          String name = met.getName();
          Annotation[] declaredAnnotations = met.getDeclaredAnnotations();
          int modifiers = met.getModifiers();
          LogUtils.i("获取class对象的所有属性:"+name+"----"+declaredAnnotations.length);
      }
  }
  
  
  2019-06-11 16:22:01.109 5536-5536/com.ycbjie.other I/yc: 获取class对象的public属性:NAME----0
  2019-06-11 16:22:01.109 5536-5536/com.ycbjie.other I/yc: 获取class对象的所有属性:age----0
  2019-06-11 16:22:01.109 5536-5536/com.ycbjie.other I/yc: 获取class对象的所有属性:list----0
  2019-06-11 16:22:01.109 5536-5536/com.ycbjie.other I/yc: 获取class对象的所有属性:name----0
  2019-06-11 16:22:01.109 5536-5536/com.ycbjie.other I/yc: 获取class对象的所有属性:sex----0
  2019-06-11 16:22:01.109 5536-5536/com.ycbjie.other I/yc: 获取class对象的所有属性:NAME----0
  ```

- 获取Filed两个方法的区别

  - 两者的区别就是 
    - getDeclaredField() 获取的是 Class 中被 private 修饰的属性。 
    - getField() 方法获取的是非私有属性，并且 getField() 在当前 Class 获取不到时会向祖先类获取。

  ```java
  //获取所有的属性，但不包括从父类继承下来的属性
  public Field[] getDeclaredFields() throws SecurityException {}
  
  //获取自身的所有的 public 属性，包括从父类继承下来的。
  public Field[] getFields() throws SecurityException {}
  ```

####获取class对象的方法

- 获取class对象的方法

  ```java
  Method[] methods = class1.getDeclaredMethods();//获取class对象的所有声明方法
  Method[] allMethods = class1.getMethods();//获取class对象的所有public方法 包括父类的方法
  Method method = class1.getMethod("info", String.class);//返回次Class对象对应类的、带指定形参列表的public方法
  Method declaredMethod = class1.getDeclaredMethod("info", String.class);//返回次Class对象对应类的、带指定形参列表的方法
  ```

- 实际案例代码

  ```java
  private void method3() {
      Student student = new Student();
      Class<? extends Student> cl = student.getClass();
  
  
      //获取class对象的所有public方法 包括父类的方法
      Method[] methods = cl.getMethods();
      for (int i=0 ; i<methods.length ; i++){
          Method met = methods[i];
          String name = met.getName();
          Annotation[] declaredAnnotations = met.getDeclaredAnnotations();
          int modifiers = met.getModifiers();
          LogUtils.i("获取class对象的所有public方法，包括父类:"+name+"----"+declaredAnnotations.length);
      }
  
      //获取class对象的所有声明方法
      Method[] declaredMethods = cl.getDeclaredMethods();
      for (int i=0 ; i<declaredMethods.length ; i++){
          Method met = declaredMethods[i];
          String name = met.getName();
          Annotation[] declaredAnnotations = met.getDeclaredAnnotations();
          int modifiers = met.getModifiers();
          LogUtils.i("获取class对象的所有声明方法:"+name+"----"+declaredAnnotations.length);
      }
  }
  
  2019-06-11 16:07:15.751 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有public方法，包括父类:equals----0
  2019-06-11 16:07:15.752 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有public方法，包括父类:getAge----0
  2019-06-11 16:07:15.752 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有public方法，包括父类:getClass----0
  2019-06-11 16:07:15.752 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有public方法，包括父类:getName----0
  2019-06-11 16:07:15.752 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有public方法，包括父类:hashCode----0
  2019-06-11 16:07:15.752 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有public方法，包括父类:notify----0
  2019-06-11 16:07:15.752 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有public方法，包括父类:notifyAll----0
  2019-06-11 16:07:15.752 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有public方法，包括父类:setAge----0
  2019-06-11 16:07:15.752 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有public方法，包括父类:setName----0
  2019-06-11 16:07:15.752 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有public方法，包括父类:setStudentAge----0
  2019-06-11 16:07:15.752 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有public方法，包括父类:toString----0
  2019-06-11 16:07:15.752 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有public方法，包括父类:wait----0
  2019-06-11 16:07:15.752 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有public方法，包括父类:wait----0
  2019-06-11 16:07:15.752 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有public方法，包括父类:wait----0
  2019-06-11 16:07:15.752 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有声明方法:getStudent----0
  2019-06-11 16:07:15.752 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有声明方法:setList----0
  2019-06-11 16:07:15.752 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有声明方法:getAge----0
  2019-06-11 16:07:15.752 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有声明方法:getName----0
  2019-06-11 16:07:15.752 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有声明方法:setAge----0
  2019-06-11 16:07:15.752 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有声明方法:setName----0
  2019-06-11 16:07:15.752 3857-3857/com.ycbjie.other I/yc: 获取class对象的所有声明方法:setStudentAge----0
  ```

####获取class对象的构造函数

- 获取class对象的构造函数

  ```java
  Constructor<?>[] allConstructors = class1.getDeclaredConstructors();//获取class对象的所有声明构造函数
  Constructor<?>[] publicConstructors = class1.getConstructors();//获取class对象public构造函数
  Constructor<?> constructor = class1.getDeclaredConstructor(String.class);//获取指定声明构造函数
  Constructor publicConstructor = class1.getConstructor(String.class);//获取指定声明的public构造函数
  ```

- 实际案例代码

  ```java
  private void method2() {
      try {
          Class<?> cl = Class.forName("com.ycbjie.other.ui.activity.Student");
          //获取class对象public构造函数
          Constructor<?>[] constructors = cl.getConstructors();
          for (int i=0 ; i<constructors.length ; i++){
              Constructor con = constructors[i];
              String name = con.getName();
              TypeVariable[] typeParameters = con.getTypeParameters();
              Annotation[] declaredAnnotations = con.getDeclaredAnnotations();
              LogUtils.i("获取class对象public构造函数:"+name+"----"+typeParameters.length);
          }
          //获取class对象的所有声明构造函数
          Constructor<?>[] declaredConstructors = cl.getDeclaredConstructors();
          for (int i=0 ; i<declaredConstructors.length ; i++){
              LogUtils.i("获取class对象的所有声明构造函数:"+declaredConstructors[i].getName());
          }
      } catch (ClassNotFoundException e) {
          e.printStackTrace();
      }
  }
  ```

####获取方法属性

- 其他方法

  ```java
  Annotation[] annotations = (Annotation[]) class1.getAnnotations();//获取class对象的所有注解
  Annotation annotation = (Annotation) class1.getAnnotation(Deprecated.class);//获取class对象指定注解
  Type genericSuperclass = class1.getGenericSuperclass();//获取class对象的直接超类的 Type
  Type[] interfaceTypes = class1.getGenericInterfaces();//获取class对象的所有接口的type集合
  ```

####获取对象信息案例

- Class对象代表加载的.class文档，取得Class对象后，就可以取得.class文档中记载的信息，如包、构造函数、数据成员、方法成员等

- 每一种信息都对有对应的类型，如包对应的类型是 java.lang.Package，构造函数对应的类型是 java.lang.reflect.Constructor

- 例如，先来为Student类增添多种类型的不同信息

  ```java
  public final class Student {
  	
  	enum Gender{
  		male,female
  	}
  	
  	private String name;
  	
  	public int age;
  	
  	protected Gender gender;
  	
  	public Student(String name,int age){
  		
  	}
  	
  	public Student(String name,int age,Gender gender){
  		
  	}
  	
  	private Student(){
  		
  	}
  	
  	public String getName() {
  		return name;
  	}
  	
  	private int getAge(){
  		return age;
  	}
  	
  	protected Gender getGender(){
  		return gender;
  	}
  }
  ```

  - 再来获取各种信息

  ```java
  public class Main {
  
  	public static void main(String[] args) {
  		try {
  			Class cl = Class.forName("com.czy.demo.Student");
  			
  			// 取得包对象
  			Package p = cl.getPackage();
  			System.out.println("包名:" + p.getName());
  			// 访问修饰符
  			int modifier = cl.getModifiers();
  			System.out.println("类访问修饰符：" + Modifier.toString(modifier));
  
  			System.out.println();
  			
  			//取得构造函数信息
  			Constructor[] constructors=cl.getConstructors();
  			for(Constructor constructor:constructors){
  				System.out.print("访问修饰符：" + Modifier.toString(constructor.getModifiers()));
  				System.out.print("   构造函数名："+constructor.getName());
  				System.out.println();
  			}
  			
  			System.out.println();
  			
  			//取得声明的数据成员
  			Field[] fields = cl.getDeclaredFields();
  			for (Field field : fields) {
  				System.out.print("访问修饰符：" + Modifier.toString(field.getModifiers()));
  				System.out.print("   类型："+field.getType().getName());
  				System.out.print("   成员名："+field.getName());
  				System.out.println();
  			}
  			
  			System.out.println();
  			
  			//取得成员方法息
  			Method[] methods=cl.getDeclaredMethods();
  			for(Method method:methods){
  				System.out.print("访问修饰符：" + Modifier.toString(method.getModifiers()));
  				System.out.print("   返回值类型："+method.getReturnType().getName());
  				System.out.print("   方法名："+method.getName());
  				System.out.println();
  			}
  		} catch (ClassNotFoundException e) {
  			e.printStackTrace();
  		}
  	}
  }
  ```

  - 运行结果

  ```java
  包名:com.yc.demo
  类访问修饰符：public final
  
  访问修饰符：public   构造函数名：com.czy.demo.Student
  访问修饰符：public   构造函数名：com.czy.demo.Student
  
  访问修饰符：private   类型：java.lang.String   成员名：name
  访问修饰符：public   类型：int   成员名：age
  访问修饰符：protected   类型：com.czy.demo.Student$Gender   成员名：gender
  
  访问修饰符：public   返回值类型：java.lang.String   方法名：getName
  访问修饰符：private   返回值类型：int   方法名：getAge
  访问修饰符：protected   返回值类型：com.czy.demo.Student$Gender   方法名：getGender
  ```

### 04反射的实际使用

####反射生成类实例对象

- **生成类的实例对象**

  - 1.使用Class对象的newInstance\(\)方法来创建该Class对象对应类的实例。这种方式要求该Class对象的对应类有默认构造器，而执行newInstance\(\)方法时实际上是利用默认构造器来创建该类的实例。
  - 2.先使用Class对象获取指定的Constructor对象，再调用Constructor对象的newInstance\(\)方法来创建该Class对象对应类的实例。通过这种方式可以选择使用指定的构造器来创建实例。

  ```java
  //第一种方式 Class对象调用newInstance()方法生成
  Object obj = class1.newInstance();
  //第二种方式 对象获得对应的Constructor对象，再通过该Constructor对象的newInstance()方法生成
  Constructor<?> constructor = class1.getDeclaredConstructor(String.class);//获取指定声明构造函数
  obj = constructor.newInstance("hello");
  ```

- new对象和反射得到对象的区别

  - 在使用反射的时候，必须确保这个类已经加载并已经连接了。使用new的时候，这个类可以没有被加载，也可以已经被加载。
  - new关键字可以调用任何public构造方法，而反射只能调用无参构造方法。
  - new关键字是强类型的，效率相对较高。 反射是弱类型的，效率低。
  - 反射提供了一种更加灵活的方式创建对象，得到对象的信息。如Spring 中AOP等的使用，动态代理的使用，都是基于反射的。解耦。

####反射调用类的方法

- **调用类的方法**

  - 1.通过Class对象的getMethods\(\)方法或者getMethod\(\)方法获得指定方法，返回Method数组或对象。
  - 2.调用Method对象中的`Object invoke(Object obj, Object... args)`方法。第一个参数对应调用该方法的实例对象，第二个参数对应该方法的参数。

  ```java
  private void method8() {
      try {
          Class<?> cl = Class.forName("com.ycbjie.other.ui.activity.Student");
          // 生成新的对象：用newInstance()方法
          Student obj = (Student) cl.newInstance();
          String student1 = obj.getStudent();
          LogUtils.i("反射调用类的方法1:"+student1);
          //首先需要获得与该方法对应的Method对象
          Method method = cl.getDeclaredMethod("setAge", int.class);
          //设置权限
          method.setAccessible(true);
          //调用指定的函数并传递参数
          method.invoke(obj, 28);
          String student2 = obj.getStudent();
          LogUtils.i("反射调用类的方法2:"+student2);
      } catch (ClassNotFoundException e) {
          e.printStackTrace();
      } catch (IllegalAccessException e) {
          e.printStackTrace();
      } catch (InstantiationException e) {
          e.printStackTrace();
      } catch (InvocationTargetException e) {
          e.printStackTrace();
      } catch (NoSuchMethodException e) {
          e.printStackTrace();
      }
  }
  
  //打印值
  2019-06-11 18:24:40.146 23666-23666/com.ycbjie.other I/yc: 反射调用类的方法1:yc---26
  2019-06-11 18:24:40.146 23666-23666/com.ycbjie.other I/yc: 反射调用类的方法2:yc---28
  ```

- 获取方法的参数

- **当通过Method的invoke\(\)方法来调用对应的方法时，Java会要求程序必须有调用该方法的权限。如果程序确实需要调用某个对象的private方法，则可以先调用Method对象的如下方法。**  

- **setAccessible\(boolean flag\)：将Method对象的acessible设置为指定的布尔值。值为true，指示该Method在使用时应该取消Java语言的访问权限检查；值为false，则知识该Method在使用时要实施Java语言的访问权限检查。**

####反射访问成员变量值

- 反射访问成员变量值

  - 1.通过Class对象的getFields\(\)方法或者getField\(\)方法获得指定方法，返回Field数组或对象。
  - 2.Field提供了两组方法来读取或设置成员变量的值：  
    - getXXX\(Object obj\):获取obj对象的该成员变量的值。此处的XXX对应8种基本类型。如果该成员变量的类型是引用类型，则取消get后面的XXX。  
    - setXXX\(Object obj,XXX val\)：将obj对象的该成员变量设置成val值。

  ```java
  private void method9() {
      try {
          Class<?> cl = Class.forName("com.ycbjie.other.ui.activity.Student");
          // 生成新的对象：用newInstance()方法
          Student obj = (Student) cl.newInstance();
          int age = obj.getAge();
          LogUtils.i("反射访问成员变量值1:"+age);
          //获取age成员变量
          //Field field = cl.getField("age");
          Field field = cl.getDeclaredField("age");
          //设置权限
          field.setAccessible(true);
          //将obj对象的age的值设置为10
          field.setInt(obj, 10);
          //获取obj对象的age的值
          int anInt = field.getInt(obj);
          LogUtils.i("反射访问成员变量值2:"+anInt);
  
          //反射修改私有变量
          // 获取声明的 code 字段，这里要注意 getField 和 getDeclaredField 的区别
          Field gradeField = cl.getDeclaredField("name");
          // 如果是 private 或者 package 权限的，一定要赋予其访问权限
          gradeField.setAccessible(true);
          // 修改 student 对象中的 Grade 字段值
          gradeField.set(obj, "逗比");
          Object o = gradeField.get(obj);
          LogUtils.i("反射访问成员变量值3:"+o.toString());
      } catch (ClassNotFoundException e) {
          e.printStackTrace();
      } catch (IllegalAccessException e) {
          e.printStackTrace();
      } catch (InstantiationException e) {
          e.printStackTrace();
      } catch (NoSuchFieldException e) {
          e.printStackTrace();
      }
  }
  
  
  
  2019-06-11 19:06:59.380 12313-12313/com.ycbjie.other I/yc: 反射访问成员变量值1:26
  2019-06-11 19:06:59.380 12313-12313/com.ycbjie.other I/yc: 反射访问成员变量值2:10
  2019-06-11 19:06:59.380 12313-12313/com.ycbjie.other I/yc: 反射访问成员变量值3:逗比
  ```

####访问私有权限说明

- 设置暴力访问权限为.setAccessible(true);

  一般情况下，我们并不能对类的私有字段进行操作，利用反射也不例外，但有的时候，例如要序列化的时候，我们又必须有能力去处理这些字段，这时候，我们就需要调用AccessibleObject上的setAccessible()方法来允许这种访问，而由于反射类中的Field，Method和Constructor继承自AccessibleObject，因此，通过在这些类上调用setAccessible()方法，我们可以实现对这些字段的操作。

  ```java
  Field gradeField = clazz.getDeclaredField("code");
  // 如果是 private 或者 package 权限的，一定要赋予其访问权限
  gradeField.setAccessible(true);
  
  Method goMethod = clazz.getDeclaredMethod("getMethod");
  // 赋予访问权限
  goMethod.setAccessible(true);
  ```

  ### nvoke()方法执行

  - Method 调用 invoke() 的时候，存在许多细节：
    - invoke() 方法中第一个参数 Object 实质上是 Method 所依附的 Class 对应的类的实例，如果这个方法是一个静态方法，那么 ojb 为 null，后面的可变参数 Object 对应的自然就是参数。
    - **invoke() 返回的对象是 Object，所以实际上执行的时候要进行强制转换。**
    - 在对Method调用invoke()的时候，如果方法本身会抛出异常，那么这个异常就会经过包装，由Method统一抛InvocationTargetException。而通过InvocationTargetException.getCause() 可以获取真正的异常。

  

###05利用Class建立对象

####情景分析

- 例如，你需要来控制学生、老师或者家长的唱歌行为，可是学生、老师和家长这些类又是由其他人来设计的，你只是对开始与暂停操作进行控制。那么该如何做呢？

####建立实例对象

- 如果已有确切的类，那么就可以使用new关键字建立实例。如果不知道类名称，那么可以利用Class.forName()动态加载.class文档，取得Class对象之后，利用其newInstance()方法建立实例

  ```java
  Class cl = Class.forName("ClassName");
  Object object = cl.newInstance();
  ```

- 这种事先不知道类名称，又需要建立类实例的需求，一般情况下都是由于开发者需要得到某个类对象并对其行为进行操纵，可是该类又是由他人开发且还未完工，因此就需要来动态加载.class文档

- 针对情景1的分析与操作步骤

  - 你可以规定学生类必须实现Sing接口

    ```java
    public interface Sing {
    	void start();
    }
    ```

  - 那么，就可以来进行自己的开发了，将动态加载的对象强转为Sing

    ```java
    public class Main {
    	public static void main(String[] args) {
    		try {
    			Sing palyer = (Sing) Class.forName("className").newInstance();
    			palyer.start();
    		} catch (Exception e) {
    			e.printStackTrace();
    		}
    		
    	}
    }
    ```

  - 然后规定他人设计的学生类必须实现Sing接口

    ```java
    public class Student implements Sing {
    
    	@Override
    	public void start() {
    		System.out.println("学生唱歌");
    	}
    }
    ```

  - 这样，等到得到确切的类名称后，修改main方法的className即可

    ```java
    public static void main(String[] args) {
    	try {
    		Sing palyer = (Sing) Class.forName("com.czy.demo.Student").newInstance();
    		palyer.start();
    	} catch (Exception e) {
    		e.printStackTrace();
    	}
    	
    }
    ```

###06操作成员方法

####指定一个student类

- 修改Student类，将get方法都指定为公有的，将set方法指定为私有的

  ```java
  public class Student {
  
  	private String name;
  
  	private int age;
  
  	public Student() {
  
  	}
  
  	public Student(String name, int age) {
  		this.name = name;
  		this.age = age;
  	}
  
  	public String getName() {
  		System.out.println("调用了getName方法，Name：" + name);
  		return name;
  	}
  
  	public int getAge() {
  		System.out.println("调用了getAge方法，Age：" + age);
  		return age;
  	}
  
  	private void setName(String name) {
  		this.name = name;
  		System.out.println("调用了setName方法,name:" + name);
  	}
  
  	private void setAge(int age) {
  		this.age = age;
  		System.out.println("调用了setAge方法，age:" + age);
  	}
  }
  ```

####反射调用公有方法

- java.lang.reflect.Method 实例是方法的代表对象，可以使用 invoke() 方法来动态调用指定的方法

- 首先来调用公有方法

  ```java
  public class Main {
  
  	public static void main(String[] args) throws Exception {
  		Class cl = Class.forName("com.czy.demo.Student");
  		// 指定构造函数
  		Constructor constructor = cl.getConstructor(String.class, Integer.TYPE);
  		// 根据指定的构造函数来获取对象
  		Object object = constructor.newInstance("杨充逗比", 25);
  
  		// 指定方法名称来获取对应的公开的Method实例
  		Method getName = cl.getMethod("getName");
  		// 调用对象object的方法
  		getName.invoke(object);
  
  		// 指定方法名称来获取对应的公开的Method实例
  		Method getAge = cl.getMethod("getAge");
  		// 调用对象object的方法
  		getAge.invoke(object);
  
  	}
  }
  ```

- 输出结果如下所示，可以知道Student对象的两个get方法成功被调用了。

  ```java
  调用了getName方法，Name：杨充逗比
  调用了getAge方法，Age：25
  ```

####反射调用私有方法

- 一般情况下，类的私有方法只有在其内部才可以被调用，通过反射我们可以来突破这一限制

- 受保护或私有方法的调用步骤略有不同

  ```java
  public class Main {
  	public static void main(String[] args) throws Exception {
  		Class cl = Class.forName("com.czy.demo.Student");
  		// 指定构造函数
  		Constructor constructor = cl.getConstructor(String.class, Integer.TYPE);
  		// 根据指定的构造函数来获取对象
  		Object object = constructor.newInstance("杨充逗比", 25);
  
  		// 指定方法名称来获取对应的私有的Method实例
  		Method setName = cl.getDeclaredMethod("setName", String.class);
  		setName.setAccessible(true);
  		setName.invoke(object, "潇湘剑雨");
  		
  		// 指定方法名称来获取对应的私有的Method实例
  		Method setAge = cl.getDeclaredMethod("setAge", Integer.TYPE);
  		setAge.setAccessible(true);
  		setAge.invoke(object, 100);
  	}
  }
  ```

- 输出结果如下所示，可以看到私有方法一样在外部被调用了

  ```java
  调用了setName方法,name:潇湘剑雨
  调用了setAge方法，age:100
  ```

### 07泛型和反射

####泛型和Class类

- 从JDK 1.5 后，Java中引入泛型机制，Class类也增加了泛型功能，从而允许使用泛型来限制Class类，例如：String.class的类型实际上是Class&lt;String&gt;。如果Class对应的类暂时未知，则使用Class&lt;?&gt;\(?是通配符\)。通过反射中使用泛型，可以避免使用反射生成的对象需要强制类型转换。

泛型的好处众多，最主要的一点就是避免类型转换，防止出现ClassCastException，即类型转换异常。以下面程序为例：

```java
public class ObjectFactory {
    public static Object getInstance(String name){
        try {
            //创建指定类对应的Class对象
            Class cls = Class.forName(name);
            //返回使用该Class对象创建的实例
            return cls.newInstance();
        } catch (ClassNotFoundException | InstantiationException | IllegalAccessException e) {
            e.printStackTrace();
            return null;
        }
    }
}
```

- 上面程序是个工厂类，通过指定的字符串创建Class对象并创建一个类的实例对象返回。但是这个对象的类型是Object对象，取出实例后需要强制类型转换。如下例：

```java
Date date = (Date) ObjectFactory.getInstance("java.util.Date");
```

- 或者如下：

```java
String string = (String) ObjectFactory.getInstance("java.util.Date");
```

- 上面代码在编译时不会有任何问题，但是运行时将抛出ClassCastException异常，因为程序试图将一个Date对象转换成String对象。

但是泛型的出现后，就可以避免这种情况。

```java
public class ObjectFactory {
    public static <T> T getInstance(Class<T> cls) {
        try {
            // 返回使用该Class对象创建的实例
            return cls.newInstance();
        } catch (InstantiationException | IllegalAccessException e) {
            e.printStackTrace();
            return null;
        }
    }

}
```

- 在上面程序的getInstance\(\)方法中传入一个Class&lt;T&gt;参数，这是一个泛型化的Class对象，调用该Class对象的newInstance\(\)方法将返回一个T对象。

```java
String instance = ObjectFactory.getInstance(String.class);
```

- 通过传入`String.class`便知道T代表String，所以返回的对象是String类型的，避免强制类型转换。当然Class类引入泛型的好处不止这一点，在以后的实际应用中会更加能体会到。

####使用反射来获取泛型信息

- 通过指定类对应的 Class 对象，可以获得该类里包含的所有 Field，不管该 Field 是使用 private 修饰，还是使用 public 修饰。

- 获得了 Field 对象后，就可以很容易地获得该 Field 的数据类型，即使用如下代码即可获得指定 Field 的类型。

  ```java
  // 获取 Field 对象 f 的类型
  Class<?> a = f.getType();
  ```

- 但这种方式只对普通类型的 Field 有效。如果该 Field 的类型是有泛型限制的类型，如 Map&lt;String, Integer&gt; 类型，则不能准确地得到该 Field 的泛型参数。

  - 为了获得指定 Field 的泛型类型，应先使用如下方法来获取指定 Field 的类型。

  ```java
  // 获得 Field 实例的泛型类型
  Type type = f.getGenericType();
  ```

- 然后将 Type 对象强制类型转换为 ParameterizedType 对象，ParameterizedType 代表被参数化的类型，也就是增加了泛型限制的类型。ParameterizedType 类提供了如下两个方法。

  - **getRawType\(\)：**返回没有泛型信息的原始类型。
  - **getActualTypeArguments\(\)：**返回泛型参数的类型。

- 下面是一个获取泛型类型的完整程序。

  ```java
  public class GenericTest{
      private Map<String , Integer> score;
      public static void main(String[] args)
          throws Exception{
          Class<GenericTest> clazz = GenericTest.class;
          Field f = clazz.getDeclaredField("score");
          // 直接使用getType()取出Field类型只对普通类型的Field有效
          Class<?> a = f.getType();
          // 下面将看到仅输出java.util.Map
          System.out.println("score的类型是:" + a);
          // 获得Field实例f的泛型类型
          Type gType = f.getGenericType();
          // 如果gType类型是ParameterizedType对象
          if(gType instanceof ParameterizedType){
              // 强制类型转换
              ParameterizedType pType = (ParameterizedType)gType;
              // 获取原始类型
              Type rType = pType.getRawType();
              System.out.println("原始类型是：" + rType);
              // 取得泛型类型的泛型参数
              Type[] tArgs = pType.getActualTypeArguments();
              System.out.println("泛型类型是:");
              for (int i = 0; i < tArgs.length; i++) 
              {
                  System.out.println("第" + i + "个泛型类型是：" + tArgs[i]);
              }
          } else{
              System.out.println("获取泛型类型出错！");
          }
      }
  }
  ```

  - 输出结果：

    > score 的类型是: interface java.util.Map  
    > 原始类型是: interface java.util.Map  
    > 泛型类型是:  
    > 第 0 个泛型类型是: class java.lang.String  
    > 第 1 个泛型类型是：class java.lang.Integer

- 从上面的运行结果可以看出，直接使用Field的getType\(\)方法只能获取普通类型的Field的数据类型：对于增加了泛型参数的类型的 Field，应该使用 getGenericType\(\) 方法来取得其类型。

- Type 也是 java.lang.reflect 包下的一个接口，该接口代表所有类型的公共高级接口，Class 是 Type 接口的实现类。Type 包括原始类型、参数化类型、数组类型、类型变量和基本类型等。

getType和getGenericType有何区别？

- 获得了 Field 对象后，就可以很容易地获得该 Field 的数据类型，即使用如下代码即可获得指定 Field 的类型。

  ```java
  // 获取 Field 对象 f 的类型
  Class<?> a = f.getType();
  ```

- 但这种方式只对普通类型的 Field 有效。如果该 Field 的类型是有泛型限制的类型，如 Map&lt;String, Integer&gt; 类型，则不能准确地得到该 Field 的泛型参数。

  - 为了获得指定 Field 的泛型类型，应先使用如下方法来获取指定 Field 的类型。

  ```java
  // 获得 Field 实例的泛型类型
  Type type = f.getGenericType();
  ```

- 然后将 Type 对象强制类型转换为 ParameterizedType 对象，ParameterizedType 代表被参数化的类型，也就是增加了泛型限制的类型。ParameterizedType 类提供了如下两个方法。

  - **getRawType\(\)：**返回没有泛型信息的原始类型。
  - **getActualTypeArguments\(\)：**返回泛型参数的类型。

####泛型和反射案例

- 通过反射获得泛型的实际类型参数

  - 把泛型变量当成方法的参数，利用Method类的getGenericParameterTypes方法来获取泛型的实际类型参数
  - 例子：

  ```java
  public class GenericTest {
  
      public static void main(String[] args) throws Exception {
          getParamType();
      }
      
       /*利用反射获取方法参数的实际参数类型*/
      public static void getParamType() throws NoSuchMethodException{
          Method method = GenericTest.class.getMethod("applyMap",Map.class);
          //获取方法的泛型参数的类型
          Type[] types = method.getGenericParameterTypes();
          System.out.println(types[0]);
          //参数化的类型
          ParameterizedType pType  = (ParameterizedType)types[0];
          //原始类型
          System.out.println(pType.getRawType());
          //实际类型参数
          System.out.println(pType.getActualTypeArguments()[0]);
          System.out.println(pType.getActualTypeArguments()[1]);
      }
  
      /*供测试参数类型的方法*/
      public static void applyMap(Map<Integer,String> map){
  
      }
  
  
      public static void applyMap(ArrayList<? extends Student> list){
      	  
      }
  }
  ```

- 输出结果：

  ```java
  java.util.Map<java.lang.Integer, java.lang.String>
  interface java.util.Map
  class java.lang.Integer
  class java.lang.String
  ```

- 注意问题

  - applyMap(ArrayList<? extends Student> list)该泛型方法，无法使用反射获取参数类型

### 08反射攻击单例

#### 如何防止反射序列化攻击单例

- 枚举单例

  ```java
  public enum Singleton {
      INSTANCE {
          @Override
          protected void read() {
              System.out.println("read");
          }
          @Override
          protected void write() {
              System.out.println("write");
          }
      };
      protected abstract void read();
      protected abstract void write();
  }
  ```

- class文件：

  ```java
  public abstract class Singleton extends Enum{
      private Singleton(String s, int i){
          super(s, i);
      }
  
      protected abstract void read();
      protected abstract void write();
      public static Singleton[] values(){
          Singleton asingleton[];
          int i;
          Singleton asingleton1[];
          System.arraycopy(asingleton = ENUM$VALUES, 0, asingleton1 = new Singleton[i = asingleton.length], 0, i);
          return asingleton1;
      }
  
      public static Singleton valueOf(String s) {
          return (Singleton)Enum.valueOf(singleton/Singleton, s);
      }
  
      Singleton(String s, int i, Singleton singleton){
          this(s, i);
      }
  
      public static final Singleton INSTANCE;
      private static final Singleton ENUM$VALUES[];
  
      static {
          INSTANCE = new Singleton("INSTANCE", 0){
  
              protected void read(){
                  System.out.println("read");
              }
  
              protected void write(){
                  System.out.println("write");
              }
  
          };
          ENUM$VALUES = (new Singleton[] {
              INSTANCE
          });
      }
  }
  ```

- 类的修饰abstract，所以没法实例化，反射也无能为力。关于线程安全的保证，其实是通过类加载机制来保证的，我们看看INSTANCE的实例化时机，是在static块中，JVM加载类的过程显然是线程安全的。对于防止反序列化生成新实例的问题还不是很明白，一般的方法我们会在该类中添加上如下方法，不过枚举中也没有显示的写明该方法。

  ```java
  //readResolve to prevent another instance of Singleton
  private Object readResolve(){
      return INSTANCE;
  }
  ```



## 多线程

多线程入门篇：https://juejin.im/post/6844903919160655880#heading-4

​                              http://concurrent.redspider.group/article/01/2.html

## IO流

​           思维导图：   https://mm.edrawsoft.cn/template/946

## java并发

​            思维导图：   https://mm.edrawsoft.cn/wx.html?work_id=7805













































 