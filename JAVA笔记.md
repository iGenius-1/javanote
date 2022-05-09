# JAVA-从入门到没毛病

本文档记录学习到的Java新知识，对于以及在c++中学过的知识不再赘述

## 一些快捷键

- 选中代码 按 CTRL+ALT+T 可以快速的将代码块放入循环或其他语句下
- ax想要快速的写出arr数组的for循环可以 arr.fori 回车
- 直接右键->generate 可快速创建有参或者无参构造器 或setter和getter
- 按alt+enter可以快捷修改文件名为public类名，也可以快捷改写方法
- 选中某变量按CTRL+alt+v可快速创建一个新的量来接受该值
- shift+F6可以同步更改变量名
- 按住alt+鼠标左键可以进行整列的编辑



## 一些很牛的代码技巧

```Java
//当遇到想要给中文排序怎么办？
// 自定义排序规则
List<String> sizes = new ArrayList<>();
Collections.addAll(sizes, "一","二","三","四","五","陆","柒","八","九","十","十一");

Collections.sort(data, new Comparator<String>() {
    @Override
    public int compare(String o1, String o2) {
        // o1   八.,....
        // o2   柒.,....
        return sizes.indexOf(o1.substring(0, o1.indexOf(".")))
                - sizes.indexOf(o2.substring(0, o2.indexOf(".")));
    }
});
```





## JAVA的类型转换问题

### 自动类型转换

```
java中默认整数型用int接收，而浮点型用double接收。
```

java中以下代码会报错而c++中可正常执行

```java
char ch='a';
char ch1='a'+1;//java会报错，因为这属于是用范围更小的类型接受范围大的类型
```

- **类型范围小**的变量，可以**直接赋值**给**类型范围大**的变量。

- 在表达式中，小范围类型的变量会自动转换成当前较大范围的类型再运算。

- 表达式的最终结果类型由表达式中的最高类型决定。 

- 在表达式中，byte、short、char 是直接转换成int类型参与运算的。（避免了运算后越界的问题）

  ![image-20220304173324453](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220304173324453.png)

### 强制类型转换

- 类型范围大的数据或者变量，不能直接**赋值**给**类型范围小**的变量，会报错。

- 可以强行将类型范围大的变量、数据赋值给类型范围小的变量。

```java
int a = 20;
byte b = (byte)a;
```

- 强制类型转换**可能**造成数据(丢失)溢出；

- 浮点型强转成整型，直接丢掉小数部分，保留整数部分返回。



## 运算符

### “+”作连接符

- “+”符号与字符串运算的时候是用作连接符的，其结果依然是一个字符串。

<img src="C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220304175754025.png" alt="image-20220304175754025"  />

- **独门秘籍：**能算则算，不能算就在一起。（计算机很聪明）

  

### 逻辑运算符

- 逻辑与 &：有一个为false、结果是false。前面一个为false后面的依然执行

- 短路与 &&： 一个为false、结果是false。前一个为false,后一个条件不执行了

- 逻辑或 |：有一个为true、结果是true。前面一个为true后面的依然执行

- 短路或 ||：一个为true、结果是true。前一个为true，后一个条件不执行了



### 三元运算符

**格式：**条件表达式 **?** 值1 **:** 值2;

```java
int a,b;
a=10;b=20;
int c = a>b? a:b;
```



### 运算符的优先级

![image-20220304195714082](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220304195714082.png)



## 分支和循环

### switch 语句注意事项

- 表达式类型只能是byte、short、int、char，JDK5开始支持枚举，JDK7开始支持String、不支持double、float（计算精度低）、long（范围太大没必要）。
- 如果代码执行到没有写break的case块，执行完后将直接进入下一个case块执行代码（而且不会进行任何匹配），直到遇到break才跳出分支，这就是switch的**穿透性**



## 数组

```Java
//数组定义：
//1.静态初始化
int[] num{0,1,2};
String[] s{"aaa","bbb"};
//也可以写成和c一样的格式,但感觉我看到的都是上面这种格式
int num[]={0,1,2};
//2.动态初始化
int[] arr=new int[3];
string[] s=new string[5];
double[] d=new double[6];
int arr[]=new int[3];
```

- java中数组是没有length()方法的，只有length属性，数组array.length返回的是该数组的长度。

- 字符串String是有length()方法的，str.length()返回的是该字符串的长度。

数组中的未赋值的内存有默认值，局部变量则没有默认值

![image-20220306153409864](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220306153409864.png)

## 方法

Java中的方法和C语言中的函数很类似，格式有些不同，且Java方法参数不支持默认值

![image-20220306165509096](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220306165509096.png)

- 方法没有被调用的时候，在**方法区**中的字节码文件中存放

- 方法被调用的时候，需要进入到**栈内存**中运行

  ### Java中没有指针

- **JAVA**中传递参数时的**引用**和C语言中的不是一个东西，没有取地址&符号的使用

- java中方法参数分为**基本参数类型和引用参数类型**，除了基本参数类型其他全是引用参数类型，引用的意义可参考c++

