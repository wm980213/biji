#   **Java高级**

## **二、Java常用类**

### **1.String类**

* **代表字符串。**Java 程序中的所有字符串字面值（如 "abc" ）都作为此类的实例实现。

*  String是一个**final类**，代表**不可变的字符序列**。 

* 字符串是常量，用双引号引起来表示。它们的值在创建之后不能更改。 

* String对象的字符内容是存储在一个字符数组value[]中的。

  ```java
  public final class String
  implements java.io.Serializable, Comparable<String>, CharSequence {
  /** The value is used for character storage. */
  private final char value[];
  /** Cache the hash code for the string */
  private int hash; // Default to 0
  ```

  

​                       String str1 = “abc”;**与**String str2 = new String(“abc”);的区别？

![](C:\Users\10463\Desktop\bj\新建文件夹\QQ截图20200305100836.png)

* 字符串常量存储在字符串常量池，目的是共享

* 字符串非常量对象存储在堆中。



#####     1.1  **String使用陷阱**

* String s1 = "a"; 

  说明：在字符串常量池中创建了一个字面量为"a"的字符串。

* s1 = s1 + "b"; 

  说明：实际上原来的“a”字符串对象已经丢弃了，现在在堆空间中产生了一个字符

  串s1+"b"（也就是"ab")。如果多次执行这些改变串内容的操作，会导致大量副本字符串对象存留在内存中，降低效率。如果这样的操作放到循环中，会极大影响程序的性能

* String s2 = "ab";

  说明：直接在字符串常量池中创建一个字面量为"ab"的字符串。

* String s3 = "a" + "b";

  说明：s3指向字符串常量池中已经创建的"ab"的字符串。

  String s4 = s1.intern();

  说明：堆空间的s1对象在调用intern()之后，会将常量池中已经存在的"ab"字符串

  赋值给s4。



##### **1.2 String常用方法**

* **boolean endsWith(String suffix)**：测试此字符串是否以指定的后缀结束

* **boolean startsWith(String prefix)**：测试此字符串是否以指定的前缀开始

* **boolean startsWith(String prefix, int toffset)**：测试此字符串从指定索引开始的子字符串是否以指定前缀开始

* **boolean contains(CharSequence s)**：当且仅当此字符串包含指定的 char 值序列时，返回 true
* **int indexOf(String str)**：返回指定子字符串在此字符串中第一次出现处的索引
* **int indexOf(String str, int fromIndex)**：返回指定子字符串在此字符串中第一次出现处的索引，从指定的索引开始

* **int lastIndexOf(String str)**：返回指定子字符串在此字符串中最右边出现处的索引
* **int lastIndexOf(String str, int fromIndex)**：返回指定子字符串在此字符串中最后一次出现处的索引，从指定的索引开始反向搜索

**注：**indexOf和lastIndexOf方法如果未找到都是返回-1



* **String replace(char oldChar, char newChar)****：**返回一个新的字符串，它是通过用 newChar 替换此字符串中出现的所有 oldChar 得到的。 

* **String replace(CharSequence target, CharSequence replacement)**：使用指定的字面值替换序列替换此字符串所有匹配字面值目标序列的子字符串。 

* **String replaceAll(String regex, String replacement)** **：** 使 用 给 定 的replacement 替换此字符串所有匹配给定的正则表达式的子字符串。 

* **String replaceFirst(String regex, String replacement)** **：** 使 用 给 定 的replacement 替换此字符串匹配给定的正则表达式的第一个子字符串。 

* **boolean matches(String regex)**：告知此字符串是否匹配给定的正则表达式。 

* **String[] split(String regex)**：根据给定正则表达式的匹配拆分此字符串。 

* **String[] split(String regex, int limit)**：根据匹配给定的正则表达式来拆分此字符串，最多不超过limit个，如果超过了，剩下的全部都放到最后一个元素中。

```JAVA
String str = "12hello34world5java7891mysql456";
//把字符串中的数字替换成,，如果结果中开头和结尾有，的话去掉
String string = str.replaceAll("\\d+", ",").replaceAll("^,|,$", "");
System.out.println(string);
String str = "12345";
//判断str字符串中是否全部有数字组成，即有1-n个数字组成
boolean matches = str.matches("\\d+");
System.out.println(matches);
String tel = "0571-4534289";
//判断这是否是一个杭州的固定电话
boolean result = tel.matches("0571-\\d{7,8}");
System.out.println(result);
```



##### 1.3 String与基本数据类型转换

