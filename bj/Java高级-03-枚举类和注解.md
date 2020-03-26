

# Java高级

## 三、枚举类与注解

### 1.枚举类

* **枚举类对象的属性不应允许被改动, 所以应该使用 private final修饰**

* **枚举类的使用 private final 修饰的属性应该在构造器中为其赋值**

* **若枚举类显式的定义了带参数的构造器, 则在列出枚举值时也必须对应的传入参数**



#####  自定义枚举类

1. **私有化类的构造器，保证不能在类的外部创建其对象**

2. **在类的内部创建枚举类的实例。声明为：public static final** 

3. **对象如果有实例变量，应该声明为private final，并在构造器中初始化**



##### **使用枚举类**

* **使用 enum 定义的枚举类默认继承了 java.lang.Enum类，因此不能再继承其他类**

* **枚举类的构造器只能使用 private 权限修饰符**

* **枚举类的所有实例必须在枚举类中显式列出(, 分隔 ; 结尾)。列出的实例系统会自动添加 public static final 修饰**

* **必须在枚举类的第一行声明枚举类对象**

* **switch 表达式中使用Enum定义的枚举类的对象作为表达式, case 子句可以直接使用枚举值的名字, 无需添加枚举类作为限定。**

```java
package com.atguigu.java;

/**
 * 一、枚举类的使用
 * 1.枚举类的理解：类的对象只有有限个，确定的。我们称此类为枚举类
 * 2.当需要定义一组常量时，强烈建议使用枚举类
 * 3.如果枚举类中只有一个对象，则可以作为单例模式的实现方式。
 *
 * 二、如何定义枚举类
 * 方式一：jdk5.0之前，自定义枚举类
 * 方式二：jdk5.0，可以使用enum关键字定义枚举类
 *
 * 三、Enum类中的常用方法：
 *    values()方法：返回枚举类型的对象数组。该方法可以很方便地遍历所有的枚举值。
 *    valueOf(String str)：可以把一个字符串转为对应的枚举类对象。要求字符串必须是枚举类对象的“名字”。如不是，会有运行时异常：IllegalArgumentException。
 *    toString()：返回当前枚举类对象常量的名称
 *
 * 四、使用enum关键字定义的枚举类实现接口的情况
 *   情况一：实现接口，在enum类中实现抽象方法
 *   情况二：让枚举类的对象分别实现接口中的抽象方法
 *
 * @author shkstart
 * @create 2019 上午 10:17
 */
public class SeasonTest {

    public static void main(String[] args) {
        Season spring = Season.SPRING;
        System.out.println(spring);

    }

}
//自定义枚举类
class Season{
    //1.声明Season对象的属性:private final修饰
    private final String seasonName;
    private final String seasonDesc;

    //2.私有化类的构造器,并给对象属性赋值
    private Season(String seasonName,String seasonDesc){
        this.seasonName = seasonName;
        this.seasonDesc = seasonDesc;
    }

    //3.提供当前枚举类的多个对象：public static final的
    public static final Season SPRING = new Season("春天","春暖花开");
    public static final Season SUMMER = new Season("夏天","夏日炎炎");
    public static final Season AUTUMN = new Season("秋天","秋高气爽");
    public static final Season WINTER = new Season("冬天","冰天雪地");

    //4.其他诉求1：获取枚举类对象的属性
    public String getSeasonName() {
        return seasonName;
    }

    public String getSeasonDesc() {
        return seasonDesc;
    }
    //4.其他诉求1：提供toString()
    @Override
    public String toString() {
        return "Season{" +
                "seasonName='" + seasonName + '\'' +
                ", seasonDesc='" + seasonDesc + '\'' +
                '}';
    }
}

```

