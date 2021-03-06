# 加载时机

- new对象、调用类的静态方法、使用静态字段（final修饰的常量除外）
- 反射调用
- 初始化一个类时，父类未初始化，则触发父类初始化
- 虚拟机启动时，主类初始化
- java.lang.invoke.MethodHandle解析结果的方法句柄触发对应的类初始化

> 虚拟机的类初始化只有以上5中情况。
>
> 不会触发类初始化的情况：
>
> 1. 在通过子类调用父类的静态字段，只初始化父类，不会初始化子类
> 2. 通过数组定义类的引用，会触发*L+类名*的数组类初始化，不会触发类的初始化
> 3. 调用类常量，由于类常量在编译期已经加载入常量池，故不会导致初始化
>
> 以上三种情况其实还是会导致类加载，只是不初始化。

# 类加载过程

###  1 加载

通过类的全限定名获取class文件的字节流，可以从任何类型的文件或网络中获取class类的字节流。

### 2 校验

字节流的格式、字节码的语义、类的继承关系、变量声明是否合法，主要时确保字节码是安全、未被修改、且可以使用。

### 3 准备

解析出类的结构放于方法区，并给类结构分配内存，包括类变量、类常量、类方法、实例方法，给类变量分配内存并赋默认值，类常量会被初始化，而实例变量在初始化时再分配内存，例如：

```java
static int a=2；
static final int b = 3;
```

在准备阶段a的值为0，b的值为3。

### 4 解析

将虚拟机常量池中的符号引用替换为直接引用。

### 5 初始化

该处初始化为类的初始化，实例的初始化将会在对象创建阶段进行。初始化的规则如下：

- \<clinit\>()方法有编译器自动收集类中的类变量赋值操作和静态块合并产生，收集的顺序由语句在源文件中出现的顺序决定，静态块只能访问定义在它之前的类变量，对于定义在它之后的类变量，它只能赋值不能访问。
- \<clinit\>()方法有编译器自动生成，在执行\<clinit\>()之前，会先执行父类\<clinit\>()，无序显示调用，而实例构造器调用父类实例构造器需要显示调用才能实现先调用父类在执行子类构造器的逻辑。
- \<clinit\>()不是必须的，如果没有类变量和静态块，则不生成。
- 接口中执行\<clinit\>()之前不会执行父接口的\<clinit\>()，只有父接口中的类变量第一次使用时才会执行父接口\<clinit\>()。
- \<clinit\>()是线程安全的，相当于方法体上加了个synchronized。
  