* **字符串 --> 基本数据类型、包装类**

  * Integer包装类的public static int **parseInt(String s)**：可以将由“数字”字符组成的字符串转换为整型。

  * 类似地,使用java.lang包中的Byte、Short、Long、Float、Double类调相应的类方法可以将由“数字”字符组成的字符串，转化为相应的基本数据类型。

* **基本数据类型、包装类 --> 字符串**

  * 调用String类的public String **valueOf(int n)**可将int型转换为字符串

  * 相应的valueOf(byte b)、valueOf(long l)、valueOf(float f)、valueOf(double d)、valueOf(boolean b)可由参数的相应类型到字符串的转换

* **字符数组 -->字符串**
  * String 类的构造器：**String(char[])** **和** **String(char[]，int offset，int length)** 分别用字符数组中的全部字符和部分字符创建字符串对象。

* **字符串-->字符数组**

  * **public char[] toCharArray()**：将字符串中的全部字符存放在一个字符数组中的方法。

  * **public void getChars(int srcBegin, int srcEnd, char[] dst,** **int dstBegin)**：提供了将指定索引范围内的字符串存放到数组中的方法。

*  **字节数组-->字符串**

  * **String(byte[])****：**通过使用平台的默认字符集解码指定的 byte 数组，构造一个新的 String。 

  * **String(byte[]****，****int offset****，****int length)** **：**用指定的字节数组的一部分，

即从数组起始位置offset开始取length个字节构造一个字符串对象。 

* **字符串-->字节数组**
  * **public byte[] getBytes()** **：**使用平台的默认字符集将此 String 编码为byte 序列，并将结果存储到一个新的 byte 数组中。 
  * **public byte[] getBytes(String charsetName)** **：**使用指定的字符集将 此 String 编码到 byte 序列，并将结果存储到新的 byte 数组



```JAVA
/**
 * 涉及到String类与其他结构之间的转换

 */
public class StringTest1 {
    /*
    String 与 byte[]之间的转换
    编码：String --> byte[]:调用String的getBytes()
    解码：byte[] --> String:调用String的构造器

    编码：字符串 -->字节  (看得懂 --->看不懂的二进制数据)
    解码：编码的逆过程，字节 --> 字符串 （看不懂的二进制数据 ---> 看得懂）

    说明：解码时，要求解码使用的字符集必须与编码时使用的字符集一致，否则会出现乱码。
     */
    @Test
    public void test3() throws UnsupportedEncodingException {
        String str1 = "abc123中国";
        byte[] bytes = str1.getBytes();//使用默认的字符集，进行编码。
        System.out.println(Arrays.toString(bytes));

        byte[] gbks = str1.getBytes("gbk");//使用gbk字符集进行编码。
        System.out.println(Arrays.toString(gbks));

        System.out.println("******************");

        String str2 = new String(bytes);//使用默认的字符集，进行解码。
        System.out.println(str2);

        String str3 = new String(gbks);
        System.out.println(str3);//出现乱码。原因：编码集和解码集不一致！


        String str4 = new String(gbks, "gbk");
        System.out.println(str4);//没有出现乱码。原因：编码集和解码集一致！


    }

    /*
    String 与 char[]之间的转换

    String --> char[]:调用String的toCharArray()
    char[] --> String:调用String的构造器
     */
    @Test
    public void test2(){
        String str1 = "abc123";  //题目： a21cb3

        char[] charArray = str1.toCharArray();
        for (int i = 0; i < charArray.length; i++) {
            System.out.println(charArray[i]);
        }

        char[] arr = new char[]{'h','e','l','l','o'};
        String str2 = new String(arr);
        System.out.println(str2);
    }

    /*
    复习：
    String 与基本数据类型、包装类之间的转换。

    String --> 基本数据类型、包装类：调用包装类的静态方法：parseXxx(str)
    基本数据类型、包装类 --> String:调用String重载的valueOf(xxx)

     */
    @Test
    public void test1(){
        String str1 = "123";
//        int num = (int)str1;//错误的
        int num = Integer.parseInt(str1);

        String str2 = String.valueOf(num);//"123"
        String str3 = num + "";

        System.out.println(str1 == str3);
    }

```



### **2.StringBuffer类**

* **StringBuffer类不同于String，其对象必须使用构造器生成。有三个构造器：** 

  * **StringBuffer()：初始容量为16的字符串缓冲区**

  * **StringBuffer(int size)：构造指定容量的字符串缓冲区**

  * **StringBuffer(String str)：将内容初始化为指定字符串内容**



