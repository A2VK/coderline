# Basic Java Law
> 复习回顾 JAVA 基础知识 

### 语言特性 

- 面向对象
- 健壮性，安全性
- 解释性，动态性，可移植性(可以说为半编译，半解释型语言)
- 多线程...
- java虚拟机
- 垃圾收集GC
- 字节码文件
- 

### 基础语法 

##### 访问修饰符
- default (即缺省，什么也不写）: 在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法
- private : 在同一类内可见。使用对象：变量、方法。 注意：不能修饰类（外部类）
- public : 对所有类可见。使用对象：类、接口、变量、方法
- protected : 对同一包内的类和所有子类可见。使用对象：变量、方法。 注意：不能修饰类（外部类）

*修饰符作用域表：*

修饰符 | 本类 | 同包下 | 同包子类 | 异包子类 | 异包 
:---: | :-: | :-: | :-: | :-: | :-:
public | Y | Y | Y | Y | Y
protected | Y | Y | Y | Y/N(interface) | N
default| Y | Y | Y | N | N
private| Y | N | N | N | N

> 接口里的变量都隐式声明为 public static final,而接口里的方法默认情况下访问权限为 public

**继承访问权限：**
- 父类中声明为 public 的方法在子类中也必须为 public
- 父类中声明为 protected 的方法在子类中要么声明为 protected，要么声明为 public，不能声明为 private
- 父类中声明为 private 的方法，不能够被继承

**static 修饰符：**
   > 被 static 修饰的变量及代码片段 将被JVM 在启动时加载到静态存储区
   - 静态变量：
        > static 关键字用来声明独立于对象的静态变量，无论一个类实例化多少对象，它的静态变量只有一份拷贝。 静态变量也被称为类变量。局部变量不能被声明为 static 变量
   - 静态方法：
        > static 关键字用来声明独立于对象的静态方法。静态方法不能使用类的非静态变量。静态方法从参数列表得到数据，然后计算这些数据

**final 修饰符：**

   - final 变量
        > 变量一旦赋值后，不能被重新赋值 所以 被 final 修饰的实例变量必须显式指定初始值
    
   - final 方法
        > 声明 final 方法的主要目的是防止该方法的内容被修改
        > 类中的 final 方法可以被子类继承，但是不能被子类修改
    
   - final 类
        > final 类不能被继承

**abstract 修饰符：**
   - 抽象类
        - 抽象类不能用来实例化对象，声明抽象类的唯一目的是为了将来对该类进行扩充
        - 一个类不能同时被 abstract 和 final 修饰。如果一个类包含抽象方法，那么该类一定要声明为抽象类，否则将出现编译错误
        - 抽象类可以包含抽象方法和非抽象方法
         
   - 抽象方法
        - 抽象方法是一种没有任何实现的方法，该方法的的具体实现由子类提供
        - 抽象方法不能被声明成 final 和 static
        - 任何继承抽象类的子类必须实现父类的所有抽象方法，除非该子类也是抽象类
        - 如果一个类包含若干个抽象方法，那么该类必须声明为抽象类。抽象类可以不包含抽象方法
        - 抽象方法的声明以分号结尾：public abstract sample();

**transient 修饰符:**

**synchronized 修饰符:**
   > 线程安全修饰符 
    
**volatile 修饰符:**
   > volatile 修饰的变量发生变更时，JVM会强制更新此变量在内存共享区的值
   
<br>

##### 变量申明类型

- 被常量修饰时在运行时无法修改  final 修饰
- ** 变量类型: **
    ```java
    
  public class People {
        static int mark;  //类变量
        String name = "xiaoming"; //实例变量
        
        public String getName() {
          return this.name;   //局部变量
        }  
  }

    ```
    - 类变量：独立于方法之外的变量 static 修饰
    - 实例变量：独立于方法之外的变量 没有 static 修饰
    - 局部变量：类的方法中的变量
    <br/><br/>
 
- ** 类变量（静态变量）**
    ```java
    public class People {
        final static int MARK = 10000;
        static int identifier = 0;
  }
    
    ```
    - 类变量也称为静态变量，在类中以static关键字声明，但必须在方法构造方法和语句块之外
    - 无论一个类创建了多少个对象，类只拥有类变量的一份拷贝
    - 静态变量除了被声明为常量外很少使用。常量是指声明为public/private,final和static类型的变量。常量初始化后不可改变
    - 静态变量储存在静态存储区。经常被声明为常量，很少单独使用static声明变量
    - 静态变量在第一次被访问时创建，在程序结束时销毁
    - 与实例变量具有相似的可见性。但为了对类的使用者可见，大多数静态变量声明为public类型
    - 默认值和实例变量相似。数值型变量默认值是0，布尔型默认值是false，引用类型默认值是null。
        变量的值可以在声明的时候指定，也可以在构造方法中指定。此外，静态变量还可以在静态语句块中初始化
    - 静态变量可以通过：ClassName.VariableName的方式访问
    - 类变量被声明为public static final类型时，类变量名称一般建议使用大写字母。如果静态变量不是public和final类型，其命名方式与实例变量以及局部变量的命名方式一致
    <br/><br/>

- ** 实例变量 **
    ```java
        public class People {
              private String name; // 实例变量
              public String iCode;
              People(String name){
                this.name = name;
              }
              
          }
    ```
    - 实例变量声明在一个类中，但在方法、构造方法和语句块之外
    - 当一个对象被实例化之后，每个实例变量的值就跟着确定
    - 实例变量在对象创建的时候创建，在对象被销毁的时候销毁
    - 实例变量的值应该至少被一个方法、构造方法或者语句块引用，使得外部能够通过这些方式获取实例变量信息
    - 实例变量可以声明在使用前或者使用后
    - 访问修饰符可以修饰实例变量
    - 实例变量对于类中的方法、构造方法或者语句块是可见的 ** 一般情况下应该把实例变量设为私有 ** 通过使用访问修饰符可以使实例变量对子类可见
    - 实例变量具有默认值。数值型变量的默认值是0，布尔型变量的默认值是false，引用类型变量的默认值是null 变量的值可以在声明时指定，也可以在构造方法中指定
    - 实例变量可以直接通过变量名访问。但在静态方法以及其他类中，就应该使用完全限定名：ObjectReference.VariableName
    <br/><br/>
    
- ** 局部变量: **
    ```java
        public class People {
          private String iCode;
          public void reCode(String code) {
            int len = 0;
            this.iCode = code;
        }
      }
    ```
    - 局部变量声明在方法、构造方法或者语句块中
    - 局部变量在方法、构造方法、或者语句块被执行的时候创建，当它们执行完成后，变量将会被销毁
    - 访问修饰符不能用于局部变量
    - 局部变量只在声明它的方法、构造方法或者语句块中可见
    - 局部变量是在栈上分配的
    - 局部变量没有默认值，所以局部变量被声明后，必须经过初始化，才可以使用
    <br/><br/>

##### 基本数据类型

   |类型 | 大小/位 | 表示范围 | 默认值 |
   |:----:|:----:|:--------:|:-----: |
   |byte |8|2^7-1 ~ 2^7|0|
   |short |16|2^15-1 ~ 2^15|0|
   |int  |32|2^31-1 ~ -2^31|0|
   |long |64|2^63-1 ~ -2^63|0L|
   |float|32|2^31-1 ~ -2^31|0.0f|
   |double|64|2^63-1 ~ -2^63|0.0d|
   |char |16|  0~65535(Unicode) |\u0000|
   |boolean |1|true/false|false|


##### 引用数据类型
    java 的基础数据为非引用类型变量，指向对象的变量为引用变量，变量申明类型后不可修改(类型不可修改)
    引用变量可引用兼容(自身/继承关系等)的其它变量
    java的对象数组都为引用类型
    java的所有应用类型的默认值都为null

##### 自动装箱
    java在 1.5 之后引入的新特性，原始基础类型与对象类型之间代码无显示额外操作的互相转换
   
   类型 | 大小/位 
   :----:|:----:
   byte| Byte
   short|Short
   int|Integer
   long|Long
   float|Float
   double|Double
   char|Character
   boolean|Boolean

    装箱(valueOf)：基础->对象   拆箱(inObject)：对象->基础
    包装类（Integer、Long、Byte、Double、Float、Short）都是抽象类 Number 的子类
    NOTE:注意避免过多的在循环变量中使用包装类
##### 自动类型转换
- 整型、实型（常量）、字符型数据可以混合运算。运算中，不同类型的数据先转化为同一类型

    低 ==> 高: byte,short,char -> int -> long -> float -> double 
- boolean类型无法类型转换
- 对象类型转换需要关联性
- 在把容量大的类型转换为容量小的类型时必须使用强制类型转换（精度溢出/损失）

##### 异常


### 面向对象 

### 集合框架（数据结构）

### JAVA数据结构 

### 流框架 IO 

### 网络编程 

### 并发编程 
> 并发 时间上同时，并行 同时运行


   - Motivation
   - Multi-threaded programming use cases
   > cpu与io性能差异
   >
   - Computer architecture
   - Operating systems basics
   - Java threads
   - Java memory model
   - Thread synchronization


### Lambda Functional programming