```java
package com.atguigu.java;

/**
 * 使用enum关键字定义枚举类
 * 说明：定义的枚举类默认继承于java.lang.Enum类
 *
 * @author shkstart
 * @create 2019 上午 10:35
 */
public class SeasonTest1 {
    public static void main(String[] args) {
        Season1 summer = Season1.SUMMER;
        //toString():返回枚举类对象的名称
        System.out.println(summer.toString());

//        System.out.println(Season1.class.getSuperclass());
        System.out.println("****************");
        //values():返回所有的枚举类对象构成的数组
        Season1[] values = Season1.values();
        for(int i = 0;i < values.length;i++){
            System.out.println(values[i]);
            values[i].show();
        }
        System.out.println("****************");
        Thread.State[] values1 = Thread.State.values();
        for (int i = 0; i < values1.length; i++) {
            System.out.println(values1[i]);
        }

        //valueOf(String objName):返回枚举类中对象名是objName的对象。
        Season1 winter = Season1.valueOf("WINTER");
        //如果没有objName的枚举类对象，则抛异常：IllegalArgumentException
//        Season1 winter = Season1.valueOf("WINTER1");
        System.out.println(winter);
        winter.show();
    }
}

interface Info{
    void show();
}

//使用enum关键字枚举类
enum Season1 implements Info{
    //1.提供当前枚举类的对象，多个对象之间用","隔开，末尾对象";"结束
    SPRING("春天","春暖花开"){
        @Override
        public void show() {
            System.out.println("春天在哪里？");
        }
    },
    SUMMER("夏天","夏日炎炎"){
        @Override
        public void show() {
            System.out.println("宁夏");
        }
    },
    AUTUMN("秋天","秋高气爽"){
        @Override
        public void show() {
            System.out.println("秋天不回来");
        }
    },
    WINTER("冬天","冰天雪地"){
        @Override
        public void show() {
            System.out.println("大约在冬季");
        }
    };

    //2.声明Season对象的属性:private final修饰
    private final String seasonName;
    private final String seasonDesc;

    //2.私有化类的构造器,并给对象属性赋值

    private Season1(String seasonName,String seasonDesc){
        this.seasonName = seasonName;
        this.seasonDesc = seasonDesc;
    }

    //4.其他诉求1：获取枚举类对象的属性
    public String getSeasonName() {
        return seasonName;
    }

    public String getSeasonDesc() {
        return seasonDesc;
    }
}
```

![](C:\Users\10463\Desktop\bj\新建文件夹\QQ截图20200318093947.png)



### 2.注解

* **Annotation 可以像修饰符一样被使用, 可用于修饰包,类, 构造器, 方法, 成员变量, 参数, 局部变量的声明, 这些信息被保存在 Annotation 的 “name=value” 对中。**

  

```markdown
**生成文档相关的注解**

@author 标明开发该类模块的作者，多个作者之间使用,分割
@version 标明该类模块的版本
@see 参考转向，也就是相关主题
@since 从哪个版本开始增加的
@param 对方法中某参数的说明，如果没有参数就不能写
@return 对方法返回值的说明，如果方法的返回值类型是void就不能写
@exception 对方法可能抛出的异常进行说明 ，如果方法没有用throws显式抛出的异常就不能写
其中
@param @return 和 @exception 这三个标记都是只用于方法的。
@param的格式要求：@param 形参名 形参类型 形参说明
@return 的格式要求：@return 返回值类型 返回值说明
@exception的格式要求：@exception 异常类型 异常说明
@param和@exception可以并列多个
```



```markdown
**在编译时进行格式检查(JDK内置的三个基本注解)**
    
@Override: 限定重写父类方法, 该注解只能用于方法
@Deprecated: 用于表示所修饰的元素(类, 方法等)已过时。通常是因为所修饰的结构危险或存在更好的选择
@SuppressWarnings: 抑制编译器警告
```



```markdown
**元注解**
   
@Target: 用于修饰 Annotation 定义, 用于指定被修饰的 Annotation 能用于修饰哪些程序元素。 @Target 也包含一个名为 value 的成员变量。
    
@Documented: 用于指定被该元 Annotation 修饰的 Annotation 类将被javadoc 工具提取成文档。默认情况下，javadoc是不包括注解的。 定义为Documented的注解必须设置Retention值为RUNTIME。
    
@Inherited: 被它修饰的 Annotation 将具有继承性。如果某个类使用了被@Inherited 修饰的 Annotation, 则其子类将自动具有该注解

@Retention: 只能用于修饰一个 Annotation 定义, 用于指定该 Annotation 的生命周期, @Rentention 包含一个 RetentionPolicy 类型的成员变量, 使用@Rentention 时必须为该 value 成员变量指定值
	 RetentionPolicy.SOURCE:在源文件中有效（即源文件保留），编译器直接丢弃这种策略的注释
	 RetentionPolicy.CLASS:在class文件中有效（即class保留） ， 当运行 Java 程序时, JVM 不会保留注解。 这是默认值
	 RetentionPolicy.RUNTIME:在运行时有效（即运行时保留），当运行 Java 程序时, JVM 会保留注释。程序可以通过反射获取该注释。

```