##### **2.1 StringBuffer类的常用方法**



* StringBuffer **append**(xxx)：提供了很多的append()方法，用于进行字符串拼接

* StringBuffer **delete**(int start,int end)：删除指定位置的内容

* StringBuffer **replace**(int start, int end, String str)：把[start,end)位置替换为str

* StringBuffer **insert**(int offset, xxx)：在指定位置插入xxx

* StringBuffer **reverse**() ：把当前字符序列逆转
* public int **indexOf**(String str)
* public String **substring**(int start,int end)
* public int **length**()
* public char **charAt**(int n )
* public void **setCharAt**(int n ,char ch)

```java
** 面试题：对比String、StringBuffer、StringBuilder
** String(JDK1.0)：不可变字符序列
** StringBuffer(JDK1.0)：可变字符序列、效率低、线程安全
** StringBuilder(JDK 5.0)：可变字符序列、效率高、线程不安全
注意：作为参数传递的话，方法内部String不会改变其值，StringBuffer和StringBuilder
会改变其值。
```



```java
package com.atguigu.java;

import org.junit.Test;

/**
 * 关于StringBuffer和StringBuilder的使用
 *
 * @author shkstart
 * @create 2019 下午 3:32
 */
public class StringBufferBuilderTest {
    /*
    对比String、StringBuffer、StringBuilder三者的效率：
    从高到低排列：StringBuilder > StringBuffer > String
     */
    @Test
    public void test3(){
        //初始设置
        long startTime = 0L;
        long endTime = 0L;
        String text = "";
        StringBuffer buffer = new StringBuffer("");
        StringBuilder builder = new StringBuilder("");
        //开始对比
        startTime = System.currentTimeMillis();
        for (int i = 0; i < 20000; i++) {
            buffer.append(String.valueOf(i));
        }
        endTime = System.currentTimeMillis();
        System.out.println("StringBuffer的执行时间：" + (endTime - startTime));

        startTime = System.currentTimeMillis();
        for (int i = 0; i < 20000; i++) {
            builder.append(String.valueOf(i));
        }
        endTime = System.currentTimeMillis();
        System.out.println("StringBuilder的执行时间：" + (endTime - startTime));

        startTime = System.currentTimeMillis();
        for (int i = 0; i < 20000; i++) {
            text = text + i;
        }
        endTime = System.currentTimeMillis();
        System.out.println("String的执行时间：" + (endTime - startTime));

    }

    /*
    StringBuffer的常用方法：
StringBuffer append(xxx)：提供了很多的append()方法，用于进行字符串拼接
StringBuffer delete(int start,int end)：删除指定位置的内容
StringBuffer replace(int start, int end, String str)：把[start,end)位置替换为str
StringBuffer insert(int offset, xxx)：在指定位置插入xxx
StringBuffer reverse() ：把当前字符序列逆转
public int indexOf(String str)
public String substring(int start,int end):返回一个从start开始到end索引结束的左闭右开区间的子字符串
public int length()
public char charAt(int n )
public void setCharAt(int n ,char ch)

        总结：
        增：append(xxx)
        删：delete(int start,int end)
        改：setCharAt(int n ,char ch) / replace(int start, int end, String str)
        查：charAt(int n )
        插：insert(int offset, xxx)
        长度：length();
        *遍历：for() + charAt() / toString()
     */
    @Test
    public void test2(){
        StringBuffer s1 = new StringBuffer("abc");
        s1.append(1);
        s1.append('1');
        System.out.println(s1);
//        s1.delete(2,4);
//        s1.replace(2,4,"hello");
//        s1.insert(2,false);
//        s1.reverse();
        String s2 = s1.substring(1, 3);
        System.out.println(s1);
        System.out.println(s1.length());
        System.out.println(s2);
    }


    /*
    String、StringBuffer、StringBuilder三者的异同？
    String:不可变的字符序列；底层使用char[]存储
    StringBuffer:可变的字符序列；线程安全的，效率低；底层使用char[]存储
    StringBuilder:可变的字符序列；jdk5.0新增的，线程不安全的，效率高；底层使用char[]存储

    源码分析：
    String str = new String();//char[] value = new char[0];
    String str1 = new String("abc");//char[] value = new char[]{'a','b','c'};

    StringBuffer sb1 = new StringBuffer();//char[] value = new char[16];底层创建了一个长度是16的数组。
    System.out.println(sb1.length());//
    sb1.append('a');//value[0] = 'a';
    sb1.append('b');//value[1] = 'b';

    StringBuffer sb2 = new StringBuffer("abc");//char[] value = new char["abc".length() + 16];

    //问题1. System.out.println(sb2.length());//3
    //问题2. 扩容问题:如果要添加的数据底层数组盛不下了，那就需要扩容底层的数组。
             默认情况下，扩容为原来容量的2倍 + 2，同时将原有数组中的元素复制到新的数组中。

            指导意义：开发中建议大家使用：StringBuffer(int capacity) 或 StringBuilder(int capacity)


     */
    @Test
    public void test1(){
        StringBuffer sb1 = new StringBuffer("abc");
        sb1.setCharAt(0,'m');
        System.out.println(sb1);

        StringBuffer sb2 = new StringBuffer();
        System.out.println(sb2.length());//0
    }

}

```



