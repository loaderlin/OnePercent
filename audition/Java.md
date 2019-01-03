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