```markdown
**注解**

@Service: 注解在类上，表示这是一个业务层bean
@Controller：注解在类上，表示这是一个控制层bean
@Repository: 注解在类上，表示这是一个数据访问层bean
@Component： 注解在类上，表示通用bean ，value不写默认就是类名首字母小写

声明Bean的注解:

@Component : 组件,没有明确的角色
@Service : 在业务逻辑层(service层)使用
@Repository : 在数据访问层(dao层)使用.使用@Repository注解可以确保DAO或者repositories提供异常转译，这个注解修饰的DAO或者repositories类会被ComponetScan发现并配置，同时也不需要为它们提供XML配置项。
@Controller : 在展现层(MVC--SpringMVC)使用
 

**注入Bean的注解:**

@Autowired : Spring提供的注解.自动导入依赖的bean
@Inject : JSR-330提供的注解
@Resource : JSR-250提供的注解
 

**配置文件的注解:**

@Configuration: 相当于传统的xml配置文件，如果有些第三方库需要用到xml文件，建议仍然通过@Configuration类作为项目的配置主类——可以使用@ImportResource注解加载xml配置文件。
@ComponentScan (cn.test.demo): 自动扫描包名下所有使用 @Component @Service  @Repository @Controller 的类,并注册为Bean
@WiselyConfiguration : 组合注解 可以替代 @Configuration和@ComponentScan
@Bean : 注解在方法上,声明当前方法的返回值为一个Bean.
@Bean(initMethod="aa",destroyMethod="bb")--> 指定 aa和bb方法在构造之后.Bean销毁之前执行.
 

**AOP切面编程注解:**

@Aspect : 声明这是一个切面 
@After @Before. @Around 定义切面,可以直接将拦截规则(切入点 PointCut)作为参数
@PointCut : 专门定义拦截规则 然后在 @After @Before. @Around 中调用
@Transcational : 事务处理
@Cacheable : 数据缓存
@EnableAaspectJAutoProxy : 开启Spring 对 这个切面(Aspect )的支持
@Target (ElementType.TYPE):元注解,用来指定注解修饰类的那个成员 -->指定拦截规则
@Retention(RetentionPolicy.RUNTIME) 
--->当定义的注解的@Retention为RUNTIME时，才能够通过运行时的反射机制来处理注解.-->指定拦截规则
 

**Spring 常用配置:**

@import :导入配置类
@Scope : 新建Bean的实例 @Scope("prototype") 声明Scope 为 Prototype
@Value : 属性注入
@Value ("我爱你")  --> 普通字符串注入
@Value ("#{systemProperties['os.name']}") -->注入操作系统属性
@Value ("#{ T (java.lang.Math).random()  * 100.0 }") --> 注入表达式结果
@Value ("#{demoService.another}") --> 注入其他Bean属性
@Value ( "classpath:com/wisely/highlight_spring4/ch2/el/test.txt" ) --> 注入文件资源
@Value ("http://www.baidu.com")-->注入网址资源
@Value ("${book.name}" ) --> 注入配置文件  注意: 使用的是$ 而不是 #
@PostConstruct : 在构造函数执行完之后执行
@PreDestroy  : 在 Bean 销毁之前执行
@ActiveProfiles : 用来声明活动的 profile
@profile: 为不同环境下使用不同的配置提供了支持
 @Profile("dev") .......对方法名为 dev-xxxx的方法提供实例化Bean
@EnableAsync : 开启异步任务的支持(多线程)
@Asyns : 声明这是一个异步任务,可以在类级别 和方法级别声明.
@EnableScheduling : 开启对计划任务的支持(定时器)
@Scheduled : 声明这是一个计划任务 支持多种计划任务,包含 cron. fixDelay fixRate
@Scheduled (dixedDelay = 5000) 通过注解 定时更新
@Conditional : 条件注解,根据满足某一特定条件创建一个特定的Bean
@ContextConfiguration : 加载配置文件
@ContextConfiguration(classes = {TestConfig.class})
@ContextConfiguration用来加载ApplicationContext 
classes属性用来加载配置类
@WebAppCofiguration : 指定加载 ApplicationContext是一个WebApplicationContext

**@Enable注解:**

@EnableAsync : 开启异步任务的支持(多线程)
@EnableScheduling : 开启对计划任务的支持(定时器)
@EnableWebMVC : 开启对Web MVC 的配置支持
@EnableAaspectJAutoProxy : 开启Spring 对 这个切面(Aspect )的支持
@EnableConfigurationProperties 开启对@ConfigurationProperties注解配置Bean的支持
@EnableJpaRepositories : 开启对Spring Data JAP Repository 的支持
@EnableTransactionManagement 开启对注解式事物的支持
@EnableCaching开启注解是缓存的支持.
@EnableDiscoveryClient 让服务发现服务器,使用服务器.Spring cloud 实现服务发现
@EnableEurekaServer 注册服务器 spring cloud 实现服务注册@
@EnableScheduling 让spring可以进行任务调度,功能类似于spring.xml文件中的命名空间<task:*>
@EnableCaching 开启Cache缓存支持;
SpringMVC 常用注解:

@Controller : 注解在类上 声明这个类是springmvc里的Controller,将其声明为一个spring的Bean.
@RequestMapping :可以注解在类上和方法上 映射WEB请求(访问路径和参数)
@RequestMapping(value= "/convert",produces+{"application/x-wisely"}) 设置访问URL 返回值类型

@ResponseBody : 支持将返回值放入response体内 而不是返回一个页面(返回的是一个组数据),表示该方法的返回结果直接写入HTTP response body中，一般在异步获取数据时使用，用于构建RESTful的api。使用@RequestMapping后，返回值通常解析为跳转路径，加上@esponsebody后返回结果不会被解析为跳转路径，而是直接写入HTTP response body中。比如异步获取json数据，加上@Responsebody后，会直接返回json数据。该注解一般会配合@RequestMapping一起使用。

@RequestBody : 允许request的参数在request体中,而不是直接连接在地址后面 次注解放置在参数前
@Path Variable : 用来接收路径参数 如/test/001,001为参数,次注解放置在参数前
@RestController : @Controller + @ResponseBody 组合注解,表示这是个控制器bean,并且是将函数的返回值直 接填入HTTP响应体中,是REST风格的控制器。
@ControllerAdvice : 通过@ControllerAdvice可以将对已控制器的全局配置放置在同一个位置
@ExceptionHandler : 用于全局处理控制器的异常
@ExceptionHandier(value=Exception.class) -->通过value属性可过滤拦截器条件,拦截所有的异常
@InitBinder : 用来设置WebDataBinder , WebDataBinder用来自动绑定前台请求参数到Model中.
@ModelAttrbuute : 绑定键值对到Model中,
@RunWith : 运行器 
@RunWith(JUnit4.class)就是指用JUnit4来运行
@RunWith(SpringJUnit4ClassRunner.class),让测试运行于Spring测试环境
@RunWith(Suite.class)的话就是一套测试集合，
@WebAppConfiguration("src/main/resources") : 注解在类上,用来声明加载的ApplicationContex 是一个WebApplicationContext ,它的属性指定的是Web资源的位置,默认为 src/main/webapp ,自定义修改为 resource

@Before : 在 xxx 前初始化

 

**Spring Boot 注解:**

 @SpringBootApplication : 是Spring Boot 项目的核心注解 主要目的是开启自动配置
@SpringBootApplication注解是一个组合注解,主要组合了@Configuration .+@EnableAutoConfiguration.+@ComponentScan
@Value : 属性注入,读取properties或者 Yml 文件中的属性
@ConfigurationProperties : 将properties属性和一个Bean及其属性关联,从而实现类型安全的配置
@ConfigurationProperties(prefix = "author",locations ={"classpath:config/author.properties"})通过@ConfigurationProperties加载配置,通过prefix属性指定配置前缀,通过location指定配置文件位置

@EnableAutoConfiguration: SpringBoot自动配置（auto-configuration）：尝试根据你添加的jar依赖自动配置你的Spring应用。例如，如果你的classpath下存在HSQLDB，并且你没有手动配置任何数据库连接beans，那么我们将自动配置一个内存型（in-memory）数据库”。你可以将@EnableAutoConfiguration或者@SpringBootApplication注解添加到一个@Configuration类上来选择自动配置。如果发现应用了你不想要的特定自动配置类，你可以使用@EnableAutoConfiguration注解的排除属性来禁用它们。

 

 

**@SuppressWarnings注解**

@SuppressWarnings("unchecked")
告诉编译器忽略 unchecked 警告信息,如使用 list ArrayList等未进行参数化产生的警告信息
@SuppressWarnings("serial")
如果编译器出现这样的警告信息: The serializable class WmailCalendar does not declare a static final serialVersionUID field of type long     使用这个注释将警告信息去掉。
@SuppressWarnings("deprecation")
如果使用了使用@Deprecated注释的方法，编译器将出现警告信息。使用这个注释将警告信息去掉。
@SuppressWarnings("unchecked", "deprecation")
告诉编译器同时忽略unchecked和deprecation的警告信息。
@SuppressWarnings(value={"unchecked", "deprecation"})
等同于@SuppressWarnings("unchecked", "deprecation")
```