### 3. 时间API

**1. java.lang.System类**

​	System类提供的public static long currentTimeMillis()用来返回当前时间与1970年1月1日0时0分0秒之间以毫秒为单位的时间差。

**2. java.util.Date类**

表示特定的瞬间，精确到毫秒

* **构造器：** 

  * **Date()****：**使用无参构造器创建的对象可以获取本地当前时间。

  * **Date(long date)**

* **常用方法**

  * **getTime():**返回自 1970 年 1 月 1 日 00:00:00 GMT 以来此 Date 对象表示的毫秒数。

  *  **toString():**把此 Date 对象转换为以下形式的 String： dow mon dd hh:mm:ss zzz yyyy 其中： dow 是一周中的某一天 (Sun, Mon, Tue, Wed, Thu, Fri, Sat)，zzz是时间标准。



**3. java.text.SimpleDateFormat类** 

 Date类的API不易于国际化，大部分被废弃了，**java.text.SimpleDateFormat**类是一个不与语言环境有关的方式来格式化和解析日期的具体类。

* **格式化：**

  * **SimpleDateFormat()** ：默认的模式和语言环境创建对象

  * **public SimpleDateFormat(String pattern)**：该构造方法可以用参数pattern指定的格式创建一个对象，该对象调用： **public String format(Date date)**：方法格式化时间对象date

* **解析：**
  * **public Date parse(String source)**：从给定字符串的开始解析文本，以生成一个日期。

**4. java.util.Calendar(日历)类**

Calendar是一个抽象基类，主用用于完成日期字段之间相互操作的功能。

* 获取Calendar实例的方法

  * 使用Calendar.getInstance()方法

  * 调用它的子类GregorianCalendar的构造器。

* 一个Calendar的实例是系统时间的抽象表示，通过get(int field)方法来取得想要的时间信息。比如YEAR、MONTH、DAY_OF_WEEK、HOUR_OF_DAY 、MINUTE、SECOND

  * **public void set(int field,int value)**

  * **public void add(int field,int amount)**

  * **public final Date getTime()**

  * **public final void setTime(Date date)** 

    

**5. 新时间日期API**

**java.time – 包含值对象的基础包**

**java.time.chrono – 提供对不同的日历系统的访问**

**java.time.format – 格式化和解析时间和日期**

**java.time.temporal – 包括底层框架和扩展特性**

**java.time.zone – 包含时区支持的类**

![](C:\Users\10463\Desktop\bj\新建文件夹\QQ截图20200306101344.png)



![](C:\Users\10463\Desktop\bj\新建文件夹\QQ截图20200306101431.png)

![](C:\Users\10463\Desktop\bj\新建文件夹\QQ截图20200306101457.png)



**java.time.format.DateTimeFormatter 类：该类提供了三种格式化方法：**

- 预定义的标准格式。如：

**ISO_LOCAL_DATE_TIME;ISO_LOCAL_DATE;ISO_LOCAL_TIME**

* 本地化相关的格式。如：ofLocalizedDateTime(FormatStyle.LONG)

