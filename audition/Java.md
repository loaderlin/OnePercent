初级

- Java关键字(小写)
- true,false,null 文字常量(literals)
- 程序遇到return语句将不会执行finally语句

### Java数据类型

8种基本数据类型:

数据类型 | 大小(二进制位数) | 范围 | 默认值
--- | --- | --- | --- |
byte(字节) | 8 | -128 - 127 | 0
shot(短整型) | 16 | -32768 - 32768 | 0
int(整型) | 32 | -2147483648-2147483648 | 0
long(长整型) | 64 | -9233372036854477808-9233372036854477808 | 0
float(浮点型) | 32 | -3.40292347E+38-3.40292347E+38 | 0.0f
double(双精度) | 64 | -1.79769313486231570E+308-1.79769313486231570E+308 | 0.0d
char(字符型) | 16  | ‘ \u0000 - u\ffff ’  | ‘\u0000 ’
boolean(布尔型) | 1 | true/false | false

### 运算符优先级

优先级 | 运算符
-- | --
括号(1级): | 	()  [ ](数组取下标) .(取成员变量)
单目(2级)(从右向左) | 	! +(正)-(负)~（按位取反） ++ -- 
算术(3-5级) | 	* / %---->>>> + ----->>>><< >> >>> 
关系(6-7级)	| < <= > >= instanceof---->>>> == !=
位(8-10级)(特殊的单目)	| & ---->>>>^ ---->>>> \|
逻辑(11-12级) | 	&& ---->>>> \|
条件(13级) | 	? :
赋值(14级)(从右向左) | 	= += -+ *= /= %= &= \|= ^= ~= <<= >>= >>>=

### 程序流程控制

switch支持的类型有：byte,short,char,int以及枚举类型

### &(与) 和 &&(短路与) 的区别？

电路问题总结

& --> 不管怎样，都会执行"&"符号左右两边的程序

&& --> 只有当符号"&&"左边程序为真(true)后，才会执行符号"&&"右边的程序。

运算规则

& --> 只要左右两边有一个为false，则为false；只有全部都为true的时候，结果为true

&& --> 只要符号左边为false，则结果为false；当左边为true，同时右边也为true，则结果为true

||（短路或）和 |（或）都是表示“或”，区别是||只要满足第一个条件，后面的条件就不再判断，而|要对所有的条件进行判断。

### Java中 "==" 和 equals 的区别

- 基本数据类型（也称原始数据类型） ：byte,short,char,int,long,float,double,boolean。他们之间的比较，应用双等号（==）,比较的是他们的值。
- 引用数据类型：当他们用（==）进行比较的时候，比较的是他们在内存中的存放地址（确切的说，是堆内存地址）。

> 对于第二种类型，除非是同一个new出来的对象，他们的比较后的结果为true，否则比较后结果为false。因为每new一次，都会重新开辟堆内存空间。

```java
public class StringDemo {
    public static void main(String args[]) {
        String str1 = "Hello";
        String str2 = new String("Hello");
        String str3 = str2; // 引用传递
        System.out.println(str1 == str2); // false
        System.out.println(str1 == str3); // false
        System.out.println(str2 == str3); // true
        System.out.println(str1.equals(str2)); // true
        System.out.println(str1.equals(str3)); // true
        System.out.println(str2.equals(str3)); // true
    }
}


public class ObjectDemo{
    public static void main(String[] args) {
        String s1 = "Hello";
        String s2 = new String("Hello");
        s2 = s2.intern();
        System.out.println(s1 == s2);       //  true
        System.out.println(s1.equals(s2));  //  true
    }
}
```

>java.lang.String的intern()方法"abc".intern()方法的返回值还是字符串"abc"，表面上看起来好像这个方法没什么用处。但实际上，它做了个小动作：检查字符串池里是否存在"abc"这么一个字符串，如果存在，就返回池里的字符串；如果不存在，该方法会 把"abc"添加到字符串池中，然后再返回它的引用。

### HashSet 与 HashMap 的区别

HashSet实现了Set接口，它不允许集合中有重复的值。仅仅存储对象。
HashSet中元素的两个关键方法hashCode和equals方法。add()

HashMap实现了Map接口，Map接口对键值对进行映射。Map不允许重复的键。Map接口有两个基本的实现，HashMap和TreeMap。TreeMap保存了对象的排列次序，而HashMap则不能。HashMap允许键和值为null。put()


## Java Test

Java默认提供的三个ClassLoader是BootStrap ClassLoader，Extension ClassLoader，APP ClassLoader

ClassLoader使用的是双亲委托模型来搜索类的

JVM在判定两个class是否相同时，不仅要判断两个类名是否相同，而且要判断是否由同一个类加载器实例加载的。

ClassLoader就是用来动态加载class文件到内存当中用的。

JVM堆分为：新生代（一般是一个Eden区，两个Survivor区），老年代（old区）。常量池属于PermGen（方法区）

Java 语言性特点
- Java致力于检查程序在编译和运行时的错误。
- Java虚拟机实现了跨平台接口
- Java操纵内存减少了内存出错的可能性
- Java还实现了真数组，避免覆盖数据的可能

Java 真数组
- 在内存中连续分配。
- 数组所存在的内存空间为数组专用，避免了数据被覆盖的问题。
- 数组内存放的类型是确定的，唯一的。

会话跟踪技术

- Cookie是Web服务器发送给客户端的一小段消息，客户端请求时，可以读取该消息发送到服务器端
- 关闭浏览器意味着临时会话ID丢失，但所有与原会话关联的会话数据仍保留在服务器上，自至会话过期
- 在禁用Cookie时可以使用URL重写技术跟踪会话
- 隐藏域在页面中对于用户（浏览器）是不可见的，在表单中插入隐藏域的目的在于收集或发送信息，以利于被处理表单的程序所使用。浏览者单击发送按钮发送表单时候，隐藏域的信息也被一起发送到服务器。