![img](https://img-blog.csdn.net/20180607221353561)



### 方法的重载

方法的重载与C语言中函数的重载一样。



## 类

Java中的类和c++中的类很相似，区别在于Java没有指针，Java的this指针的使用的是“."操作。Java也省去了拷贝构造函数

- 类名首字母建议大写，且有意义，满足“驼峰模式”。

- 一个Java文件中可以定义多个class类，但只能一个类是public修饰，而且public修饰的类名必须成为代码文件名（按alt+enter可以快捷修改文件名为public类名）。实际开发中建议还是一个文件定义一个class类。

  ![image-20220306205443372](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220306205443372.png)

![image-20220306205527457](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220306205527457.png)





### JAVA对象内存图

- c++中有拷贝构造函数，可以将一个对象的属性全部赋给另一个对象，但这两个对象是不同的，所指向的内存不是同一块；c++也可以使用重载之后的“=”符号实现将一个对象的属性全部赋给另一个对象，但两者依然是不同的对象。

- 与此不同的是，Java中的对象可以直接通过“=”符号创建，创建出来的新对象与旧对象指向同一块内存，即**两者是同一个对象**。Java没有拷贝构造函数

  

![image-20220306212625585](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220306212625585.png)

### 成员变量与局部变量的区别

成员变量有**初始值**而局部变量没有

![image-20220307195113402](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220307195113402.png)



## String

- java.lang.String 类代表字符串，String类定义的变量可以用于指向字符串对象，然后操作该字符串。

- Java 程序中的所有字符串文字（例如“abc”）都为此类的对象。

- String其实常被称为**不可变字符串类型**，它的对象在创建后不能被更改。（如果要更改，每次更改都会返回一个新的对象）

  

  ### string创建对象

![image-20220307205426272](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220307205426272.png)

- 以“”方式给出的字符串对象，在**字符串常量池**中存储，而且相同内容只会在其中存储一份。
- 通过构造器new对象，每new一次都会产生一个新对象，放在堆内存中。（**只要不是通过“”给出的字符串就会放到堆内存中**）

可以直接把数组里的内容拼接为字符串输出

![image-20220307210825974](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220307210825974.png)

### string常用API

#### equals

- JAVA中只有基本数据类型可用“==”号判断内容是否相同；String等引用类型的变量不能使用“==”直接判断是否相等，因为引用类型的值在栈区存储的是指针，用“==”将会比较这两个**地址**是否相等
- JAVA中无法用**[]**去访问字符串中某个位置的字符，要用特定的api。数组中仍然可用[]

![image-20220307213213524](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220307213213524.png)

![image-20220310160853751](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220310160853751.png)



## ArrayList（集合）

创建对象：**ArrayList list = new ArrayList();**

在不使用**泛型**时，可以往集合中添加任意类型的元素，但这样并不好；

*用System.Out.Println(某集合)，会打印该集合所有的元素值；虽然集合的名称对应的也是栈区的一个指针，但集合内部会实现找到对应数据的功能。

![image-20220310165712263](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220310165712263.png)

### ArrayLIst泛型(统一集合中的元素类型)

- ArrayList<String> ：此集合只能操作字符串类型的元素。 

- ArrayList<Integer>：此集合只能操作整数类型的元素。

  ### 常用API

  ![image-20220310171631592](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220310171631592.png)



# 面向对象进阶

## static

### **static修饰的成员变量**

- 静态成员变量（有static修饰，**属于类**、加载一次，可以被共享访问）

- 访问格式：	**类名.静态成员变量(推荐)**
  	对象.静态成员变量(不推荐)

- **static修饰的成员变量**在内存中是被单独存放的，所有类对象**共享**，是属于类的

![image-20220311222801635](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220311222801635.png)

### **static修饰的成员方法**

静态成员方法（有static修饰，**属于类**和对象共享）

访问格式： **类名.静态成员方法**
                    对象.静态成员方法（不推荐）

![image-20220311223459616](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220311223459616.png)

由于static修饰的成员方法是所有对象共享的，且可以直接通过类访问，所以适合用来写一些通用的方法，比如定义一个**工具类方法**来生成验证码。

如果一个类中只有工具类方法，建议把**构造器私有**，以避免用户创建对象，浪费内存。



### static访问注意实现：

- **静态方法只能访问静态的成员，不可以直接访问实例成员。静态方法只能调用静态方法**

- 实例方法可以访问静态的成员，也可以访问实例成员。

- 静态方法中是不可以出现this关键字的。 

  其实中心思想就是，**static 修饰的成员变量或方法是共享的，是属于类的，不需要创建对象即可访问**，所以static修饰的方法不可以访问成员变量，因为当访问static修饰的成员方法时，不存在与之对应的对象，也就没有对应的成员变量可供访问（成员变量需要定义类的对象后才有意义）。从内存的角度会更好理解.



### 代码块

- 代码块是类的5大成分之一（成员变量、构造器，方法，**代码块**，内部类），定义在类中方法外。
- 在Java类下，使用 { } 括起来的代码被称为代码块 。

![image-20220311224843841](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220311224843841.png)



### static应用

**单例设计模式**：一个类永远只能拥有一个对象

#### 饿汉单例模式：

**在要用前就创建好了对象**

![image-20220311225337164](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220311225337164.png)

#### 懒汉单例模式：

**提供一个静态方法，通过该方法得到一个对象**

![image-20220311225602506](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220311225602506.png)





## 继承

Java中提供一个**关键字extends**，用这个关键字，我们可以让一个类和另一个类建立起父子关系。当子类继承父类后，就可以直接使用父类公共的属性和方法了。因此，用好这个技术可以很好的我们提高代码的复用性.

- 子类们相同特征（共性属性，共性方法）放在父类中定义。
- 子类独有的的属性和行为应该定义在子类自己里面。

**格式：public class Student extends People {}**



**父类与子类在内存上的关系：**我的理解是**子类将父类所有内容都包括在自己的空间中了**，但由于权限，父类的私有内容无法访问，且父类中的static修饰的内容依然是公用的，独立的。

![image-20220311230046460](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220311230046460.png)



### 继承的特点

1. 子类可以继承父类的属性和行为，但是***子类不能继承父类的构造器***。
2. Java是单继承模式：**一个类只能继承一个直接父类**。（避免继承的方法或变量重复）
3. Java不支持多继承、但是**支持多层继承**。
4. Java中所有的类都是**Object类**的子类。
5. java中子类**可以继承父类的私有属性，但不能直接使用**，使用方法后面会讲？
6. 严格来讲，子类并不能继承父类的static修饰的变量或方法，因为**static**修饰的属性是共有的，独立的。更倾向于叫共享该属性而不是继承。



**继承后访问成员有就近原则，如果强行要访问父类成员，可使用super**

![image-20220311231747778](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220311231747778.png)





### 方法重写

在继承体系中，子类出现了和父类中一模一样的方法声明，我们就称子类这个方法是重写的方法。当子类需要父类的功能，但父类的该功能不完全满足自己的需求时，子类可以重写父类中的方法。

- 重载： 发生在同一个类中，方法名必须相同，参数类型不同、个数不同、顺序不同，方法返回值和访问修饰符可以不同，发生在编译时。
-  重写： 发生在父子类中，方法名、参数列表必须相同，返回值范围小于等于父类，抛出的异常范围小于等于父类，访问修饰符范围大于等于父类；如果父类方法访问修饰符为private则子类就不能重写该方法。

![image-20220311232036543](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220311232036543.png)



### 子类构造器的特点

- 子类在初始化的时候，有可能会使用到父类中的数据，如果父类没有完成初始化，子类将无法使用父类的数据。
- **子类初始化之前，一定要调用父类构造器先完成父类数据空间的初始化。**
- 子类中所有的构造器默认都会先访问父类中无参的构造器，再执行自己。子**类构造器的第一行语句默认都是：super()**，不写也存在。

1. **如果父类中没有无参数构造器，只有有参构造器，会出现什么现象呢？**
   会报错。因为子类默认是调用父类无参构造器的。
2. **如何解决？**
   子类构造器中可以通过书写 super(…)，手动调用父类的有参数构造器



### this和super

当子类没有定义方法时，this对象会寻找父类中的方法

![image-20220311232710693](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220311232710693.png)

#### this调用本类其他构造器

用于重载有参构造器的调用，示例如下

```Java
//在学员信息登记系统中，后台创建对象封装数据的时候如果用户没有输入学校，则默认使用“黑马培训中心”。
//如果用户输入了学校则使用用户输入的学校信息。
public class Student {          
    private String schoolName;  
    private String name;
    public Student(String name){
          this(name , “黑马培训中心”);	
    }	
     
    public Student(String name , String schoolName ){
          this.name = name;        
          this.schoolName = schoolName;
    }	
}

```

**this(...)和super(…)使用注意点：**

1. 子类通过 this (...）去调用本类的其他构造器，本类其他构造器会通过 super 去手动调用父类的构造器，最终还是会调用父类构造器的。
2. 注意：this(…) super(…) 都只能放在构造器的第一行，所以**二者不能共存在同一个构造器中**。



## 包-package

一般项目从顶到下的顺序是 project->module->package->class

- **建包语句**必须在第一行，一般IDEA工具会帮助创建

- **相同包下的类可以直接访问，不同包下的类必须导包,才可以使用**！导包格式：import 包名.类名;（直接写需要用的类名，idea会提供快捷导包的方法）

- 假如一个类中需要用到不同类，而这个两个类的名称是一样的，那么默认只能导入一个类，另一个类要**带包名访问**。

  格式是：**包名.类名  对象名=new 包名.类名();**

![image-20220312170711067](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220312170711067.png)



## 权限修饰符

![image-20220312171732758](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220312171732758.png)



## final修饰符

**final的作用**

- final 关键字是最终的意思，可以修饰（方法，变量，类）
- 修饰方法：表明该方法是最终方法，不能被重写。
- 修饰变量：表示该变量第一次赋值后，不能再次被赋值(有且仅能被赋值一次)。
- 修饰类：表明该类是最终类，不能被继承。



**final修饰变量的注意**

- final修饰的变量是基本类型：那么变量存储的数据值不能发生改变。
- final修饰的变量是引用类型：那么变量存储的地址值不能发生改变，但是地址指向的对象内容是可以发生变化的。

![image-20220312200931402](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220312200931402.png)



## 常量

常量是使用了**public static final**修饰的成员变量，必须有初始化值，而且执行的过程中其值不能被改变。

例如 public static final String s="italent"; 

常量的作用和C语言中类似



## 枚举

枚举是一种特殊类型

Java中的枚举和C语言中的不一样，**Java中的枚举不可以给枚举对象赋初值，枚举的作用就只是作信息的标志和分类**，通常配合switch语句使用。

<img src="C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220312205901297.png" alt="image-20220312205901297"  />

枚举在switch 语句中的使用和在其他地方的使用格式不同，这里并没有细讲，用到了再说。



## 抽象类-abstract

拥有**抽象方法**的类是**抽象类**，抽象类的子类必须重载抽象方法，这也是抽象类的意义所在：给出子类必须要拥有的方法并且由子类自己去完成该方法（因为每个子类对该方法的要求可能不同，但每个子类又都需要该方法）

- 在Java中**abstract**是抽象的意思，如果一个类中的某个方法的具体实现不能确定，就可以申明成abstract修饰的抽象方法（不能写方法体了），这个类必须用abstract修饰，被称为抽象类。

```Java
//格式：
public abstract class Animal{
	public abstract void run();
}

```

1. **抽象类的作用是什么样的？**

   可以被子类继承、**充当模板的**、同时也可以提高代码复用。

2. **抽象方法是什么样的？**

   只有方法签名，没有方法体，使用了abstract修饰。

3. **继承抽象类有哪些要注意？**

   一个类如果继承了抽象类，那么这个类必须重写完抽象类的全部抽象方法。否则这个类也必须定义成抽象类。

   

***抽象类不能创建对象，因为抽象类中有抽象方法，抽象方法是未完成的方法，而且从本质上来说，抽象类的本义就是用来被继承的，是“模板”的基础.**

***不能用abstract修饰变量、代码块、构造器。**



![image-20220312213851160](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220312213851160.png)

### 模板方法模式

- 把功能定义成一个所谓的模板方法，放在**抽象类中**，模板方法中**只定义通用且能确定的代码**。
- 模板方法中不能决定的功能定义成抽象方法让具体子类去实现。



1. 简言之就是把**通用的方法在模板中实现**，需要子类自己实现的方法定义为抽象方法，这就叫模板
2. 模板方法要用final修饰，避免子类重写





## 接口-interface

**JDK8 之前**的接口可以看成一个**完全抽象的类**，接口中只有抽象方法和常量；

之后的版本又为接口新增了几个功能，如default或static修饰的方法，类似于普通的成员方法，可以被实现类直接调用。

```java
//接口用关键字interface来定义
public interface 接口名 {
       // 常量
       // 抽象方法
} 

```

- 接口不能实例化。
- JDK8之前接口中只能是抽象方法和常量，没有其他成分了。
- 接口中的成员都是public 修饰的，写不写都是，因为规范的目的是为了公开化。



### 接口的用法

- 接口是用来被类实现（**implements**）的，实现接口的类称为**实现类**。实现类可以理解成所谓的子类。
- 接口可以被类单实现，也可以被类多实现。如果多实现的接口具有同名的方法也无所谓，因为这些方法最终都是要在实现类中重写；**但如果不同接口中的同名方法的返回值不同，在一个实现类中实现这些接口则会报错。**
- 一个类实现接口，必须重写完全部接口的全部抽象方法，否则这个类需要定义成抽象类。

```
实现类的格式：
修饰符 class 实现类 implements 接口1, 接口2, 接口3 , ... {
}
实现的关键字：implements
```



### 接口和接口的多继承

- 类和类的关系：单继承。
- 类和接口的关系：多实现。
- 接口和接口的关系：多继承，一个接口可以同时继承多个接口。
- **接口多继承的作用**：规范合并，整合多个接口为同一个接口，便于子类实现。



### JDK8新增接口功能

JDK8版本开始后，Java只对接口的成员方法进行了新增，**允许接口中直接定义带有方法体的方法**，以便于接口的更新。



​     **JDK8开始后新增了那些方法?**

1. 默认方法：default修饰，实现类对象调用。
2. 静态方法：static修饰，必须用当前接口名调用
3. 私有方法：private修饰，jdk9开始才有的，只能在接口内部被调用。他们都会默认被public修饰。



- 如果使用default，static或者private修饰必须要写方法体，且**默认是public修饰**。
- 除去这三种修饰符修饰的方法，其他方法都是**默认public abstract 修饰**的，不要有**方法体**。



### 接口的注意事项

1. **接口不能创建对象**

2. 一个类实现多个接口，多个接口中有同样的静态方法（static）不冲突。因为静态方法只能用接口名调用，不能用实现类调用。

3. 一个类继承了父类，同时又实现了接口，父类中和接口中有同名方法，默认用父类的。

   同时继承父类和实现接口的类的格式应该是 ：extends父类 implements 接口

4. 一个类实现了多个接口，多个接口中存在同名的默认方法（default），不冲突，这个类**重写该方法**即可。

5. 一个接口继承多个接口，是没有问题的，如果多个接口中存在规范冲突则不能多继承。（例如返回值不同）





## 多态

不同的类继承同一个父类，例如 class A,class B extends A，class C extends A；B,C同属于A的子类，而B、C中的功能并不一样。在开发中如果代码中写了有关B的一系列功能，需要再写关于C的相同功能的话就会产生重复类似的代码，而利用多态就可以解决这个问题。但**多态不能使用子类的独有功能**，要强制类型转换，将父类转为子类才可以使用子类的独有功能。

```Java
多态的常见形式：
父类类型 对象名称 = new 子类构造器;
接口     对象名称 = new 实现类构造器;	
```

​	**多态中成员访问特点：**

- 方法调用：编译看左边，运行看右边。

- 变量调用：编译看左边，运行也看左边。（多态侧重行为多态）

  **多态的前提：**

- **有继承/实现关系**；有父类引用指向子类对象；有方法重写。



![image-20220314150833884](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220314150833884.png)



![image-20220314150941040](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220314150941040.png)





## 内部类

内部类就是定义在一个类里面的类，里面的类可以理解成（寄生），外部类可以理解成（宿主）。当一个事物的内部，还有一个部分需要一个完整的结构进行描述，而这个内部的完整的结构又只为外部事物提供服务，那么整个内部的完整结构可以选择使用内部类来设计。内部类提供了更好的封装性，内部类本身就可以用private protectecd等修饰，封装性可以做更多控制。外部类只能用public修饰。

```Java
//外部类
public class People{
	// 内部类
	public class Heart{
	}
}
```

### 静态内部类

- 有static修饰，**属于外部类本身。**
- 它的特点和使用与普通类是完全一样的，类有的成分它都有，只是位置在别人里面而已。

```Java
public class Outer{
        // 静态成员内部类
        public static class Inner{
        }
}
//静态内部类创建对象的格式： 
格式：外部类名.内部类名 对象名 = new 外部类名.内部类构造器;
范例：Outer.Inner in =  new Outer.Inner();
```

![image-20220314183701489](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220314183701489.png)

**我认为static修饰的内部类相当于把一个独立的类（内部类）放在了另一个类中（外部类），而其实这两个类并没有什么联系。**



### 成员内部类

- 无static修饰，**属于外部类的对象。**
- JDK16之前，成员内部类中不能定义静态成员，JDK 16开始也可以定义静态成员了。

```Java
public class Outer {
	// 成员内部类
	public class Inner {
    }
}
成员内部类创建对象的格式：    
格式：外部类名.内部类名 对象名 = new  外部类构造器.new 内部类构造器();
范例：Outer.Inner in =  new Outer().new  Inner();
```

![image-20220314184855357](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220314184855357.png)

```Java
//**注意：在成员内部类中访问所在外部类对象 ，格式：外部类名.this
    public String name;
    public  class inner{
        void print()
        {
            System.out.println(outer.this.name);
        }
    }
}
```



### 局部内部类

- 局部内部类放在方法、代码块、构造器等执行体中。
- 局部内部类的类文件名为： 外部类$N内部类.class。



### 匿名内部类-重点

- 本质上是一个没有名字的局部内部类，定义在方法中、代码块中、等。
- 作用：**方便创建子类对象**，最终目的为了简化代码编写。

```Java
//格式：匿名内部类可用于创建 普通类，抽象类或者接口的子类对象
new 类|抽象类名|或者接口名() {
		重写方法;
};
//例子
Animal a = new Animal() {
	public void run() {
	}
};
//接口是不能创建实例的，匿名内部类相当于直接创建一个接口的实现类的对象
a. run();
test(a);
```

- 匿名内部类是一个没有名字的内部类。

- 匿名内部类写出来就会产生一个匿名内部类的对象。

- 匿名内部类的对象类型相当于是当前new的那个的类型的**子类类型**。

- 开发中不是我们主动去定义匿名内部类的，而是别人需要我们写或者我们可以写的时候才会使用。匿名内部类的代码可以实现代码进一步的简化

- 匿名内部类可以作为方法的实际参数进行传输。（就是直接把匿名内部类当函数参数，而不用先用参数接受匿名内部类的对象）

  ```java
  //例如上面的代码中的test(a)可以写成
  test(new Animal() {
  	public void run() {
  	}
  })
  ```

**匿名内部类常用于comparator()接口的快速实现**，注意在比较浮点型数值大小时要用Double.compare(),因为函数的返回值是int类型

![image-20220322111423168](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220322111423168.png)



## 常用API

**API(Application Programming interface)  应用程序编程接口。**



### Object类

- Object类的方法是**一切子类对象都可以直接使用的**，所以我们要学习Object类的方法。
- 一个类要么默认继承了Object类，要么间接继承了Object类，Object类是Java中的祖宗类。
- **Object类可以接收所有引用类型**，要使用子类的特有功能时再强制类型转化为子类即可

![image-20220315091809226](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220315091809226.png)

- 父类toString()方法存在的意义就是**为了被子类重写**，以便返回对象的内容信息，而不是地址信息！！

- equals的作用也是**让子类重写**，以便比较2个子类对象的内容是否相同。
- Java自带的API有的会重写toString() 和 equals() 



### Objects

Objects是一个工具类，提供了一些方法去完成一些功能。调用时直接 **Objects.方法名** ；因为Objects定义的方法都是静态方法，用类名直接调用，且其构造函数是私有的，不能创建对象。

![image-20220315092629326](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220315092629326.png)

官方在进行字符串比较时，没有用字符串对象的的equals方法，而是选择了Objects的equals方法来比较。使用Objects的equals方法在进行对象的比较会更安全。

```Java
public static boolean equals(Object a, Object b) {
	return (a == b) || (a != null && a.equals(b));
}
//先判空，再用String的equals()方法来比较
```



### StringBuilder

- StringBuilder是一个可变的字符串类，我们可以把它看成是一个对象容器。
- 作用：提高字符串的操作效率，如拼接、修改等。

![image-20220315093558343](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220315093558343.png)

![image-20220315093629062](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220315093629062.png)

![image-20220315093706650](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220315093706650.png)

String是不可变字符串类型，意思是为String在栈区开辟的空间里存的内容：实体在堆区的地址是不可变的；每次拼接其实在底层还是调用了StringBulider，每次拼接都要换一次地址（在栈区重新开辟），所以效率低。

![image-20220315094509887](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220315094509887.png)

- String ：内容是不可变的、拼接字符串性能差。
- StringBuilder：内容是可变的、拼接字符串性能好、代码优雅。
- 定义字符串使用String
- 拼接、修改等操作字符串使用StringBuilder



### Math类

- 包含执行基本数字运算的方法，Math类没有提供公开的构造器。
- 如何使用类中的成员呢？看类的成员是否都是静态的，如果是，通过类名就可以直接调用

![image-20220315094658565](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220315094658565.png)



### System类

- System也是一个工具类，代表了当前系统，提供了一些与系统相关的方法。

![image-20220315094748093](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220315094748093.png)



### BigDecimal

用于解决浮点型运算精度失真的问题

```Java
//使用步骤
//创建对象BigDecimal封装浮点型数据（最好的方式是调用方法）
public static BigDecimal valueOf(double val):   包装浮点数成为BigDecimal对象。
//BigDecimal对象获取
BigDecimal b1 = BigDecimal.valueOf(0.1);
```

![image-20220315094926134](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220315094926134.png)



### 日期与时间

#### Date类

**Date类代表当前所在系统的日期时间信息。**

![image-20220316143639166](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220316143639166.png)

![image-20220316143737720](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220316143737720.png)

***Date类还有 before()和after()方法用来判断时间的先后顺序。**



#### SimpleDateFormat 类

**可以去完成日期时间的格式化操作**

![image-20220316144125807](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220316144125807.png)![image-20220316144857898](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220316144857898.png)

```java
//指定格式的例子
SimpleDateFormat s=new SimpleDateFormat("yyyy年mm月dd日 hh：mm：ss");
Date d=s.format(time);  //d就是被格式化后的Date对象
String t="2022年03月16日 14：50：00";
Date d1=s.parse(t);//d1就是将字符串解析后的Date对象
```



#### Calendar

- Calendar代表了系统此刻日期对应的日历对象。
- Calendar是一个抽象类，**不能直接创建对象**。（Calendar创建对象的方式与之前讲的**单例模式**是一样的）

![image-20220316152331118](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220316152331118.png)

```java
Calendar c=Calendar.getInstance();
```

![image-20220316152406651](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220316152406651.png)

```java
什么是字段？
Calendar c=Calendar.getInstance();
System.out.println(c);
输出：java.util.GregorianCalendar[time=1647415570638,areFieldsSet=true,areAllFieldsSet=true,lenient=true,zone=sun.util.calendar.ZoneInfo[id="GMT+08:00",offset=28800000,dstSavings=0,useDaylight=false,transitions=0,lastRule=null],firstDayOfWeek=1,minimalDaysInFirstWeek=1,ERA=1,YEAR=2022,MONTH=2,WEEK_OF_YEAR=12,WEEK_OF_MONTH=3,DAY_OF_MONTH=16,DAY_OF_YEAR=75,DAY_OF_WEEK=4,DAY_OF_WEEK_IN_MONTH=3,AM_PM=1,HOUR=3,HOUR_OF_DAY=15,MINUTE=26,SECOND=10,MILLISECOND=638,ZONE_OFFSET=28800000,DST_OFFSET=0]
//以上这些关于当前Calendar对象有关时间的详细参数就是字段
```



### JDK8新增日期API

方法真的有很多，大概知道就行，真的用到了再具体去查



#### LocalDate、LocalTime、LocalDateTime

- 他们 分别表示日期，时间，日期时间对象，他们的类的实例是**不可变的对象**（如果改变了，则返回一个新的对象，原对象不变）。
- 他们三者构建对象和API都是通用的



#### Instant时间戳

- JDK8获取时间戳特别简单，且功能更丰富。Instant类由一个静态的工厂方法now()可以返回当前时间戳。

- 时间戳是包含日期和时间的，与java.util.Date很类似，事实上Instant就是类似JDK8 以前的Date。
- Instant和Date这两个类可以进行转换。



####  DateTimeFormatter

- 在JDK8中，引入了一个全新的日期与时间格式器DateTimeFormatter。
- 正反都能调用format方法。



#### Period

- 在Java8中，我们可以使用以下类来计算**日期间隔差异**：java.time.Period
- 主要是 Period 类方法 getYears()，getMonths() 和 getDays() 来计算,只能精确到年月日。
- 用于 LocalDate 之间的比较。



#### Duration

- 在Java8中，我们可以使用以下类来计算**时间间隔差异**：java.time.Duration
- 提供了使用基于时间的值测量时间量的方法。
- 用于 LocalDateTime 之间的比较。也可用于 Instant 之间的比较。



#### ChronoUnit

ChronoUnit类可用于在单个时间单位内测量一段时间，这个工具类是最全的了，可以用于比较所有的时间单位



## 包装类

其实就是8种基本数据类型对应的引用类型。java为了让所有的数据类型都是引用类型，符合面向对象的标准，引入了包装类；

- java为了实现一切皆对象，为8种基本类型提供了对应的引用类型。
- 后面的集合和泛型其实也只能支持包装类型，不支持基本数据类型。

![image-20220318142006685](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220318142006685.png)

**自动装箱：**基本类型的数据和变量可以直接赋值给包装类型的变量。

**自动拆箱：**包装类型的变量可以直接赋值给基本数据类型的变量。

![image-20220318142323026](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220318142323026.png)



## 正则表达式

![image-20220318142505969](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220318142505969.png)

![image-20220318142607255](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220318142607255.png)



### 正则表达式支持爬取信息

```Java
String rs = "来黑马程序学习Java,电话020-43422424，或者联系邮箱" +
			"itcast@itcast.cn,电话18762832633，0203232323" +
			"邮箱bozai@itcast.cn，400-100-3233 ，4001003232";
	// 需求：从上面的内容中爬取出 电话号码和邮箱。
	// 1.定义爬取规则
	String regex = "(\\w{1,}@\\w{2,10}(\\.\\w{2,10}){1,2})|" +
					"(1[3-9]\\d{9})|(0\\d{2,5}-?\\d{5,15})|400-?\\d{3,8}-?\\d{3,8}";
	// 2.编译正则表达式成为一个匹配规则对象
	Pattern pattern = Pattern.compile(regex);
	// 3.通过匹配规则对象得到一个匹配数据内容的匹配器对象
	Matcher matcher = pattern.matcher(rs);
	// 4.通过匹配器去内容中爬取出信息
	while(matcher.find()){
		System.out.println(matcher.group());
	}
//万物皆对象，匹配规则也是对象（pattern），匹配器也是对象（matcher），集体的方法待用到时看API
```





## Arrays类

数组操作工具类，专门用于操作数组元素的。

![image-20220318143955053](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220318143955053.png)

![image-20220318144321644](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220318144321644.png)



## Lambda表达式

- Lambda表达式是JDK 8开始后的一种新语法形式。
- **作用：简化匿名内部类的代码写法。**
- 必须是接口的匿名内部类，接口中**只能有一个**抽象方法	

![image-20220318144726046](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220318144726046.png)



![image-20220318144937807](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220318144937807.png)



**lambda表达式其实就是，单方法接口的匿名内部类的简化书写格式，在C++中使用仿函数作为函数参数，而在java中是用接口的对象作为参数。**

接口不能创建对象，必须要有一个类先实现接口，再由这个类创建对象，但这样写太麻烦了，于是就用到了匿名内部类。

![image-20220318150354814](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220318150354814.png)

Comparator接口有两个抽象方法，一个是compare，另一个是equals方法；这与函数式接口定义有冲突，因为在调用用lambda表达式调用Comparator接口中都是实现了compare方法，并没有实现equals，而equals是Object中的方法，所用的类都继承Object类，所以equals继承了Object中是实现，所以函数式接口(Functional Interface)就是一个有且仅有一个(除和Object中方法有相同签名的外)抽象方法，但是可以有多个非抽象方法的接口。



### 省略规则

**Lambda表达式的省略写法（进一步在Lambda表达式的基础上继续简化）**

1. 参数类型可以省略不写。
2. 如果只有一个参数，参数类型可以省略，同时()也可以省略。
3. 如果Lambda表达式的方法体代码只有一行代码。可以省略大括号不写,同时要省略分号！
4. 如果Lambda表达式的方法体代码只有一行代码。可以省略大括号不写。此时，如果这行代码是return语句，必须省略return不写，同时也必须省略";"不写



# 集合

- 数组定义后类型确定，长度固定
- 集合类型可以不固定，大小是可变的
- 数组可以存储基本类型和引用类型的数据。
- **集合只能存储引用数据类型的数据。**
- 数组适合做数据个数和类型确定的场景。
- 集合适合做数据个数不确定，且要做增删元素的场景。

![image-20220320150202779](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220320150202779.png)



## 泛型深入

- 泛型：是JDK5中引入的特性，可以在编译阶段约束操作的数据类型，并进行检查。
- 泛型的格式：<数据类型>; 注意：泛型只能支持引用数据类型。泛型：是JDK5中引入的特性，可以在编译阶段约束操作的数据类型，并进行检查。
- 集合体系的全部接口和实现类都是支持泛型的使用的。
- 统一数据类型。
- **把运行时期的问题提前到了编译期间，避免了强制类型转换可能出现的异常**，因为编译阶段类型就能确定下来。



### 泛型类

![image-20220321173953369](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220321173953369.png)



### 泛型方法

![image-20220321174104727](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220321174104727.png)



### 泛型接口

![image-20220321174135179](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220321174135179.png)



### 泛型通配符、上下限

![image-20220321174243429](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220321174243429.png)

![image-20220321174259356](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220321174259356.png)

```java
//通配符使用案例
在使用集合时，要确定数据类型，例如ArrayList<String> a;（集合的底层就是泛型）
  如果使用集合时无法确定类型，不能写Array<T> a;会报错，只能写Array<?> a;]
```



## Collection集合

![image-20220320150254339](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220320150254339.png)

```java
//集合对于泛型的支持
//集合都是支持泛型的，可以在编译阶段约束集合只能操作某种数据类型
Collection<String> lists = new ArrayList<String>();//这是多态的写法
Collection<String> lists = new ArrayList<>(); // JDK 1.7开始后面的泛型类型申明可以省略不写
ArrayList<String> lists1=new ArrayList<>();//我偏向于这么写，为什么吃饱了没事写多态呢？多态又不可以直接使用子类的独有功能
错误写法：ArrayList<int> lists1=new ArrayList<>();//不支持基本数据类型，可以用包装类代替
```

**注意：集合和泛型都只能支持引用数据类型，不支持基本数据类型**，所以集合中存储的元素都认为是对象。



![image-20220321091655211](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220321091655211.png)

***为什么上述最后一个API用Obeject[]接收返回值？**

**答：因为collection集合中的数据类型并不确定，而Ob**eject是所有类的父类，可以用来接收所有引用类型（多态的思想），当需要用到子类的特定方法时，只需把object类强制转换为该子类。



### Collection 集合的遍历方式

- 集合专有遍历方式
- Iterator<E> iterator()：得到迭代器对象，**默认指向当前集合的索引0**
- 迭代器越界报错：NoSuchElementException

#### 1.迭代器 Iterator

![image-20220321163349557](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220321163349557.png)

```Java
ArrayList<String> lists=new ArrayList<>();
Iterator<String> it = lists.iterator();
	while(it.hasNext()){
		String ele = it.next();
		System.out.println(ele);
}
```



#### 2.增强for循环

- 既可以遍历集合也可以遍历数组。

- 修改第三方变量的值不会影响到集合中的元素（用增强for取出来的元素值，其实是原来数据的拷贝）

```java
格式：
for(元素数据类型 变量名 : 数组或者Collection集合) {
         //在此处使用变量即可，该变量就是元素
}
举例：
Collection<String> list = new ArrayList<>();
...
for(String ele : list) {
	System.out.println(ele);
}
```



#### 3.Lambda表达式



![image-20220321170328083](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220321170328083.png)

```Java
//Consumer是一个函数接口
//定义：
@FunctionalInterface
public interface Consumer<T> {
  
    void accept(T t);
 
    default Consumer<T> andThen(Consumer<? super T> after) {
        Objects.requireNonNull(after);
        return (T t) -> { accept(t); after.accept(t); };
    }
}
```



```JAVA
//用lambda表达式之前
Collection<String> lists = new ArrayList<>();
...
lists.forEach(new Consumer<String>() {
	@Override
	public void accept(String s) {
	System.out.println(s);
	}
});
//foreach()底层其实就是用增强for来回调重写的Consumer匿名内部类方法；
default void forEach(Consumer<? super T> action) {
        Objects.requireNonNull(action);
        for (T t : this) {
            action.accept(t);
        }
    }

//用lambda表达式之后
lists.forEach(s -> {
    System.out.println(s);
});
//  lists.forEach(s -> System.out.println(s));
```

### 存储自定义类型的对象

![image-20220321171402573](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220321171402573.png)

### 集合的并发修改异常问题

![image-20220321173422011](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220321173422011.png)



### List系列集合

![image-20220321172059775](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220321172059775.png)

- 有序：存储和取出的元素顺序一致
- 有索引：可以通过索引操作元素
- 可重复：存储的元素可以重复
- **ArrayList**底层是基于**数组**实现的，根据查询元素快，增删相对慢。
- **LinkedList**底层基于**双链表**实现的，查询元素慢，增删首尾元素是非常快的。

![image-20220321171927394](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220321171927394.png)



#### ArrayList

- ArrayList底层是**基于数组实现的**：根据索引定位元素快，增删需要做元素的移位操作。
- 第一次创建集合并添加第一个元素的时候，在底层创建一个**默认长度为10**的数组。
- 当元素存满容器时，会按照1.5倍扩容

```Java
List<String> list = new ArrayList<>();
list.add("a");
//增加元素是在队尾，size指的是元素的个数，Java中好像没有提供方法获取容器的capacity
```



#### LinkedList

- **底层数据结构是双链表**，查询慢，首尾操作的速度是极快的，所以多了很多首尾操作的特有API。

![image-20220321173133857](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220321173133857.png)



### set系列集合

![image-20220322113436732](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220322113436732.png)

- HashSet : 无序、不重复、无索引。
- LinkedHashSet：有序、不重复、无索引。
- TreeSet：排序、不重复、无索引。
- **Set集合的功能上基本上与Collection的API一致。**



#### 哈希表

- **哈希值**：是JDK根据对象的**地址**，按照**哈希函数**算出来的**int类型**的数值。

- Object类的API： public int hashCode()；返回对象的哈希值
- 同一个对象多次调用hashCode()方法返回的哈希值是相同的
- 默认情况下，不同对象的哈希值是不同的。
- 默认长度16，默认加载因为0.75，当数组存满到16*0.75=12时，就自动扩容，每次扩容原先的两倍
- 当挂在元素下面的数据过多时，查询性能降低，从JDK8开始后，当链表长度超过8的时候，自动转换为红黑树。

![image-20220322114021173](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220322114021173.png)



#### HashSet

- **无序、不重复、无索引。**

- 底层结构：哈希表（数组、链表、红黑树的结合体）
- 去重复的原理：如果位置不为null，表示有元素，则调用equals方法比较；如果一样，则不存，如果不一样，则存入数组。
- 当存储**自定义类型对象**时，如果希望Set集合认为2个内容一样的对象是重复的，必须**重写对象的hashCode()和equals()方法**。(直接在对象的类中重写即可，可以用**快捷键**)

```Java
//例如：
public class Student {
    private String name;
    private int age;
    private char sex;

    public Student(String name, int age, char sex) {
        this.name = name;
        this.age = age;
        this.sex = sex;
    }
    //重写equals()
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return age == student.age && sex == student.sex && Objects.equals(name, student.name);
    }
    //重写hashCode()
    @Override
    public int hashCode() {
        return Objects.hash(name, age, sex);
    }
}
```



#### LinkedHashSet

- **有序、不重复、无索引。**
- 这里的有序指的是保证**存储和取出的元素顺序一致**
- 原理：底层数据结构是依然哈希表，只是每个元素又额外的多了一个**双链表的机制**记录存储的顺序。
- 不重复的原理和HashSet是一样的



#### **TreeSet**

- **不重复、无索引、可排序**
- 可排序：按照元素的大小默认升序（有小到大）排序，**当元素是自定义类型时需要自定义排序方法**。
- TreeSet集合**底层是基于红黑树的数据结构实现排序的**，增删改查性能都较好。
- 注意：TreeSet集合是一定要排序的，可以将元素按照指定的规则进行排序。

**TreeSet集合默认的规则**

1. 对于数值类型：Integer , Double，官方默认按照大小进行升序排序。
2. 对于字符串类型：默认按照首字符的编号升序排序。
3. 对于自定义类型如Student对象，TreeSet无法直接排序，需要自定义排序方法

**自定义排序方式一：**让自定义的类（如学生类）**实现Comparable接口重写里面的compareTo方法**来定制比较规则。

```Java
//方法一：实现Comparable接口重写里面的compareTo方法
public class Apple implements Comparable<Apple>{
    private String name;
    private String color;
    private double price;
    private int weight;

    public Apple(String name, String color, double price, int weight) {
        this.name = name;
        this.color = color;
        this.price = price;
        this.weight = weight;
    }

    @Override
    public int compareTo(Apple o) {
        // 按照重量进行比较的
        return this.weight - o.weight ; 
        //如果要保留相同重量的元素可写成 return (this.weight-o.weight)>=0 ? 1:-1;
    }
}
```

**自定义排序方式二：**TreeSet集合有参数构造器，可以**设置Comparator接口对应的比较器对象**，来定制比较规则。

```Java
 // 方式二：集合自带比较器对象进行规则定制
Set<Apple> apples = new TreeSet<>(new Comparator<Apple>() {
            @Override
            public int compare(Apple o1, Apple o2) {
                // return o1.getWeight() - o2.getWeight(); // 升序
                // return o2.getWeight() - o1.getWeight(); // 降序
                // 注意：浮点型建议直接使用Double.compare进行比较
                // return Double.compare(o1.getPrice() , o2.getPrice()); // 升序
                return Double.compare(o2.getPrice() , o1.getPrice()); // 降序
            }
        });
//可以简化为一行
Set<Apple> apples = new TreeSet<>(( o1,  o2) ->  Double.compare(o2.getPrice() , o1.getPrice()) );//lambda表达式
```

![image-20220322122423421](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220322122423421.png)



### 可变参数

- 可变参数用在形参中可以**接收多个数据**。
- **可变参数的格式：数据类型...参数名称**
- 传输参数非常灵活，方便。可以不传输参数，可以传输1个或者多个，也可以传输一个数组
- 可变参数在方法内部**本质上就是一个数组**。
- 1.一个形参列表中可变参数只能有一个
  2.可变参数必须放在形参列表的最后面

```Java
public class MethodDemo {
    public static void main(String[] args) {

        sum(); // 1、不传参数
        sum(10); // 2、可以传输一个参数
        sum(10, 20, 30); // 3、可以传输多个参数
        sum(new int[]{10, 20, 30, 40, 50}); // 4、可以传输一个数组
    }
    /**
       注意：一个形参列表中只能有一个可变参数,可变参数必须放在形参列表的最后面
     * @param nums
     */
    public static void sum(  int...nums){
        // 注意：可变参数在方法内部其实就是一个数组。 nums
        System.out.println("元素个数：" + nums.length);
        System.out.println("元素内容：" + Arrays.toString(nums));
    }
}
```



### Collections集合工具类

- java.utils.Collections:是集合工具类
- 作用：Collections并不属于集合，是用来**操作集合的工具类**。

![image-20220323105825402](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220323105825402.png)

![image-20220323110142582](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220323110142582.png)





## Map集合

- Map集合是一种双列集合，每个元素包含两个数据。
  Map集合的每个元素的**格式：key=value**(键值对元素)。
  Map集合也被称为“**键值对集合**”。
- Collection集合的格式: [元素1,元素2,元素3..]
  Map集合的完整格式：{key1=value1 , key2=value2 , key3=value3 , ...}

![image-20220323110608423](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220323110608423.png)

- HashMap:元素按照键是无序，不重复，无索引，值不做要求。（与Map体系一致）
- LinkedHashMap:元素按照键是有序，不重复，无索引，值不做要求。
- TreeMap：元素按照建是排序，不重复，无索引的，值不做要求。



![image-20220323110832228](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220323110832228.png)



### Map集合的遍历方式

#### 1.**键找值的方式遍历：**

**先获取Map集合全部的键，再根据遍历键找值。**

![image-20220323111052362](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220323111052362.png)

```java
Map<String , Integer> maps = new HashMap<>();
// 1.添加元素: 无序，不重复，无索引。
maps.put("娃娃",30);
maps.put("iphoneX",100);
maps.put("huawei",1000);
maps.put("生活用品",10);
maps.put("手表",10);
System.out.println(maps);
// maps = {huawei=1000, 手表=10, 生活用品=10, iphoneX=100, 娃娃=30}

// 1、键找值：第一步：先拿到集合的全部键。
Set<String> keys = maps.keySet();
// 2、第二步：遍历每个键，根据键提取值
for (String key : keys) {
    int value = maps.get(key);
    System.out.println(key + "===>" + value);
```

#### 2.键值对的方式遍历

**把“键值对“看成一个整体，难度较大。**

1. 先把Map集合转换成Set集合，Set集合中每个元素都是键值对实体类型了。
2. 遍历Set集合，然后提取键以及提取值。

![image-20220323111935636](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220323111935636.png)

```Java
 // 1、把Map集合转换成Set集合
        Set<Map.Entry<String, Integer>> entries = maps.entrySet();
        // 2、开始遍历
        for(Map.Entry<String, Integer> entry : entries){
            String key = entry.getKey();
            int value = entry.getValue();
            System.out.println(key + "====>" + value);
        }
    }
```



- Map是java中的接口，Map.Entry是Map的一个内部接口。
- Map提供了一些常用方法，如keySet()、entrySet()等方法。
- **keySet()方法返回值是Map中key值的集合；entrySet()的返回值也是返回一个Set集合，此集合存储的数据类型为Map.Entry类的对象。**
- **Map.Entry是Map声明的一个内部静态类，该类为泛型，定义为Entry<K,V>。它表示Map中的一个实体（一个key-value对）。接口中有getKey(),getValue方法。**



#### 3.Lambda表达式

JDK 1.8开始之后的新技术：Lambda表达式。

![image-20220323113249727](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220323113249727.png)

```Java
//BiConsumer其实就是有两个参数的Consumer，是一个函数接口，其内部也只有一个action方法用于回调，主要用于forEach（）遍历；
public class MapDemo03 {
    public static void main(String[] args) {
        Map<String , Integer> maps = new HashMap<>();
        // 1.添加元素: 无序，不重复，无索引。
        maps.put("娃娃",30);
        maps.put("iphoneX",100);//  Map集合后面重复的键对应的元素会覆盖前面重复的整个元素！
        maps.put("huawei",1000);
        maps.put("生活用品",10);
        maps.put("手表",10);
        System.out.println(maps);

          //maps = {huawei=1000, 手表=10, 生活用品=10, iphoneX=100, 娃娃=30}
        maps.forEach(new BiConsumer<String, Integer>() {
            @Override
            public void accept(String key, Integer value) {
                System.out.println(key + "--->" + value);
            }
        });
        //简写
        maps.forEach((k, v) -> System.out.println(k + "--->" + v));
    }
}
```



### HashMap

- 使用最多的Map集合是HashMap。

- HashMap是Map里面的一个实现类。特点都是由键决定的：**无序、不重复、无索引**

- 没有额外需要学习的特有方法，直接使用Map里面的方法就可以了。

- **HashMap跟HashSet底层原理是一模一样的**，都是哈希表结构，只是HashMap的每个元素包含两个值而已。

  实际上：Set系列集合的底层就是Map实现的，只是Set集合中的元素只要键数据，不要值数据而已。

- 注意事项：

1. 依赖hashCode方法和equals方法保证键的唯一。
2. 如果键要存储的是**自定义对象**，**需要重写hashCode和equals方法**。具体实现方法同HashSet



### LinkedHashMap

- 由键决定：**有序、不重复、无索引**。
- 这里的有序指的是保证存储和取出的元素顺序一致
- 原理：底层数据结构是依然哈希表，只是每个键值对元素又额外的多了一个双链表的机制记录存储的顺序。同LinkHashSet

![image-20220323192739190](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220323192739190.png)

### TreeMap

- 由键决定特性：**不重复、无索引、可排序**
- 可排序：按照键数据的大小默认升序（有小到大）排序。只能对键排序。
- 注意：TreeMap集合是一定要排序的，可以默认排序，也可以将键按照指定的规则进行排序，**如果键值是自定义对象，则一定要自行定义排序方法**
- **TreeMap跟TreeSet一样底层原理是一样的。**



​	**TreeMap集合自定义排序规则有2种，同TreeSet**

1. 类实现Comparable接口，重写比较规则。
2. 集合自定义Comparator比较器对象，重写比较规则。



## 不可变集合

- 不可变集合，就是**不可被修改**的集合。不可以添加、删除或者修改元素；
- 集合的数据项在创建的时候提供，并且在整个生命周期中都不可改变。否则报错。

![image-20220325145156374](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220325145156374.png)

```Java
 // 1、不可变的List集合
        List<Double> lists = List.of(569.5, 700.5, 523.0,  570.5);

        // 2、不可变的Set集合
        Set<String> names = Set.of("迪丽热巴", "迪丽热九", "马尔扎哈", "卡尔眨巴" );

        // 3、不可变的Map集合
        Map<String, Integer> maps = Map.of("huawei",2, "Java开发", 1 , "手表", 1);
```



# Stream流

- 在Java 8中，得益于**Lambda**所带来的函数式编程， 引入了一个全新的Stream流概念。
- 目的：用于**简化集合和数组操作的API**，例如：

```Java
names.stream().filter(s -> s.startsWith("张")).filter(s -> s.length() == 3).forEach(s -> System.out.println(s));
```

- Stream操作集合或者数组的第一步是先得到Stream流，然后才能使用流的功能。

![image-20220325145711919](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220325145711919.png)



## 获取Stream流

![image-20220325145904181](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220325145904181.png)

```Java
  /** --------------------Collection集合获取流-------------------------------   */
        Collection<String> list = new ArrayList<>();
        Stream<String> s =  list.stream();

        /** --------------------Map集合获取流-------------------------------   */
        Map<String, Integer> maps = new HashMap<>();
        // 键流
        Stream<String> keyStream = maps.keySet().stream();
		//maps.keySet()把map中的键提取成一个set集合，所以最终获取流还是通过collection的stream方法
        // 值流
        Stream<Integer> valueStream = maps.values().stream();
        // 键值对流（拿整体）
        Stream<Map.Entry<String,Integer>> keyAndValueStream =  maps.entrySet().stream();
```

![image-20220325150609438](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220325150609438.png)

```Java
/** ---------------------数组获取流------------------------------   */
        String[] names = {"赵敏","小昭","灭绝","周芷若"};
        Stream<String> nameStream = Arrays.stream(names);//Arrays工具类的静态函数
        Stream<String> nameStream2 = Stream.of(names);//Stream接口的静态方法
```



## Stream流的常用API

- 中间方法也称为非终结方法，调用完成后**返回新的Stream流**可以继续使用，支持链式编程。
- 在Stream流中无法直接修改集合、数组中的数据，因为**进入流中的数据是拷贝**。
- 注意：终结操作方法，调用完成后流就无法继续使用了，原因是不会返回Stream了。

![image-20220325155700228](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220325155700228.png)

![image-20220325155717590](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220325155717590.png)

```Java
 // Stream<T> filter(Predicate<? super T> predicate)
        list.stream().filter(new Predicate<String>() {
            @Override
            public boolean test(String s) {
                return s.startsWith("张");
            }
        });//原码，底层会遍历每个元素，交给test()方法，返回值为真则保留当前元素

        list.stream().filter(s -> s.startsWith("张")).forEach(s -> System.out.println(s));//lambda表达式简化后

        long size = list.stream().filter(s -> s.length() == 3).count();
        System.out.println(size);

       // list.stream().filter(s -> s.startsWith("张")).limit(2).forEach(s -> System.out.println(s));
        list.stream().filter(s -> s.startsWith("张")).limit(2).forEach(System.out::println);

        list.stream().filter(s -> s.startsWith("张")).skip(2).forEach(System.out::println);

// map加工方法: 第一个参数原材料  -> 第二个参数是加工后的结果。
        // 给集合元素的前面都加上一个：黑马的：
		list.stream().map(new Function<String, String>() {
            @Override
            public String apply(String s) {
                return  "黑马的：" + s;
            }
        });//源码，底层会遍历每个元素，放入apply()方法中加工；

        list.stream().map(s -> "黑马的：" + s).forEach(a -> System.out.println(a));//lambda表达式简化后

        // 需求：把所有的名称 都加工成一个学生对象。
         list.stream().map(s -> new Student(s)).forEach(s -> System.out.println(s));
		//list.stream().map(Student::new).forEach(System.out::println); // 构造器引用  方法引用

// 合并流。
        Stream<String> s1 = list.stream().filter(s -> s.startsWith("张"));
        Stream<String> s2 = Stream.of("java1", "java2");
        // public static <T> Stream<T> concat(Stream<? extends T> a, Stream<? extends T> b)
        Stream<String> s3 = Stream.concat(s1 , s2);
        s3.distinct().forEach(s -> System.out.println(s));
```



## Stream流的收集操作

- 收集Stream流的含义：就是把Stream流操作后的结果数据转回到集合或者数组中去。

- Stream流：方便操作集合/数组的**手段**。
- 集合/数组：才是开发中的**目的**。

![image-20220325160230155](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220325160230155.png)

```Java
Stream<String> s1 = list.stream().filter(s -> s.startsWith("张"));
        List<String> zhangList = s1.collect(Collectors.toList()); // 可变集合
        zhangList.add("java1");
        System.out.println(zhangList);

//       List<String> list1 = s1.toList(); // 得到不可变集合
//       list1.add("java");
//       System.out.println(list1);

        // 注意注意注意：“流只能使用一次”
        Stream<String> s2 = list.stream().filter(s -> s.startsWith("张"));
        Set<String> zhangSet = s2.collect(Collectors.toSet());
        System.out.println(zhangSet);

        Stream<String> s3 = list.stream().filter(s -> s.startsWith("张"));
        Object[] arrs1 = s3.toArray();//默认用object类型接收，因为数据可能不纯
        String[] arrs = s3.toArray(String[]::new); // 强制用string类型介绍，底层原理不管
        System.out.println("Arrays数组内容：" + Arrays.toString(arrs));
```



# 异常处理

- 异常是程序在“编译”或者“执行”的过程中可能出现的问题，注意：语法错误不算在异常体系中。 
- 比如:数组索引越界、空指针异常、 日期格式化异常，等…
- **异常一旦出现了，如果没有提前处理，程序就会退出JVM虚拟机而终止.**
- 研究异常并且避免异常，然后提前处理异常，体现的是程序的**安全, 健壮性**。

![image-20220325162816987](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220325162816987.png)



![image-20220325162912571](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220325162912571.png)



## 运行时异常

直接继承自RuntimeException或者其子类，编译阶段不会报错，运行时可能出现的错误。

**运行时异常示例**

- 数组索引越界异常: ArrayIndexOutOfBoundsException
- 空指针异常 : NullPointerException，直接输出没有问题，但是调用空指针的变量的功能就会报错。
- 数学操作异常：ArithmeticException
- 类型转换异常：ClassCastException
- 类型转换异常：ClassCastException

运行时异常：一般是程序员业务没有考虑好或者是编程逻辑不严谨引起的程序错误，**自己的水平有问题**！



## 编译时异常

- 不是RuntimeException或者其子类的异常，编译阶就报错，必须处理，否则代码不通过。
- 如果方法内部定义了一个**编译异常情况**（该异常是编译异常类或其子类的对象），那么调用该方法时就必须要先处理异常，例如时间解析方法就必须先处理异常。这样做的好处是提醒程序员该方法可能会出现异常。

```Java
//编译异常示例：
String date = "2015-01-12 10:23:21";
SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
Date d = sdf.parse(date);//日期解析异常：ParseException
System.out.println(d);
```

**编译时异常的作用是什么：**

- 是担心程序员的技术不行，在编译阶段就爆出一个错误, 目的在于提醒不要出错!
- 编译时异常是可遇不可求。遇到了就遇到了呗。



## 异常的默认处理流程

1. 默认会在出现异常的代码那里自动的创建一个异常对象：ArithmeticException（或者其他种类的异常）。
2. 异常会从方法中出现的点这里抛出给调用者，调用者最终抛出给JVM虚拟机。
3. 虚拟机接收到异常对象后，先在控制台直接输出异常栈信息数据。
4. 直接从当前执行的异常点干掉当前程序。
5. 后续代码没有机会执行了，因为程序已经死亡。（非常不好）



## 编译时异常的处理机制

编译时异常的处理形式有三种：

1. 出现异常直接抛出去给调用者，调用者也继续抛出去。
2. 出现异常自己捕获处理，不麻烦别人。
3. 前两者结合，出现异常直接抛出去给调用者，调用者捕获处理。



### 异常处理方式1 - throws

- throws：用在方法上，可以将方法内部出现的异常抛出去给本方法的调用者处理。
- 这种方式并不好，发生异常的方法自己不处理异常，如果异常最终抛出去给虚拟机将引起程序死亡。

![image-20220325164049136](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220325164049136.png)

```Java
public static void main(String[] args) throws Exception {
    System.out.println("程序开始。。。。。");
    parseTime("2011-11-11 11:11:11");
    System.out.println("程序结束。。。。。");
}

public static void parseTime(String date) throws Exception {
    SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
    Date d = sdf.parse(date);
    System.out.println(d);
    InputStream is = new FileInputStream("E:/meinv.jpg");
}
```



### 异常处理方式2 - try catch

- 监视捕获异常，**用在方法内部**，可以将方法内部出现的异常直接捕获处理。
- 这种方式还可以，发生异常的方法自己**独立完成异常的处理，程序可以继续往下执行**。
- 注意：一个整体尽量放在一起try，因为如果前面出现异常，后面的代码再执行就没意义了。

![image-20220325164404197](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220325164404197.png)

```Java
public static void main(String[] args) {
    System.out.println("程序开始。。。。");
    parseTime("2011-11-11 11:11:11");
    System.out.println("程序结束。。。。");
}

public static void parseTime(String date) {
    try {
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy/MM-dd HH:mm:ss");
        Date d = sdf.parse(date);
        System.out.println(d);

        InputStream is = new FileInputStream("E:/meinv.jpg");
    } catch (Exception e) {
        e.printStackTrace(); // 打印异常栈信息
    }
}
```



### 异常处理方式3 - 前两者结合

- 方法直接将异通过throws抛出去给调用者
- 调用者收到异常后直接捕获处理。

```Java
public static void main(String[] args) {
    System.out.println("程序开始。。。。");
    try {
        parseTime("2011-11-11 11:11:11");
        System.out.println("功能操作成功~~~");
    } catch (Exception e) {
        e.printStackTrace();
        System.out.println("功能操作失败~~~");
    }
    System.out.println("程序结束。。。。");
}

public static void parseTime(String date) throws Exception {
    SimpleDateFormat sdf = new SimpleDateFormat("yyyy、MM-dd HH:mm:ss");
    Date d = sdf.parse(date);
    System.out.println(d);

    InputStream is = new FileInputStream("D:/meinv.jpg");
}
```

- 在开发中按照规范来说第三种方式是最好的：底层的异常抛出去给最外层，最外层集中捕获处理。
- 实际应用中，只要代码能够编译通过，并且功能能完成，那么每一种异常处理方式似乎也都是可以的。



## 运行时异常的处理形式

- 运行时异常编译阶段不会出错，是运行时才可能出错的，所以编译阶段不处理也可以。

- 按照规范建议还是处理：建议在最外层调用处集中捕获处理即可。
- 运行时出现异常是自动向上层throw的，不用写

```java
public class Test {
    public static void main(String[] args) {
        System.out.println("程序开始。。。。。。。。。。");
        try {
            chu(10, 0);
        } catch (Exception e) {
            e.printStackTrace();
        }
        System.out.println("程序结束。。。。。。。。。。");
    }

    public static void chu(int a , int b) { // throws RuntimeException{
        System.out.println(a);
        System.out.println(b);
        int c = a / b;
        System.out.println(c);
    }
}
```



## 自定义异常

- Java无法为这个世界上全部的问题提供异常类。
- 如果企业想通过异常的方式来管理自己的某个业务问题，就需要自定义异常类了。



### 自定义编译时异常 

1. 定义一个异常类继承Exception.
2.  重写构造器。
3.  在出现异常的地方用throw new 自定义对象抛出
4. 作用：编译时异常是编译阶段就报错，提醒更加强烈，一定需要处理！！

**在方法体内部定义一个编译异常情况，那么调用该方法时必须先处理异常，因为我定义了异常情况，说明调用该方法就有可能产生异常，而编译异常是在编译时就需要处理的。**

```Java
public class ItheimaAgeIlleagalException extends Exception{ //继承编译异常类
    public ItheimaAgeIlleagalException() {  //无参构造器
    }

    public ItheimaAgeIlleagalException(String message) { //有参构造器
        super(message); //直接用父类中的异常显示方法就行，message是需要显示的信息
    }
}

public class ExceptionDemo {
    public static void main(String[] args) {
        try {
            checkAge2(-23);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static void checkAge(int age) throws ItheimaAgeIlleagalException {//因为方法体中有编译异常情况，所以这里一定要抛异常
        if(age < 0 || age > 200){
            // 抛出去一个异常对象给调用者
            // throw ：在方法内部直接创建一个异常对象，并从此点抛出
            // throws : 用在方法申明上的，抛出方法内部的异常
            throw new ItheimaAgeIlleagalException(age + " is illeagal!");//创建一个异常对象，并将它抛出去
        }else {
            System.out.println("年龄合法：推荐商品给其购买~~");
        }
    }
}
```



### 自定义运行时异常

1. 定义一个异常类继承RuntimeException.
2. 重写构造器。
3. 在出现异常的地方用throw new 自定义对象抛出!
4. 作用：提醒不强烈，**编译阶段不报错**！！运行时才可能出现！！

```Java
public class ItheimaAgeIlleagalRuntimeException extends RuntimeException{
    public ItheimaAgeIlleagalRuntimeException() {//继承运行时异常类
    }

    public ItheimaAgeIlleagalRuntimeException(String message) {
        super(message);
    }
}
public class ExceptionDemo {
    public static void main(String[] args) {

        try {
            checkAge2(-23);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static void checkAge2(int age)  {//因为方法体中是运行时异常，运行时才报错，并且出错了会自动抛出，所以这里不用写throws
        if(age < 0 || age > 200){
            // 抛出去一个异常对象给调用者
            // throw ：在方法内部直接创建一个异常对象，并从此点抛出
            // throws : 用在方法申明上的，抛出方法内部的异常
            throw new ItheimaAgeIlleagalRuntimeException(age + " is illeagal!");//定义一个运行时异常，并将其抛出
        }else {
            System.out.println("年龄合法：推荐商品给其购买~~");
        }
    }

}
```



# 日志框架 - Logback

程序中的日志可以用来记录程序运行过程中的信息，并可以进行永久存储。

***最重要的是要记住，控制信息是记录在lockback.xml文件里面的，进去修改相关参数就可以，注释都写得很清楚**。

代码就照着下图写就行了。

![image-20220326135746632](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220326135746632.png)



- Logback主要分为三个技术模块：
- logback-core： logback-core 模块为其他两个模块奠定了基础，必须有。
-  logback-classic：它是log4j的一个改良版本，同时它完整实现了slf4j API。
-  logback-access 模块与 Tomcat 和 Jetty 等 Servlet 容器集成，以提供 HTTP 访问日志功能



![image-20220326134158064](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220326134158064.png)

![image-20220326134309276](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220326134309276.png)

![image-20220326134400588](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220326134400588.png)





# File/IO流

- File类可以定位文件：进行删除、获取文本本身信息等操作。但是不能读写文件内容。
- IO流技术可以对硬盘中的文件进行读写



## File类

- File类在包java.io.File下、代表操作系统的文件对象（文件、文件夹）。
- File类提供了诸如：定位文件，获取文件本身的信息、删除文件、创建文件（文件夹）等功能。

![image-20220401170824513](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220401170824513.png)

![image-20220401170858362](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220401170858362.png)



![image-20220401171029903](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220401171029903.png)

![image-20220401171125788](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220401171125788.png)

![image-20220401171252101](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220401171252101.png)



## 字符集

- 计算机底层可以表示十进制编号。计算机可以给人类字符进行编号存储，这套编号规则就是字符集。
- 编码前的字符集和编码好的字符集必须一致，否则会出现中文字符乱码
- 英文和数字在任何国家的编码中都不会乱码

### 常见字符集

![image-20220401171623086](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220401171623086.png)

![image-20220401172150360](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220401172150360.png)



### 字符集的编码、解码操作

![image-20220401172709763](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220401172709763.png)

```Java
// 1、编码：把文字转换成字节（使用指定的编码）
String name = "abc我爱你中国";
// byte[] bytes = name.getBytes(); // 以当前代码默认字符集进行编码 （UTF-8）
byte[] bytes = name.getBytes("GBK"); // 指定编码
System.out.println(bytes.length);
System.out.println(Arrays.toString(bytes));

// 2、解码：把字节转换成对应的中文形式（编码前 和 编码后的字符集必须一致，否则乱码 ）
// String rs = new String(bytes); // 默认的UTF-8
String rs = new String(bytes, "GBK"); // 指定GBK解码
System.out.println(rs);
```



## 原始IO流

- I表示input，是数据从硬盘文件读入到内存的过程，称之输入，负责读。
- O表示output，是内存程序的数据从内存到写出到硬盘文件的过程，称之输出，负责写。

**流的四大类:**

- 字节输入流：以内存为基准，来自磁盘文件/网络中的数据**以字节的形式**读入到内存中去的流称为字节输入流。
- 字节输出流：以内存为基准，把内存中的数据**以字节**写出到磁盘文件或者网络中去的流称为字节输出流。
- 字符输入流：以内存为基准，来自磁盘文件/网络中的数据**以字符**的形式读入到内存中去的流称为字符输入流。
- 字符输出流：以内存为基准，把内存中的数据**以字符**写出到磁盘文件或者网络介质中去的流称为字符输出流。

![image-20220401173027920](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220401173027920.png)



### 字节流

#### 文件字节输入流

![image-20220401173329114](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220401173329114.png)

```Java
InputStream is = new FileInputStream("file-io-app\\src\\data.txt");//相对路径
 //一次读取一个字节
int b;
while (( b = is.read() ) != -1){
    System.out.print((char) b);
}//因为一次只读一个字节，而UTF-8的中文字占三个字节，所以输出中文会乱码，但如果是将文件中所有内容拷贝的话则不会出错。

//一次读取一个字节数组
byte[] buffer = new byte[3];//一次读取3个字节
        int len; // 记录每次实际读取的字节数。
        while ((len = is.read(buffer)) != -1) {
            // 读取多少倒出多少
            System.out.print(new String(buffer, 0 , len));
        }
```



**一次读完全部字节，从而使中文不乱码，且读取效率提高**，但文件太大时可能会导致内存溢出

![image-20220401174524088](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220401174524088.png)

```Java
		 // 1、创建一个文件字节输入流管道与源文件接通
        File f = new File("file-io-app/src/data03.txt");
        InputStream is = new FileInputStream(f);

        // 2、定义一个字节数组与文件的大小刚刚一样大。
        byte[] buffer = new byte[(int) f.length()];
        int len = is.read(buffer);
        System.out.println("读取了多少个字节：" + len);
        System.out.println("文件大小：" + f.length());
        System.out.println(new String(buffer));

        // 读取全部字节数组
        byte[] buffer = is.readAllBytes();
        System.out.println(new String(buffer));
```



#### 文件字节输出流

作用：以内存为基准，把内存中的数据以字节的形式写出到磁盘文件中去的流。

![image-20220401175524926](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220401175524926.png)

![image-20220401175557897](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220401175557897.png)

```Java
  // 1、创建一个文件字节输出流管道与目标文件接通
        OutputStream os = new FileOutputStream("file-io-app/src/out04.txt" , true); // 追加数据管道
//      OutputStream os = new FileOutputStream("file-io-app/src/out04.txt"); // 先清空之前的数据，写新数据进入

        // 2、写数据出去
        // a.public void write(int a):写一个字节出去
        os.write('a');
        os.write(98);
        os.write("\r\n".getBytes()); // 换行
        // os.write('徐'); // [ooo]

        // b.public void write(byte[] buffer):写一个字节数组出去。
        byte[] buffer = {'a' , 97, 98, 99};
        os.write(buffer);
        os.write("\r\n".getBytes()); // 换行

        byte[] buffer2 = "我是中国人".getBytes();
//      byte[] buffer2 = "我是中国人".getBytes("GBK");
        os.write(buffer2);
        os.write("\r\n".getBytes()); // 换行


        // c. public void write(byte[] buffer , int pos , int len):写一个字节数组的一部分出去。
        byte[] buffer3 = {'a',97, 98, 99};
        os.write(buffer3, 0 , 3);
        os.write("\r\n".getBytes()); // 换行

        // os.flush(); // 写数据必须，刷新数据 可以继续使用流
        os.close(); // 释放资源，包含了刷新的！关闭后流不可以使用了
    }
```



#### 文件拷贝

**字节流适合做一切文件数据的拷贝**：任何文件的底层都是字节，拷贝是一字不漏的转移字节，只要前后文件格式、编码一致没有任何问题。

```Java
try {
    // 1、创建一个字节输入流管道与原视频接通
    InputStream is = new FileInputStream("file-io-app/src/out04.txt");

    // 2、创建一个字节输出流管道与目标文件接通
    OutputStream os = new FileOutputStream("file-io-app/src/out05.txt");

    // 3、定义一个字节数组转移数据
    byte[] buffer = new byte[1024];
    int len; // 记录每次读取的字节数。
    while ((len = is.read(buffer)) != -1){
        os.write(buffer, 0 , len);
    }
    System.out.println("复制完成了！");

    // 4、关闭流。
    os.close();
    is.close();
} catch (Exception e){
    e.printStackTrace();
}
```



### 资源释放方式

#### try-catch-finally

![image-20220401195356593](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220401195356593.png)

#### try-with-resource

finally虽然可以用于释放资源，但是释放资源的代码过于繁琐

![image-20220401195539817](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220401195539817.png)

**JDK 7 以及 JDK 9的()中只能放置资源对象，否则报错**
**什么是资源呢？**
**资源都是实现了Closeable/AutoCloseable接口的类对象**

```Java
        try (
                // 这里面只能放置资源对象，用完会自动关闭：自动调用资源对象的close方法关闭资源（即使出现异常也会做关闭操作）
                // 1、创建一个字节输入流管道与原视频接通
               InputStream is = new FileInputStream("file-io-app/src/out04.txt");
                // 2、创建一个字节输出流管道与目标文件接通
               OutputStream os = new FileOutputStream("file-io-app/src/out05.txt");

               // int age = 23; // 这里只能放资源
                MyConnection connection = new MyConnection(); // 最终会自动调用资源的close方法
                ) {

            // 3、定义一个字节数组转移数据
            byte[] buffer = new byte[1024];
            int len; // 记录每次读取的字节数。
            while ((len = is.read(buffer)) != -1){
                os.write(buffer, 0 , len);
            }
            System.out.println("复制完成了！");

        } catch (Exception e){
            e.printStackTrace();
        }

    }
}

class MyConnection implements AutoCloseable{
    @Override
    public void close() throws IOException {
        System.out.println("连接资源被成功释放了！");
    }
```



### 字符流

- 字节流读取中文输出会乱码。或者内存溢出。

- 读取中文输出，字符流更合适，最小单位是按照单个字符读取的。



#### 文件字符输入流

![image-20220401202259863](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220401202259863.png)

```Java
Reader fr = new FileReader("file-io-app\\src\\data06.txt");
int code;
//每次读取一个字符
while ((code = fr.read()) != -1){
	System.out.print((char) code);
}

 // 2、用循环，每次读取一个字符数组的数据。  1024 + 1024 + 8
        char[] buffer = new char[1024]; // 1K字符
        int len;
        while ((len = fr.read(buffer)) != -1) {
            String rs = new String(buffer, 0, len);
            System.out.print(rs);
        }
```

#### 文件字符输出流

![image-20220401202412234](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220401202412234.png)

![image-20220401202448931](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220401202448931.png)

```Java
 // 1、创建一个字符输出流管道与目标文件接通
        // Writer fw = new FileWriter("file-io-app/src/out08.txt"); // 覆盖管道，每次启动都会清空文件之前的数据
        Writer fw = new FileWriter("file-io-app/src/out08.txt", true); // 覆盖管道，每次启动都会清空文件之前的数据

//      a.public void write(int c):写一个字符出去
        fw.write(98);
        fw.write('a');
        fw.write('徐'); // 不会出问题了
        fw.write("\r\n"); // 换行

//       b.public void write(String c)写一个字符串出去
        fw.write("abc我是中国人");
        fw.write("\r\n"); // 换行

//       c.public void write(char[] buffer):写一个字符数组出去
        char[] chars = "abc我是中国人".toCharArray();
        fw.write(chars);
        fw.write("\r\n"); // 换行

//       d.public void write(String c ,int pos ,int len):写字符串的一部分出去
        fw.write("abc我是中国人", 0, 5);
        fw.write("\r\n"); // 换行

//       e.public void write(char[] buffer ,int pos ,int len):写字符数组的一部分出去
        fw.write(chars, 3, 5);
        fw.write("\r\n"); // 换行

        // fw.flush();// 刷新后流可以继续使用
        fw.close(); // 关闭包含刷线，关闭后流不能使用
```



## 缓冲流

- 缓冲流也称为**高效流**、或者高级流。之前学习的字节流可以称为原始流。
- 作用：**缓冲流自带缓冲区、可以提高原始字节流、字符流读写数据的性能**
- 字节缓冲输入流： BufferedInputStream
  字节缓冲输出流：BufferedOutputStream
  字符缓冲输入流：BufferedReader
  字符缓冲输出流：BufferedWriter

![image-20220402153745087](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220402153745087.png)

![image-20220402211223667](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220402211223667.png)

### 字节缓冲流

- 字节缓冲输入流自带了8KB缓冲池，以后我们直接从缓冲池读取数据，所以性能较好。
- 字节缓冲输出流自带了8KB缓冲池，数据就直接写入到缓冲池中去，写数据性能极高了。
- 使用方法就是将原始流包装成缓冲流，功能以及方法调用上并没有变化

![image-20220402154652779](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220402154652779.png)

```Java
try (
        // 这里面只能放置资源对象，用完会自动关闭：自动调用资源对象的close方法关闭资源（即使出现异常也会做关闭操作）
        // 1、创建一个字节输入流管道与原视频接通
        InputStream is = new FileInputStream("D:\\resources\\newmeinv.jpeg");
        // a.把原始的字节输入流包装成高级的缓冲字节输入流
        InputStream bis = new BufferedInputStream(is);
        // 2、创建一个字节输出流管道与目标文件接通
        OutputStream os = new FileOutputStream("D:\\resources\\newmeinv222.jpeg");
        // b.把字节输出流管道包装成高级的缓冲字节输出流管道
        OutputStream bos = new BufferedOutputStream(os);

) {

    // 3、定义一个字节数组转移数据
    byte[] buffer = new byte[1024];
    int len; // 记录每次读取的字节数。
    while ((len = bis.read(buffer)) != -1){
        bos.write(buffer, 0 , len);
    }
    System.out.println("复制完成了！");

} catch (Exception e){
    e.printStackTrace();
}
```



### 字符缓冲流

![image-20220402155017620](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220402155017620.png)

```Java
  try (
                // 1、创建一个文件字符输入流与源文件接通。
                Reader fr = new FileReader("io-app2/src/data01.txt");
                // a、把低级的字符输入流包装成高级的缓冲字符输入流。
                BufferedReader br = new BufferedReader(fr);
                ){

            // 2、用循环，每次读取一个字符数组的数据。  1024 + 1024 + 8
//            char[] buffer = new char[1024]; // 1K字符
//            int len;
//            while ((len = br.read(buffer)) != -1) {
//                String rs = new String(buffer, 0, len);
//                System.out.print(rs);
//            }

              String line;
              while ((line = br.readLine()) != null){
                  System.out.println(line);
              }
        } catch (IOException e) {
            e.printStackTrace();
        }
```

![image-20220402155155504](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220402155155504.png)

```Java
  // 1、创建一个字符输出流管道与目标文件接通
        FileWriter fw = new FileWriter("io-app2/src/out02.txt"); // 覆盖管道，每次启动都会清空文件之前的数据
       //Writer fw = new FileWriter("io-app2/src/out02.txt", true); // 追加数据
        BufferedWriter bw = new BufferedWriter(fw);

//      a.public void write(int c):写一个字符出去
        bw.write(98);
        bw.write('a');
        bw.write('徐'); // 不会出问题了
        bw.newLine(); // bw.write("\r\n"); // 换行

//       b.public void write(String c)写一个字符串出去
        bw.write("abc我是中国人");
        bw.newLine(); // bw.write("\r\n"); // 换行

//       c.public void write(char[] buffer):写一个字符数组出去
        char[] chars = "abc我是中国人".toCharArray();
        bw.write(chars);
        bw.newLine(); // bw.write("\r\n"); // 换行

//       d.public void write(String c ,int pos ,int len):写字符串的一部分出去
        bw.write("abc我是中国人", 0, 5);
        bw.newLine(); // bw.write("\r\n"); // 换行

//       e.public void write(char[] buffer ,int pos ,int len):写字符数组的一部分出去
        bw.write(chars, 3, 5);
        bw.newLine(); // bw.write("\r\n"); // 换行

        // fw.flush();// 刷新后流可以继续使用
        bw.close(); // 关闭包含刷线，关闭后流不能使用
```



## 转换流

- 如果代码编码和文件编码不一致，使用字符流**直接读取会乱码**。
- 使用字符输入转换流，可以提取文件（GBK）的**原始字节流**，原始字节不会存在问题。然后把字节流以指定编码转换成字符输入流，这样字符输入流中的字符就不乱码了

![image-20220402204703832](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220402204703832.png)

![image-20220402205110967](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220402205110967.png)

```Java
// 代码UTF-8   文件 GBK  "D:\\resources\\data.txt"
// 1、提取GBK文件的原始字节流。  
InputStream is = new FileInputStream("D:\\resources\\data.txt");
// 2、把原始字节流转换成字符输入流
// Reader isr = new InputStreamReader(is); // 默认以UTF-8的方式转换成字符流。 还是会乱码的  跟直接使用FileReader是一样的
Reader isr = new InputStreamReader(is , "GBK"); // 以指定的GBK编码转换成字符输入流  完美的解决了乱码问题

BufferedReader br = new BufferedReader(isr);//再用缓冲流将转换流包装，提高效率
String line;
while ((line = br.readLine()) != null){
    System.out.println(line);
}
```

![image-20220402205519411](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220402205519411.png)

```Java
// 1、定义一个字节输出流
OutputStream os = new FileOutputStream("io-app2/src/out03.txt");

// 2、把原始的字节输出流转换成字符输出流
// Writer osw = new OutputStreamWriter(os); // 以默认的UTF-8写字符出去 跟直接写FileWriter一样
Writer osw = new OutputStreamWriter(os , "GBK"); // 指定GBK的方式写字符出去

// 3、把低级的字符输出流包装成高级的缓冲字符输出流。
BufferedWriter bw = new BufferedWriter(osw);

bw.write("我爱中国1~~");
bw.write("我爱中国2~~");
bw.write("我爱中国3~~");

bw.close();
```



## 序列化对象

- 作用：以内存为基准，把内存中的对象存储到磁盘文件中去，称为对象序列化。
- 使用到的流是对象字节输出流：ObjectOutputStream
- 序列化对象的要求：对象必须实现序列化接口

![image-20220402210833012](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220402210833012.png)

![image-20220402211005921](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220402211005921.png)

```Java
// 1、创建学生对象
Student s = new Student("陈磊", "chenlei","1314520", 21);

// 2、对象序列化：使用对象字节输出流包装字节输出流管道
ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("io-app2/src/obj.txt"));

// 3、直接调用序列化方法
oos.writeObject(s);

// 4、释放资源
oos.close();

//对象如果要序列化，必须实现Serializable序列化接口。
public class Student implements Serializable {
    // 申明序列化的版本号码
    // 序列化的版本号与反序列化的版本号必须一致才不会出错！
    private static final long serialVersionUID = 1;
    private String name;
    private String loginName;
    // transient修饰的成员变量不参与序列化了
    private transient String passWord;
    private int age ;

    public Student(String name, String loginName, String passWord, int age) {
        this.name = name;
        this.loginName = loginName;
        this.passWord = passWord;
        this.age = age;
    }
```



### 对象反序列化

- 使用到的流是对象字节输入流：ObjectInputStream
- 作用：以内存为基准，把存储到磁盘文件中去的对象数据恢复成内存中的对象，称为对象反序列化。

![image-20220402211822154](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220402211822154.png)

```Java
// 1、创建对象字节输入流管道包装低级的字节输入流管道
ObjectInputStream is = new ObjectInputStream(new FileInputStream("io-app2/src/obj.txt"));

// 2、调用对象字节输入流的反序列化方法
Student s = (Student) is.readObject();

System.out.println(s);
```



## 打印流

- **作用：打印流可以实现方便、高效的打印数据到文件中去。**打印流一般是指：PrintStream，PrintWriter两个类。
- 可以实现打印什么数据就是什么数据，例如打印整数97写出去就是97，打印boolean的true，写出去就是true。
- PrintStream和PrintWriter的区别
  **打印数据功能上是一模一样的**，都是使用方便，性能高效（核心优势）
  PrintStream继承自字节输出流OutputStream，支持写**字节数据**的方法。
  PrintWriter继承自字符输出流Writer，支持写**字符数据**出去。

![image-20220402211956095](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220402211956095.png)

![image-20220402212106315](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220402212106315.png)

![image-20220402212355285](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220402212355285.png)

```Java
 // 1、创建一个打印流对象
//        PrintStream ps = new PrintStream(new FileOutputStream("io-app2/src/ps.txt"));
//        PrintStream ps = new PrintStream(new FileOutputStream("io-app2/src/ps.txt" , true)); // 追加数据，在低级管道后面加True
//        PrintStream ps = new PrintStream("io-app2/src/ps.txt" );
        PrintWriter ps = new PrintWriter("io-app2/src/ps.txt"); // 打印功能上与PrintStream的使用没有区别

        ps.println(97);
        ps.println('a');
        ps.println(23.3);
        ps.println(true);
        ps.println("我是打印流输出的，我是啥就打印啥");

        ps.close();
```



### 输出语句重定向

属于打印流的一种应用，可以把输出语句的打印位置改到文件。

```Java
System.out.println("锦瑟无端五十弦");
System.out.println("一弦一柱思华年");//会打印到屏幕

// 改变输出语句的位置（重定向）
PrintStream ps = new PrintStream("io-app2/src/log.txt");
System.setOut(ps); // 把系统打印流改成我们自己的打印流

System.out.println("庄生晓梦迷蝴蝶");//会打印到文件中
System.out.println("望帝春心托杜鹃");
```



## Properties

- 其实就是一个Map集合，但是我们一般不会当集合使用，因为HashMap更好用。

- Properties代表的是一个属性文件，可以**把自己对象中的键值对信息存入到一个属性文件中去**。

  属性文件：后缀是.properties结尾的文件,里面的内容都是 key=value，后续做系统配置信息的。

![image-20220402213041452](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220402213041452.png)

![image-20220402213208305](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220402213208305.png)

```Java
// 需求：使用Properties把键值对信息存入到属性文件中去。
Properties properties = new Properties();
properties.setProperty("admin", "123456");
properties.setProperty("dlei", "003197");
properties.setProperty("heima", "itcast");
System.out.println(properties);

/**
   参数一：保存管道 字符输出流管道
   参数二：保存心得（随便写）
 */
properties.store(new FileWriter("io-app2/src/users.properties"), "乱写");

// 需求：Properties读取属性文件中的键值对信息。（读取）
        Properties properties = new Properties();
        System.out.println(properties);

        // 加载属性文件中的键值对数据到属性对象properties中去
        properties.load(new FileReader("io-app2/src/users.properties"));

        System.out.println(properties);
        String rs = properties.getProperty("dlei");
        System.out.println(rs);
        String rs1 = properties.getProperty("admin");
        System.out.println(rs1);
```



## IO框架：commons-io

- commons-io是apache开源基金组织提供的一组有关IO操作的类库，可以提高IO功能开发的效率。
- commons-io工具包提供了很多有关io操作的类。有两个主要的类FileUtils, IOUtils
- 利用common-io几乎可以完成所有的io流操作，非常牛

![image-20220402213831175](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220402213831175.png)

![image-20220402213855733](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220402213855733.png)





# 多线程

- 线程(thread)是一个程序内部的一条执行路径。
- 我们之前启动程序执行后，main方法的执行其实就是一条单独的执行路径。



## 多线程的创建

![image-20220403210111407](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220403210111407.png)

### 1.继承Thread类

- Java是通过java.lang.Thread 类来代表线程的。 
- 按照面向对象的思想，Thread类应该提供了实现多线程的方式。

![image-20220403202733276](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220403202733276.png)

```Java
public static void main(String[] args) {
        // 3、new一个新线程对象
        Thread t = new MyThread();
        // 4、调用start方法启动线程（执行的还是run方法）
        t.start();

        for (int i = 0; i < 5; i++) {
            System.out.println("主线程执行输出：" + i);
        }
    }
}
/**
   1、定义一个线程类继承Thread类
 */
class MyThread extends Thread{
    /**
       2、重写run方法，里面是定义线程以后要干啥
     */
    @Override
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("子线程执行输出：" + i);
        }
    }
```

**1、为什么不直接调用了run方法，而是调用start启动线程。**

- 直接调用run方法会当成普通方法执行，此时相当于还是单线程执行。
- 只有调用start方法才是启动一个新的线程执行。

**2、把主线程任务放在子线程之前会发生什么？**

- 这样主线程一直是先跑完的，相当于是一个单线程的效果了。



### 2.实现Runnable接口

![image-20220403203408649](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220403203408649.png)

![image-20220403203501478](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220403203501478.png)

```Java
 public static void main(String[] args) {
        // 3、创建一个任务对象
        Runnable target = new MyRunnable();
        // 4、把任务对象交给Thread处理
        Thread t = new Thread(target);
        // Thread t = new Thread(target, "1号");
        // 5、启动线程
        t.start();

        for (int i = 0; i < 10; i++) {
            System.out.println("主线程执行输出：" + i);
        }
    }
}
/**
   1、定义一个线程任务类 实现Runnable接口
 */
class MyRunnable  implements Runnable {
    /**
       2、重写run方法，定义线程的执行任务的
     */
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println("子线程执行输出：" + i);
        }
    }
     
//Runable是函数式接口，表达式可用lambda简化
//		1、2、3、4、5步骤可简化为
//     new Thread(() -> {
//                for (int i = 0; i < 10; i++) {
//                    System.out.println("子线程3执行输出：" + i);}
//        }).start();
     
```



### 3.实现Callable接口

**1、前2种线程创建方式都存在一个问题：**

- 他们重写的run方法均不能直接返回结果。不适合需要返回线程执行结果的业务场景。

**2、怎么解决这个问题呢？**

- JDK 5.0提供了Callable和FutureTask来实现。
- 这种方式的优点是：可以得到线程执行的结果。

![image-20220403205120925](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220403205120925.png)

![image-20220403205435284](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220403205435284.png)

```Java
 // 3、创建Callable任务对象
        Callable<String> call = new MyCallable(100);
        // 4、把Callable任务对象 交给 FutureTask 对象
        //  FutureTask对象的作用1： 是Runnable的对象（实现了Runnable接口），可以交给Thread了
        //  FutureTask对象的作用2： 可以在线程执行完毕之后通过调用其get方法得到线程执行完成的结果
        FutureTask<String> f1 = new FutureTask<>(call);
        // 5、交给线程处理
        Thread t1 = new Thread(f1);
        // 6、启动线程
        t1.start();

        Callable<String> call2 = new MyCallable(200);
        FutureTask<String> f2 = new FutureTask<>(call2);
        Thread t2 = new Thread(f2);
        t2.start();

        try {
            // 如果f1任务没有执行完毕，这里的代码会等待，直到线程1跑完才提取结果（get()方法的特性）。
            String rs1 = f1.get();
            System.out.println("第一个结果：" + rs1);
        } catch (Exception e) {
            e.printStackTrace();
        }

        try {
            // 如果f2任务没有执行完毕，这里的代码会等待，直到线程2跑完才提取结果。
            String rs2 = f2.get();
            System.out.println("第二个结果：" + rs2);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

/**
    1、定义一个任务类 实现Callable接口  应该申明线程任务执行完毕后的结果的数据类型
 */
class MyCallable implements Callable<String>{
    private int n;
    public MyCallable(int n) {     //构造器
        this.n = n;
    }

    /**
       2、重写call方法（任务方法）
     */
    @Override
    public String call() throws Exception {   //定义返回值类型
        int sum = 0;
        for (int i = 1; i <= n ; i++) {
            sum += i;
        }
        return "子线程执行的结果是：" + sum;
    }
```



## Thread常用API

![image-20220404160715849](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220404160715849.png)

![image-20220404161034391](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220404161034391.png)



## 线程安全

- 多个线程同时操作同一个共享资源的时候可能会出现业务安全问题，称为线程安全问题。
- 线程安全问题出现的原因：存在多线程并发、同时访问共享资源、存在修改共享资源

![image-20220404161337111](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220404161337111.png)



## 线程同步

- 为了解决线程安全问题。
- **核心思想：**加锁，把共享资源进行上锁，每次只能一个线程进入访问完毕以后解锁，然后其他线程才能进来。



### 加锁方式一：同步代码块

- 作用：把出现线程安全问题的核心代码给上锁。
- 原理：每次只能一个线程进入，执行完毕后自动解锁，其他线程才可以进来执行。
- 锁对象要求：理论上，**锁对象只要对于当前同时执行的线程来说是同一个对象即可**。（锁住当前对象，不让当前对象反复访问）

```Java
//格式
synchronized(同步锁对象) {
	操作共享资源的代码(核心代码)
}
```

- 锁对象用任意唯一的对象不好，会影响其他无关线程的执行。
- 规范上：建议使用共享资源作为锁对象。
- 对于**实例方法**建议使用**this**作为锁对象。
- 对于**静态方法**建议使用**字节码（类名.class）**对象作为锁对象。

```Java
/**
  小明 小红
 */
public void drawMoney(double money) {
    // 1、拿到是谁来取钱
    String name = Thread.currentThread().getName();
    // 同步代码块
    // 小明 小红
    // this == acc 共享账户
    synchronized (this) {
        // 2、判断余额是否足够
        if(this.money >= money){
            // 钱够了
            System.out.println(name+"来取钱，吐出：" + money);
            // 更新余额
            this.money -= money;
            System.out.println(name+"取钱后，余额剩余：" + this.money);
        }else{
            // 3、余额不足
            System.out.println(name+"来取钱，余额不足！");
        }
    }
}
```



### 加锁方式二：同步方法

- 作用：把出现线程安全问题的核心方法给上锁。
- 原理：每次只能一个线程进入，执行完毕以后自动解锁，其他线程才可以进来执行。

```Java
//格式
修饰符 synchronized 返回值类型 方法名称(形参列表) {
	操作共享资源的代码
}
```

**同步方法底层原理：**

- 同步方法其实底层也是有隐式锁对象的，只是**锁的范围是整个方法代码**。
- 如果方法是**实例方法**：同步方法默认用**this**作为的锁对象。但是代码要高度面向对象！
- 如果方法是**静态方法**：同步方法默认用**类名.class**作为的锁对象。

```Java
/**
  小明 小红
   this == acc
 */
public synchronized void drawMoney(double money) {
    // 1、拿到是谁来取钱
    String name = Thread.currentThread().getName();
    // 2、判断余额是否足够
    // 小明  小红
    if(this.money >= money){
        // 钱够了
        System.out.println(name+"来取钱，吐出：" + money);
        // 更新余额
        this.money -= money;
        System.out.println(name+"取钱后，余额剩余：" + this.money);
    }else{
        // 3、余额不足
        System.out.println(name+"来取钱，余额不足！");
    }
}
```



### 加锁方式三：Lock锁

- 为了更清晰的表达如何加锁和释放锁，JDK5以后提供了一个新的锁对象Lock，**更加灵活、方便**。
- Lock实现提供比使用synchronized方法和语句可以获得更广泛的锁定操作。
- **Lock是接口**不能直接实例化，这里采用它的实现类ReentrantLock来构建Lock锁对象。
- ![image-20220404164013842](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220404164013842.png)

```Java
// final修饰后：锁对象是唯一和不可替换的，非常专业
private final Lock lock = new ReentrantLock();

 /**
      小明 小红
     */
    public void drawMoney(double money) {
        // 1、拿到是谁来取钱
        String name = Thread.currentThread().getName();
        // 2、判断余额是否足够
        // 小明  小红
        lock.lock(); // 上锁
        try {
            if(this.money >= money){
                // 钱够了
                System.out.println(name+"来取钱，吐出：" + money);
                // 更新余额
                this.money -= money;
                System.out.println(name+"取钱后，余额剩余：" + this.money);
            }else{
                // 3、余额不足
                System.out.println(name+"来取钱，余额不足！");
            }
        } finally {
            lock.unlock(); // 解锁
        }
    }
```



## 线程通信

![image-20220404164354053](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220404164354053.png)

![image-20220404164431687](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220404164431687.png)

```Java
// 小红 小明
public synchronized void drawMoney(double money) {
    try {
        String name = Thread.currentThread().getName();
        if(this.money >= money){
            // 有钱，取钱
            this.money -= money;
            System.out.println(name+"来取钱"+ money +"成功，取钱后余额剩余：" + this.money);
            // 取钱后  唤醒别人等待自己
            this.notify(); // 唤醒别人：干爹
            this.wait(); // 等待了当前取钱线程：小红
        }else{
            // 没钱，唤醒别人等待自己
            this.notify();
            this.wait();
        }
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
}

// 干爹
public synchronized void saveMoney(double money) {
    try {
        String name = Thread.currentThread().getName();
        if(this.money > 0){
            // 有钱，不存钱
            // 唤醒别人等待自己
            this.notify(); // 唤醒别人：小红
            this.wait(); // 等待了当前取钱线程：干爹
        }else{
            // 没钱，存钱
            this.money += money;
            System.out.println(name +"来存钱，存钱后余额是：" + this.money);
            // 存钱后有钱：唤醒别人等待自己
            this.notify();
            this.wait();
        }
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
}
```



## 线程池

- 线程池就是一个可以复用线程的技术。
- **不使用线程池的问题**：如果用户每发起一个请求，后台就创建一个新线程来处理，下次新任务来了又要创建新线程，而创建新线程的开销是很大的，这样会严重影响系统的性能。

<img src="C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220404165251822.png" alt="image-20220404165251822" style="zoom:50%;" />



### 手动创建线程池

![image-20220404165739007](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220404165739007.png)

![image-20220404165547876](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220404165547876.png)

![image-20220404173510809](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220404173510809.png)

- **1.谁代表线程池？**

  ExecutorService接口

- **2.临时线程什么时候创建？**

  新任务提交时发现核心线程都在忙，任务队列也满了，并且还可以创建临时线程，此时才会创建临时线程。

- **3.什么时候会开始拒绝任务？**

  核心线程和临时线程都在忙，任务队列也满了，新的任务过来的时候才会开始任务拒绝。



### 线程池处理Runnable任务

```Java
//ThreadPoolExecutor创建线程池对象示例
ExecutorService pools = new ThreadPoolExecutor(3, 5, 8 , TimeUnit.SECONDS, new ArrayBlockingQueue<>(6),
Executors.defaultThreadFactory() , new ThreadPoolExecutor.AbortPolicy());
```

![image-20220404170643403](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220404170643403.png)

```Java
  // 1、创建线程池对象
        ExecutorService pool = new ThreadPoolExecutor(3, 5 ,
                6, TimeUnit.SECONDS, new ArrayBlockingQueue<>(5) , Executors.defaultThreadFactory(),
               new ThreadPoolExecutor.AbortPolicy() );

        // 2、给任务线程池处理。
        Runnable target = new MyRunnable();
        pool.execute(target);
        pool.execute(target);
        pool.execute(target);

        pool.execute(target);
        pool.execute(target);
        pool.execute(target);
        pool.execute(target);
        pool.execute(target);

        // 创建临时线程
        pool.execute(target);
        pool.execute(target);
//        // 不创建，拒绝策略被触发！！！
//        pool.execute(target);

        // 关闭线程池（开发中一般不会使用）。
        // pool.shutdownNow(); // 立即关闭，即使任务没有完成，会丢失任务的！
        pool.shutdown(); // 会等待全部任务执行完毕之后再关闭（建议使用的）
    }
```



### 线程池处理Callable任务

![image-20220404173613303](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220404173613303.png)

```Java
  // 1、创建线程池对象
        ExecutorService pool = new ThreadPoolExecutor(3, 5 ,
                6, TimeUnit.SECONDS, new ArrayBlockingQueue<>(5) , Executors.defaultThreadFactory(),
               new ThreadPoolExecutor.AbortPolicy() );

        // 2、给任务线程池处理。
        Future<String> f1 = pool.submit(new MyCallable(100));
        Future<String> f2 = pool.submit(new MyCallable(200));
        Future<String> f3 = pool.submit(new MyCallable(300));
        Future<String> f4 = pool.submit(new MyCallable(400));
        Future<String> f5 = pool.submit(new MyCallable(500));

//        String rs = f1.get();
//        System.out.println(rs);

        System.out.println(f1.get());
        System.out.println(f2.get());
        System.out.println(f3.get());
        System.out.println(f4.get());
        System.out.println(f5.get());
    }
```



### Executors工具类实现线程池

![image-20220404173916185](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220404173916185.png)

```Java
  // 1、创建固定线程数据的线程池
    ExecutorService pool = Executors.newFixedThreadPool(3);

    pool.execute(new MyRunnable());
    pool.execute(new MyRunnable());
    pool.execute(new MyRunnable());
    pool.execute(new MyRunnable()); // 已经没有多余线程了
}
```

![图片1](C:\Users\xad Talent\Desktop\图片1.png)



## 定时器

- 定时器是一种控制任务延时调用，或者周期调用的技术。
- 作用：闹钟、定时邮件发送。

![image-20220409150327237](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220409150327237.png)

```JAVA
  // 1、创建Timer定时器
        Timer timer = new Timer();  // 定时器本身就是一个单线程。
        // 2、调用方法，处理定时任务
        timer.schedule(new TimerTask() {
            @Override
            public void run() {
                System.out.println(Thread.currentThread().getName() + "执行AAA~~~" + new Date());
//                try {
//                    Thread.sleep(5000);
//                } catch (InterruptedException e) {
//                    e.printStackTrace();
//                }
            }
        }, 0, 2000);

        timer.schedule(new TimerTask() {
            @Override
            public void run() {
                System.out.println(Thread.currentThread().getName() + "执行BB~~~"+ new Date());
                System.out.println(10/0);
            }
        }, 0, 2000);

        timer.schedule(new TimerTask() {
            @Override
            public void run() {
                System.out.println(Thread.currentThread().getName() + "执行CCC~~~"+ new Date());
            }
        }, 0, 3000);
    }
```

![image-20220409150406539](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220409150406539.png)

```java
 // 1、创建ScheduledExecutorService线程池，做定时器
    ScheduledExecutorService pool = Executors.newScheduledThreadPool(3);

    // 2、开启定时任务
    pool.scheduleAtFixedRate(new TimerTask() {
        @Override
        public void run() {
            System.out.println(Thread.currentThread().getName() + "执行输出：AAA  ==》 " + new Date());
            try {
                Thread.sleep(100000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }, 0, 2, TimeUnit.SECONDS);


    pool.scheduleAtFixedRate(new TimerTask() {
        @Override
        public void run() {
            System.out.println(Thread.currentThread().getName() + "执行输出：BBB  ==》 " + new Date());
            System.out.println(10 / 0);
        }
    }, 0, 2, TimeUnit.SECONDS);


    pool.scheduleAtFixedRate(new TimerTask() {
        @Override
        public void run() {
            System.out.println(Thread.currentThread().getName() + "执行输出：CCC  ==》 " + new Date());
        }
    }, 0, 2, TimeUnit.SECONDS);

}
```



# 网络编程

此节代码过多，如有API不会使用，打开黑马Java网络编程文件夹里的代码进行学习

常见的通信模式有如下2种形式：Client-Server(CS) 、 Browser/Server(BS) 

<img src="C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220409151341406.png" alt="image-20220409151341406" style="zoom:50%;" />



<img src="C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220409151416652.png" alt="image-20220409151416652" style="zoom:50%;" />

## 实现网络编程关键的三要素

- IP地址：设备在网络中的地址，是唯一的标识。
- 端口：应用程序在设备中唯一的标识。
- 协议:   数据在网络中传输的规则，常见的协议有UDP协议和TCP协议。

### IP

```
IP常用命令：
ipconfig：查看本机IP地址
ping IP地址：检查网络是否连通

特殊IP地址：
本机IP: 127.0.0.1或者localhost：称为回送地址也可称本地回环地址，只会寻找当前所在本机。
```

![image-20220409151939589](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220409151939589.png)

### 端口号

![image-20220409152424906](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220409152424906.png)



### 通信协议

![image-20220409152532640](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220409152532640.png)



## UDP通信

- UDP是一种无连接、不可靠传输的协议。
- 将数据源IP、目的地IP和端口以及数据封装成数据包，大小限制在64KB内，直接发送出去即可。

![image-20220409153016533](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220409153016533.png)

![image-20220409153041064](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220409153041064.png)

![image-20220409153110734](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220409153110734.png)

```Java
// 1、创建发送端对象：发送端自带默认的端口号（人）
DatagramSocket socket = new DatagramSocket(6666);

// 2、创建一个数据包对象封装数据（韭菜盘子）
/**
 public DatagramPacket(byte buf[], int length,
 InetAddress address, int port)
 参数一：封装要发送的数据（韭菜）
 参数二：发送数据的大小
 参数三：服务端的主机IP地址
 参数四：服务端的端口
 */
byte[] buffer = "我是一颗快乐的韭菜，你愿意吃吗？".getBytes();
DatagramPacket packet = new DatagramPacket( buffer, buffer.length,
        InetAddress.getLocalHost() , 8888);

// 3、发送数据出去
socket.send(packet);

socket.close();

//需要发送数据的时候，DatagramSocket指定自己的端口号，DatagramPacket指定对方的端口号。需要接收数据的时候，必须指定和上面发送端的DatagramPacket一致的端口号，而用来接收数据的DatagramPacket不需要指定端口号。
```

![image-20220409153203592](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220409153203592.png)

```Java
// 1、创建接收端对象：注册端口（人）
DatagramSocket socket = new DatagramSocket(8888);

// 2、创建一个数据包对象接收数据（韭菜盘子）
byte[] buffer = new byte[1024 * 64];
DatagramPacket packet = new DatagramPacket(buffer, buffer.length);

// 3、等待接收数据。
socket.receive(packet);

// 4、取出数据即可
// 读取多少倒出多少
int len = packet.getLength();
String rs = new String(buffer,0, len);
System.out.println("收到了：" + rs);

// 获取发送端的ip和端口
String ip  =packet.getSocketAddress().toString();
System.out.println("对方地址：" + ip);

int port  = packet.getPort();
System.out.println("对方端口：" + port);

socket.close();
```



![image-20220409153905152](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220409153905152.png)

![image-20220409153919560](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220409153919560.png)

具体方法去看代码，我是觉得这一段讲的很培训班，没兴趣学



## TCP通信

- 客户端怎么发，服务端就应该怎么收。
- 客户端如果没有消息，服务端会进入阻塞等待。
- Socket一方关闭或者出现异常、对方Socket也会失效或者出错。

![image-20220409154110623](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220409154110623.png)

![image-20220409154439816](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220409154439816.png)

**客户端实现步骤：**

1. 创建客户端的Socket对象，请求与服务端的连接。
2. 使用socket对象调用getOutputStream()方法得到字节输出流。
3. 使用字节输出流完成数据的发送。
4. 释放资源：关闭socket管道。

```Java
try {
    System.out.println("====客户端启动===");
    // 1、创建Socket通信管道请求有服务端的连接
    // public Socket(String host, int port)
    // 参数一：服务端的IP地址
    // 参数二：服务端的端口
    Socket socket = new Socket("127.0.0.1", 7777);

    // 2、从socket通信管道中得到一个字节输出流 负责发送数据
    OutputStream os = socket.getOutputStream();

    // 3、把低级的字节流包装成打印流
    PrintStream ps = new PrintStream(os);

    // 4、发送消息
    ps.println("我是TCP的客户端，我已经与你对接，并发出邀请：约吗？");
    ps.flush();

    // 关闭资源。不能关，会出bug，线程结束了自己会关
    // socket.close();

} catch (Exception e) {
    e.printStackTrace();
}
```

![image-20220409194902194](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220409194902194.png)**服务端实现步骤：**

1. 创建ServerSocket对象，注册服务端端口。
2. 调用ServerSocket对象的accept()方法，等待客户端的连接，并得到Socket管道对象。
3. 通过Socket对象调用getInputStream()方法得到字节输入流、完成数据的接收。
4. 释放资源：关闭socket管道

```Java
try {
    System.out.println("===服务端启动成功===");
    // 1、注册端口
    ServerSocket serverSocket = new ServerSocket(7777);
    // 2、必须调用accept方法：等待接收客户端的Socket连接请求，建立Socket通信管道
    Socket socket = serverSocket.accept();
    // 3、从socket通信管道中得到一个字节输入流
    InputStream is = socket.getInputStream();
    // 4、把字节输入流包装成缓冲字符输入流进行消息的接收
    BufferedReader br = new BufferedReader(new InputStreamReader(is));
    // 5、按照行读取消息
    String msg;
    if ((msg = br.readLine()) != null){
        System.out.println(socket.getRemoteSocketAddress() + "说了：: " + msg);
    }
} catch (Exception e) {
    e.printStackTrace();
}
```

以下内容看ppt和代码，我觉得我暂时用不上

![image-20220409195358775](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220409195358775.png)





# 重要的技术



## 单元测试-Junit单元测试框架

- 单元测试就是针对最小的功能单元编写测试代码，Java程序最小的功能单元是方法，因此，单元测试就是针对Java方法的测试，进而检查方法的正确性。

- JUnit是使用Java语言实现的单元测试框架，它是开源的，Java开发者都应当学习并使用JUnit编写单元测试。
- 此外，几乎所有的IDE工具都集成了JUnit，这样我们就可以直接在IDE中编写并运行JUnit测试，JUnit目前最新版本是5。

- **JUnit优点：**

  JUnit可以灵活的选择执行哪些测试方法，可以一键执行全部测试方法。
   Junit可以生成全部方法的测试报告。
   单元测试中的某个方法测试失败了，不会影响其他测试方法的测试。

- 测试某个方法直接右键该方法启动测试。测试全部方法，可以选择类或者模块启动。

![image-20220410160814528](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220410160814528.png)

```Java
/**
   测试方法
   注意点：
        1、必须是公开的，无参数 无返回值的方法
        2、测试方法必须使用@Test注解标记。
 */
@Test   
public void testLoginName(){
    UserService userService = new UserService();
    String rs = userService.loginName("admin","123456");

    // 进行预期结果的正确性测试：断言。
    Assert.assertEquals("您的登录业务可能出现问题", "登录成功", rs );////第一个参数是期望值，第二个参数，实际值
}

@Test
public void testSelectNames(){
    UserService userService = new UserService();
    userService.selectNames();
} //直接进行测试，看代码能不能正常运行
```

![image-20220410162129040](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220410162129040.png)



## 反射

- 反射是指对于任何一个Class类，在"运行的时候"都可以直接得到这个类全部成分。
- 在运行时,可以直接得到这个类的构造器对象：Constructor
- 在运行时,可以直接得到这个类的成员变量对象：Field
- 在运行时,可以直接得到这个类的成员方法对象：Method
- 这种运行时动态获取类信息以及动态调用类中成分的能力称为Java语言的反射机制。

```Java
//反射的关键：
//反射的第一步都是先得到编译后的Class类对象，然后就可以得到Class的全部成分。
HelloWorld.java -> javac -> HelloWorld.class
Class c = HelloWorld.class;
```

- 反射是**在运行时**获取类的字节码文件对象：然后可以**解析类中的全部成分**。
- 反射的**核心思想和关键**就是:得到编译以后的class文件对象。



### 获取Class类的对象

Class是一个特殊的类，和定义类时写的修饰符class不同

![image-20220410164159715](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220410164159715.png)

```Java
//三种方法
// 1、Class类中的一个静态方法：forName(全类名：包名 + 类名)
Class c = Class.forName("com.itheima.d2_reflect_class.Student");
System.out.println(c); // Student.class

// 2、类名.class
Class c1 = Student.class;
System.out.println(c1);

// 3、对象.getClass() 获取对象对应类的Class对象。
Student s = new Student();
Class c2 = s.getClass();
System.out.println(c2);
```



### 获取构造器对象

第一步：获得class对象	第二步：获得Constructor对象	第三步：创建对象

![image-20220410164451882](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220410164451882.png)

```Java
public class Student {
    private String name;
    private int age;

    private Student(){
        System.out.println("无参数构造器执行！");
    }

    public Student(String name, int age) {
        System.out.println("有参数构造器执行！");
        this.name = name;
        this.age = age;
    }
}

public class TestStudent01 {
    // 1. getConstructors:
    // 获取全部的构造器：只能获取public修饰的构造器。
    // Constructor[] getConstructors()
    @Test
    public void getConstructors(){
        // a.第一步：获取类对象
        Class c = Student.class;
        // b.提取类中的全部的构造器对象(这里只能拿public修饰)
        Constructor[] constructors = c.getConstructors();
        // c.遍历构造器
        for (Constructor constructor : constructors) {
            System.out.println(constructor.getName() + "===>" + constructor.getParameterCount());
        }
    }

    // 2.getDeclaredConstructors():
    // 获取全部的构造器：只要你敢写，这里就能拿到，无所谓权限是否可及。
    @Test
    public void getDeclaredConstructors(){
        // a.第一步：获取类对象
        Class c = Student.class;
        // b.提取类中的全部的构造器对象
        Constructor[] constructors = c.getDeclaredConstructors();
        // c.遍历构造器
        for (Constructor constructor : constructors) {
            System.out.println(constructor.getName() + "===>" + constructor.getParameterCount());
        }
    }

    // 3.getConstructor(Class... parameterTypes)
    // 获取某个构造器：只能拿public修饰的某个构造器
    @Test
    public void getConstructor() throws Exception {
        // a.第一步：获取类对象
        Class c = Student.class;
        // b.定位单个构造器对象 (按照参数定位无参数构造器 只能拿public修饰的某个构造器)
        Constructor cons = c.getConstructor();
        System.out.println(cons.getName() + "===>" + cons.getParameterCount());
    }

    // 4.getConstructor(Class... parameterTypes)
    // 获取某个构造器：只要你敢写，这里就能拿到，无所谓权限是否可及。
    @Test
    public void getDeclaredConstructor() throws Exception {
        // a.第一步：获取类对象
        Class c = Student.class;
        // b.定位单个构造器对象 (按照参数定位无参数构造器)
        Constructor cons = c.getDeclaredConstructor();
        System.out.println(cons.getName() + "===>" + cons.getParameterCount());

        // c.定位某个有参构造器
        Constructor cons1 = c.getDeclaredConstructor(String.class, int.class);
        System.out.println(cons1.getName() + "===>" + cons1.getParameterCount());
    }
}
```

![image-20220410165840069](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220410165840069.png)

```Java
// 1.调用构造器得到一个类的对象返回。
@Test
public void getDeclaredConstructor() throws Exception {
    // a.第一步：获取类对象
    Class c = Student.class;
    // b.定位单个构造器对象 (按照参数定位无参数构造器)
    Constructor cons = c.getDeclaredConstructor();
    System.out.println(cons.getName() + "===>" + cons.getParameterCount());

    // 如果遇到了私有的构造器，可以暴力反射
    cons.setAccessible(true); // 权限被打开

    Student s = (Student) cons.newInstance();
    System.out.println(s);

    System.out.println("-------------------");

    // c.定位某个有参构造器
    Constructor cons1 = c.getDeclaredConstructor(String.class, int.class);
    System.out.println(cons1.getName() + "===>" + cons1.getParameterCount());

    Student s1 = (Student) cons1.newInstance("孙悟空", 1000);
    System.out.println(s1);
}
```



### 获取成员变量对象

![image-20220410171025127](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220410171025127.png)

```Java
/**
 * 1.获取全部的成员变量。
 * Field[] getDeclaredFields();
 *  获得所有的成员变量对应的Field对象，只要申明了就可以得到
 */
@Test
public void getDeclaredFields(){
    // a.定位Class对象
    Class c = Student.class;
    // b.定位全部成员变量
    Field[] fields = c.getDeclaredFields();
    // c.遍历一下
    for (Field field : fields) {
        System.out.println(field.getName() + "==>" + field.getType());
    }
}

/**
    2.获取某个成员变量对象 Field getDeclaredField(String name);
 */
@Test
public void getDeclaredField() throws Exception {
    // a.定位Class对象
    Class c = Student.class;
    // b.根据名称定位某个成员变量
    Field f = c.getDeclaredField("age");
    System.out.println(f.getName() +"===>" + f.getType());
}
```

![image-20220410171239502](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220410171239502.png)

```Java
@Test
public void setField() throws Exception {
    // a.反射第一步，获取类对象
    Class c = Student.class;
    // b.提取某个成员变量
    Field ageF = c.getDeclaredField("age");

    ageF.setAccessible(true); // 暴力打开权限

    // c.赋值
    Student s = new Student();
    ageF.set(s , 18);  // s.setAge(18);
    System.out.println(s);

    // d、取值
    int age = (int) ageF.get(s);
    System.out.println(age);
}
```



### 获取方法对象

![image-20220410171620746](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220410171620746.png)![image-20220410172344239](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220410172344239.png)

```Java
public class Dog {
    private String name ;
    public Dog(){}

    public Dog(String name) {
        this.name = name;
    }
    public void run(){
        System.out.println("狗跑的贼快~~");
    }
    private void eat(){
        System.out.println("狗吃骨头");
    }
    private String eat(String name){
        System.out.println("狗吃" + name);
        return "吃的很开心！";
    }
    public static void inAddr(){
        System.out.println("在黑马学习Java!");
    }
}
/**
 * 1.获得类中的所有成员方法对象
 */
@Test
public void getDeclaredMethods(){
    // a.获取类对象
    Class c = Dog.class;
    // b.提取全部方法；包括私有的
    Method[] methods = c.getDeclaredMethods();
    // c.遍历全部方法
    for (Method method : methods) {
        System.out.println(method.getName() +" 返回值类型：" + method.getReturnType() + " 参数个数：" + method.getParameterCount());
    }
}

/**
 * 2. 获取某个方法对象
 */
@Test
public void getDeclardMethod() throws Exception {
    // a.获取类对象
    Class c = Dog.class;
    // b.提取单个方法对象
    Method m = c.getDeclaredMethod("eat");
    Method m2 = c.getDeclaredMethod("eat", String.class);

    // 暴力打开权限了
    m.setAccessible(true);
    m2.setAccessible(true);

    // c.触发方法的执行
    Dog d = new Dog();
    // 注意：方法如果是没有结果回来的，那么返回的是null.
    Object result = m.invoke(d);
    System.out.println(result);

    Object result2 = m2.invoke(d, "骨头");
    System.out.println(result2);
}
```



### 反射的作用

#### 绕过编译阶段为集合添加数据

![image-20220410172510233](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220410172510233.png)



#### 通用框架的底层原理

![image-20220410172801995](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220410172801995.png)



## 注解

- Java 注解（Annotation）又称 Java 标注，是 JDK5.0 引入的一种注释机制。
- Java 语言中的类、构造器、方法、成员变量、参数等都可以被注解进行标注。
- 作用：对Java中类、方法、成员变量做标记，然后进行特殊处理，至于到底做何种处理由业务需求来决定。
  例如：JUnit框架中，标记了注解@Test的方法就可以被当成测试方法执行，而没有标记的就不能当成测试方法执行。

![image-20220410173045898](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220410173045898.png)



### 自定义注解

```Java
//格式
public @interface 注解名称 {
	public 属性类型 属性名() default 默认值 ;
}
```

```Java
public @interface MyBook {
    String name();
    String[] authors();
    double price();
}

@MyBook(name="《精通JavaSE1》",authors = {"黑马", "dlei"} , price = 199.5)
    public static void main(String[] args) {
        @MyBook(name="《精通JavaSE2》",authors = {"黑马", "dlei"} , price = 199.5)
        int age = 21;
    }
```



### 元注解

- 元注解：就是注解注解的注解
- 元注解有两个：
   @Target: 约束自定义注解只能在哪些地方使用
   @Retention：申明注解的生命周期

![image-20220410174120630](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220410174120630.png)

```Java
@Target({ElementType.TYPE,ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
public @interface Bookk {
    String value();
    double price() default 100;
    String[] author();
}
```



### 注解解析

注解的操作中经常需要进行解析，注解的解析就是判断是否存在注解，存在注解就解析出内容。

![image-20220410174506332](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220410174506332.png)

**解析注解的技巧：**

1. 注解在哪个成分上，我们就先拿哪个成分对象。
2.  比如注解作用成员方法，则要获得该成员方法对应的Method对象，再来拿上面的注解
3.  比如注解作用在类上，则要该类的Class对象，再来拿上面的注解
4.  比如注解作用在成员变量上，则要获得该成员变量对应的Field对象，再来拿上面的注解

```Java
public class AnnotationDemo3 {
    @Test
    public void parseClass(){
        // a.先得到类对象
        Class c = BookStore.class;
        // b.判断这个类上面是否存在这个注解
        if(c.isAnnotationPresent(Bookk.class)){
            //c.直接获取该注解对象
            Bookk book = (Bookk) c.getDeclaredAnnotation(Bookk.class);
            System.out.println(book.value());
            System.out.println(book.price());
            System.out.println(Arrays.toString(book.author()));
        }
    }

    @Test
    public void parseMethod() throws NoSuchMethodException {
        // a.先得到类对象
        Class c = BookStore.class;

        Method m = c.getDeclaredMethod("test");

        // b.判断这个类上面是否存在这个注解
        if(m.isAnnotationPresent(Bookk.class)){
            //c.直接获取该注解对象
            Bookk book = (Bookk) m.getDeclaredAnnotation(Bookk.class);
            System.out.println(book.value());
            System.out.println(book.price());
            System.out.println(Arrays.toString(book.author()));
        }
    }
}

@Bookk(value = "《情深深雨濛濛》", price = 99.9, author = {"琼瑶", "dlei"})
class BookStore{

    @Bookk(value = "《三少爷的剑》", price = 399.9, author = {"古龙", "熊耀华"})
    public void test(){
    }
}
```



## 动态代理

代理就是被代理者没有能力或者不愿意去完成某件事情，需要找个人代替自己去完成这件事，动态代理就是用来对业务功能（方法）进行代理的。

**关键步骤**
  1.必须有接口，实现类要实现接口（代理通常是基于接口实现的）。
  2.创建一个实现类的对象，该对象为业务对象，紧接着为业务对象做一个代理对象。

![image-20220410192209612](C:\Users\xad Talent\AppData\Roaming\Typora\typora-user-images\image-20220410192209612.png)

```Java
//接口
public interface UserService {
    String login(String loginName , String passWord) ;
}

//实现类
public class UserServiceImpl implements UserService{
    @Override
    public String login(String loginName, String passWord)  {
        try {
            Thread.sleep(1000);
        } catch (Exception e) {
            e.printStackTrace();
        }
        if("admin".equals(loginName) && "1234".equals(passWord)) {
            return "success";
        }
        return "登录名和密码可能有毛病";
    }
}

//代理类
public class ProxyUtil {
    /**
      生成业务对象的代理对象。
     * @param obj
     * @return
     */
    public static <T> T  getProxy(T obj) {
        // 返回了一个代理对象了
/**
    public static Object newProxyInstance(ClassLoader loader,  Class<?>[] interfaces, InvocationHandler h)
    参数一：类加载器，负责加载代理类到内存中使用。
    参数二：获取被代理对象实现的全部接口。代理要为全部接口的全部方法进行代理
    参数三：代理的核心处理逻辑
 */        
        return (T)Proxy.newProxyInstance(obj.getClass().getClassLoader(),
                obj.getClass().getInterfaces(),
                new InvocationHandler() {
                    @Override
                    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                        // 参数一：代理对象本身。一般不管
                        // 参数二：正在被代理的方法
                        // 参数三：被代理方法，应该传入的参数
                       long startTimer = System .currentTimeMillis();
                        // 马上触发方法的真正执行。(触发真正的业务功能)
                        Object result = method.invoke(obj, args);

                        long endTimer = System.currentTimeMillis();
                        System.out.println(method.getName() + "方法耗时：" + (endTimer - startTimer) / 1000.0 + "s");

                        // 把业务功能方法执行的结果返回给调用者
                        return result;
                    }
                });
    }
}

//main方法
public class Test {
    public static void main(String[] args) {
        // 1、把业务对象，直接做成一个代理对象返回，代理对象的类型也是 UserService类型
        UserService userService = ProxyUtil.getProxy(new UserServiceImpl());
        System.out.println(userService.login("admin", "1234")); // 走代理
    }
}
```







































































