* 自定义的格式。如：ofPattern(“yyyy-MM-dd hh:mm:ss”)

  ```JAVA
  package com.atguigu.java;
  
  import org.junit.Test;
  
  import java.time.*;
  import java.time.format.DateTimeFormatter;
  import java.time.format.FormatStyle;
  import java.time.temporal.TemporalAccessor;
  import java.util.Date;
  
  /**
   * jdk 8中日期时间API的测试
   *
   * @author shkstart
   * @create 2019 下午 2:44
   */
  public class JDK8DateTimeTest {
  
      @Test
      public void testDate(){
          //偏移量
          Date date1 = new Date(2020 - 1900,9 - 1,8);
          System.out.println(date1);//Tue Sep 08 00:00:00 GMT+08:00 2020
      }
  
      /*
      LocalDate、LocalTime、LocalDateTime 的使用
      说明：
          1.LocalDateTime相较于LocalDate、LocalTime，使用频率要高
          2.类似于Calendar
       */
      @Test
      public void test1(){
          //now():获取当前的日期、时间、日期+时间
          LocalDate localDate = LocalDate.now();
          LocalTime localTime = LocalTime.now();
          LocalDateTime localDateTime = LocalDateTime.now();
  
          System.out.println(localDate);
          System.out.println(localTime);
          System.out.println(localDateTime);
  
          //of():设置指定的年、月、日、时、分、秒。没有偏移量
          LocalDateTime localDateTime1 = LocalDateTime.of(2020, 10, 6, 13, 23, 43);
          System.out.println(localDateTime1);
  
  
          //getXxx()：获取相关的属性
          System.out.println(localDateTime.getDayOfMonth());
          System.out.println(localDateTime.getDayOfWeek());
          System.out.println(localDateTime.getMonth());
          System.out.println(localDateTime.getMonthValue());
          System.out.println(localDateTime.getMinute());
  
          //体现不可变性
          //withXxx():设置相关的属性
          LocalDate localDate1 = localDate.withDayOfMonth(22);
          System.out.println(localDate);
          System.out.println(localDate1);
  
  
          LocalDateTime localDateTime2 = localDateTime.withHour(4);
          System.out.println(localDateTime);
          System.out.println(localDateTime2);
  
          //不可变性
          LocalDateTime localDateTime3 = localDateTime.plusMonths(3);
          System.out.println(localDateTime);
          System.out.println(localDateTime3);
  
          LocalDateTime localDateTime4 = localDateTime.minusDays(6);
          System.out.println(localDateTime);
          System.out.println(localDateTime4);
      }
  
      /*
      Instant的使用
      类似于 java.util.Date类
  
       */
      @Test
      public void test2(){
          //now():获取本初子午线对应的标准时间
          Instant instant = Instant.now();
          System.out.println(instant);//2019-02-18T07:29:41.719Z
  
          //添加时间的偏移量
          OffsetDateTime offsetDateTime = instant.atOffset(ZoneOffset.ofHours(8));
          System.out.println(offsetDateTime);//2019-02-18T15:32:50.611+08:00
  
          //toEpochMilli():获取自1970年1月1日0时0分0秒（UTC）开始的毫秒数  ---> Date类的getTime()
          long milli = instant.toEpochMilli();
          System.out.println(milli);
  
          //ofEpochMilli():通过给定的毫秒数，获取Instant实例  -->Date(long millis)
          Instant instant1 = Instant.ofEpochMilli(1550475314878L);
          System.out.println(instant1);
      }
  
      /*
      DateTimeFormatter:格式化或解析日期、时间
      类似于SimpleDateFormat
  
       */
  
      @Test
      public void test3(){
  //        方式一：预定义的标准格式。如：ISO_LOCAL_DATE_TIME;ISO_LOCAL_DATE;ISO_LOCAL_TIME
          DateTimeFormatter formatter = DateTimeFormatter.ISO_LOCAL_DATE_TIME;
          //格式化:日期-->字符串
          LocalDateTime localDateTime = LocalDateTime.now();
          String str1 = formatter.format(localDateTime);
          System.out.println(localDateTime);
          System.out.println(str1);//2019-02-18T15:42:18.797
  
          //解析：字符串 -->日期
          TemporalAccessor parse = formatter.parse("2019-02-18T15:42:18.797");
          System.out.println(parse);
  
  //        方式二：
  //        本地化相关的格式。如：ofLocalizedDateTime()
  //        FormatStyle.LONG / FormatStyle.MEDIUM / FormatStyle.SHORT :适用于LocalDateTime
          DateTimeFormatter formatter1 = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.LONG);
          //格式化
          String str2 = formatter1.format(localDateTime);
          System.out.println(str2);//2019年2月18日 下午03时47分16秒
  
  
  //      本地化相关的格式。如：ofLocalizedDate()
  //      FormatStyle.FULL / FormatStyle.LONG / FormatStyle.MEDIUM / FormatStyle.SHORT : 适用于LocalDate
          DateTimeFormatter formatter2 = DateTimeFormatter.ofLocalizedDate(FormatStyle.MEDIUM);
          //格式化
          String str3 = formatter2.format(LocalDate.now());
          System.out.println(str3);//2019-2-18
  
  
  //       重点： 方式三：自定义的格式。如：ofPattern(“yyyy-MM-dd hh:mm:ss”)
          DateTimeFormatter formatter3 = DateTimeFormatter.ofPattern("yyyy-MM-dd hh:mm:ss");
          //格式化
          String str4 = formatter3.format(LocalDateTime.now());
          System.out.println(str4);//2019-02-18 03:52:09
  
          //解析
          TemporalAccessor accessor = formatter3.parse("2019-02-18 03:52:09");
          System.out.println(accessor);
  
      }
  
  }
  
  ```

  