```java

package com.atguigu.java1;

import org.junit.Test;

import java.lang.annotation.Annotation;
import java.util.ArrayList;
import java.util.Date;

/**
 * 注解的使用
 *
 * 1. 理解Annotation:
 * ① jdk 5.0 新增的功能
 *
 * ② Annotation 其实就是代码里的特殊标记, 这些标记可以在编译, 类加载, 运行时被读取, 并执行相应的处理。通过使用 Annotation,
 * 程序员可以在不改变原有逻辑的情况下, 在源文件中嵌入一些补充信息。
 *
 * ③在JavaSE中，注解的使用目的比较简单，例如标记过时的功能，忽略警告等。在JavaEE/Android
 * 中注解占据了更重要的角色，例如用来配置应用程序的任何切面，代替JavaEE旧版中所遗留的繁冗
 * 代码和XML配置等。
 *
 * 2. Annocation的使用示例
 * 示例一：生成文档相关的注解
 * 示例二：在编译时进行格式检查(JDK内置的三个基本注解)
     @Override: 限定重写父类方法, 该注解只能用于方法
     @Deprecated: 用于表示所修饰的元素(类, 方法等)已过时。通常是因为所修饰的结构危险或存在更好的选择
     @SuppressWarnings: 抑制编译器警告

  * 示例三：跟踪代码依赖性，实现替代配置文件功能
  *
  * 3. 如何自定义注解：参照@SuppressWarnings定义
      * ① 注解声明为：@interface
      * ② 内部定义成员，通常使用value表示
      * ③ 可以指定成员的默认值，使用default定义
      * ④ 如果自定义注解没有成员，表明是一个标识作用。

     如果注解有成员，在使用注解时，需要指明成员的值。
     自定义注解必须配上注解的信息处理流程(使用反射)才有意义。
     自定义注解通过都会指明两个元注解：Retention、Target

     4. jdk 提供的4种元注解
       元注解：对现有的注解进行解释说明的注解
     Retention：指定所修饰的 Annotation 的生命周期：SOURCE\CLASS（默认行为）\RUNTIME
            只有声明为RUNTIME生命周期的注解，才能通过反射获取。
     Target:用于指定被修饰的 Annotation 能用于修饰哪些程序元素
     *******出现的频率较低*******
     Documented:表示所修饰的注解在被javadoc解析时，保留下来。
     Inherited:被它修饰的 Annotation 将具有继承性。

     5.通过反射获取注解信息 ---到反射内容时系统讲解

     6. jdk 8 中注解的新特性：可重复注解、类型注解

     6.1 可重复注解：① 在MyAnnotation上声明@Repeatable，成员值为MyAnnotations.class
                    ② MyAnnotation的Target和Retention等元注解与MyAnnotations相同。

     6.2 类型注解：
     ElementType.TYPE_PARAMETER 表示该注解能写在类型变量的声明语句中（如：泛型声明）。
     ElementType.TYPE_USE 表示该注解能写在使用类型的任何语句中。

      *
 * @author shkstart
 * @create 2019 上午 11:37
 */
public class AnnotationTest {

    public static void main(String[] args) {
        Person p = new Student();
        p.walk();

        Date date = new Date(2020, 10, 11);
        System.out.println(date);

        @SuppressWarnings("unused")
        int num = 10;

//        System.out.println(num);

        @SuppressWarnings({ "unused", "rawtypes" })
        ArrayList list = new ArrayList();
    }

    @Test
    public void testGetAnnotation(){
        Class clazz = Student.class;
        Annotation[] annotations = clazz.getAnnotations();
        for(int i = 0;i < annotations.length;i++){
            System.out.println(annotations[i]);
        }
    }
}


//jdk 8之前的写法：
//@MyAnnotations({@MyAnnotation(value="hi"),@MyAnnotation(value="hi")})
@MyAnnotation(value="hi")
@MyAnnotation(value="abc")
class Person{
    private String name;
    private int age;

    public Person() {
    }
    @MyAnnotation
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    @MyAnnotation
    public void walk(){
        System.out.println("人走路");
    }
    public void eat(){
        System.out.println("人吃饭");
    }
}

interface Info{
    void show();
}

class Student extends Person implements Info{

    @Override
    public void walk() {
        System.out.println("学生走路");
    }

    public void show() {

    }
}

class Generic<@MyAnnotation T>{

    public void show() throws @MyAnnotation RuntimeException{

        ArrayList<@MyAnnotation String> list = new ArrayList<>();

        int num = (@MyAnnotation int) 10L;
    }

}
```