### 4. Java比较器

* **自然排序：java.lang.Comparable**

* **定制排序：java.util.Comparator**

  

**方式一：自然排序：java.lang.Comparabl**

* **Comparable接口强行对实现它的每个类的对象进行整体排序。这种排序被称为类的自然排序。**
  * 实现 Comparable 的类必须实现 compareTo(Object obj) 方法，两个对象即通过 compareTo(Object obj) 方法的返回值来比较大小。如果当前对象this大 于形参对象obj，则返回正整数，如果当前对象this小于形参对象obj，则返回负整数，如果当前对象this等于形参对象obj，则返回零。 

* **Comparable** **的典型实现**：(默认都是从小到大排列的) 

  * String：按照字符串中字符的Unicode值进行比较

  * Character：按照字符的Unicode值来进行比较

  * 数值类型对应的包装类以及BigInteger、BigDecimal：按照它们对应的数值大小进行比较
  *  Boolean：true 对应的包装类实例大于 false 对应的包装类实例

  * Date、Time等：后面的日期时间比前面的日期时间大



**方式二：定制排序：java.util.Comparator**

* **当元素的类型没有实现java.lang.Comparable接口而又不方便修改代码，或者实现了java.lang.Comparable接口的排序规则不适合当前的操作，那么可以考虑使用Comparator的对象来排序，强行对多个对象进行整体排序的比较。**

* **重写compare(Object o1,Object o2)方法，比较o1和o2的大小：如果方法返回正整数，则表示o1大于o2；如果返回0，表示相等；返回负整数，表示o1小于o2。** 

* 可以将 Comparator 传递给 sort 方法（如 Collections.sort 或 Arrays.sort），从而允许在排序顺序上实现精确控制。 

* 还可以使用 Comparator 来控制某些数据结构（如有序 set或有序映射）的顺序，或者为那些没有自然顺序的对象 collection 提供排序

![](C:\Users\10463\Desktop\bj\新建文件夹\QQ截图20200306105536.png)



### 5. System类

* System类代表系统，系统级的很多属性和控制方法都放置在该类的内部。

该类位于java.lang包。 

* 由于该类的构造器是private的，所以无法创建该类的对象，也就是无法实

例化该类。其内部的成员变量和成员方法都是static的，所以也可以很方便

的进行调用。 

* 成员变量
  * System类内部包含in、out和err三个成员变量，分别代表标准输入流

(键盘输入)，标准输出流(显示器)和标准错误输出流(显示器)。 

* 成员方法

  * **native long currentTimeMillis()**： 该方法的作用是返回当前的计算机时间，时间的表达格式为当前计算机时间和GMT时间(格林威治时间)1970年1月1号0时0分0秒所差的毫秒数。

  *  **void exit(int status)**：该方法的作用是退出程序。其中status的值为0代表正常退出，非零代表异常退出。**使用该方法可以在图形界面编程中实现程序的退出功能**等。
  * **void gc()**：该方法的作用是请求系统进行垃圾回收。至于系统是否立刻回收，则取决于系统中垃圾回收算法的实现以及系统执行时的情况。

  * **String getProperty(String key)**：该方法的作用是获得系统中属性名为key的属性对应的值。



### 6. Math类

**java.lang.Math提供了一系列静态方法用于科学计算。其方法的参数和返回**

**值类型一般为double型。**

**abs** **绝对值**

**acos,asin,atan,cos,sin,tan** **三角函数**

**sqrt** **平方根**

**pow(double a,doble b) a的b次幂**

**log** **自然对数**

**exp e为底指数**

**max(double a,double b)**

**min(double a,double b)**

**random()** **返回0.0到1.0的随机数**

**long round(double a) double型数据a转换为long型（四舍五入）**

**toDegrees(double angrad)** **弧度—>角度**

**toRadians(double angdeg)** **角度—>弧度**