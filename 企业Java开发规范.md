﻿# 一、编程规约  
## (一) 命名风格  
1. **【强制】** 代码中的命名均不能以下划线或美元符号开始，也不能以下划线或美元符号结束。 反例：_name/__name/$name/name_/name$/name__  
2. **【强制】** 代码中的命名严禁使用拼音与英文混合的方式，更不允许直接使用中文的方式。 说明：正确的英文拼写和语法可以让阅读者易于理解，避免歧义。注意，即使纯拼音命名方式也要避免采用。  
    正例：alibaba / taobao / youku / hangzhou 等国际通用的名称，可视同英文。 反例：DaZhePromotion [打折] / getPingfenByName() [评分] / int 某变量 = 3  
3. **【强制】** 类名使用UpperCamelCase风格，但以下情形例外：DO / BO / DTO / VO / AO / PO / UID等。  
    正例：MarcoPolo / UserDO / XmlService / TcpUdpDeal / TaPromotion 反例：macroPolo / UserDo / XMLService / TCPUDPDeal / TAPromotion  
4. **【强制】** 方法名、参数名、成员变量、局部变量都统一使用lowerCamelCase风格，必须遵从驼峰形式。  
    正例：localValue / getHttpMessage() / inputUserId  
5. **【强制】** 常量命名全部大写，单词间用下划线隔开，力求语义表达完整清楚，不要嫌名字长。  
    正例：MAX_STOCK_COUNT 反例：MAX_COUNT  
6. **【强制】** 抽象类命名使用Abstract或Base开头；异常类命名使用Exception结尾；测试类命名以它要测试的类的名称开始，以Test结尾。  
7. **【强制】** 类型与中括号紧挨相连来表示数组。正例：定义整形数组int[] arrayDemo;反例：在main参数中，使用String args[]来定义。  
8. **【强制】** POJO类中布尔类型的变量，都不要加is前缀，否则部分框架解析会引起序列化错误。  
    反例：定义为基本数据类型Boolean isDeleted的属性，它的方法也是isDeleted()，RPC框架在反向解析的时候，“误以为”对应的属性名称是deleted，导致属性获取不到，进而抛出异常。  
9. **【强制】** 包名统一使用小写，点分隔符之间有且仅有一个自然语义的英语单词。包名统一使用单数形式，但是类名如果有复数含义，类名可以使用复数形式。  
    正例：应用工具类包名为com.alibaba.ai.util、类名为MessageUtils（此规则参考spring的框架结构）  
10. **【强制】** 杜绝完全不规范的缩写，避免望文不知义。  
    反例：AbstractClass“缩写”命名成AbsClass；condition“缩写”命名成 condi，此类随意缩写严重降低了代码的可阅读性。  
11. **【推荐】** 为了达到代码自解释的目标，任何自定义编程元素在命名时，使用尽量完整的单词组合来表达其意。  
    正例：在JDK中，表达原子更新的类名为：AtomicReferenceFieldUpdater。反例：变量int a的随意命名方式。  
12. **【推荐】** 如果模块、接口、类、方法使用了设计模式，在命名时需体现出具体模式。 说明：将设计模式体现在名字中，有利于阅读者快速理解架构设计理念。  
    正例：public class OrderFactory; public class LoginProxy; public class ResourceObserver;  
13. **【推荐】** 接口类中的方法和属性不要加任何修饰符号（public 也不要加），保持代码的简洁性，并加上有效的Javadoc注释。尽量不要在接口里定义变量，如果一定要定义变量，肯定是与接口方法相关，并且是整个应用的基础常量。  
    正例：接口方法签名void commit(); 接口基础常量String COMPANY = "alibaba"; 反例：接口方法定义public abstract void f(); 说明：JDK8中接口允许有默认实现，那么这个default方法，是对所有实现类都有价值的默认实现。  
14. 接口和实现类的命名有两套规则：  
    1）**【强制】** 对于Service和DAO类，基于SOA的理念，暴露出来的服务一定是接口，内部的实现类用Impl的后缀与接口区别。  
        正例：CacheServiceImpl实现CacheService接口。  
    2） **【推荐】** 如果是形容能力的接口名称，取对应的形容词为接口名（通常是–able的形式）。  
        正例：AbstractTranslator实现 Translatable接口。  
15. **【参考】** 枚举类名建议带上Enum后缀，枚举成员名称需要全大写，单词间用下划线隔开。 说明：枚举其实就是特殊的类，域成员均为常量，且构造方法被默认强制是私有。  
    正例：枚举名字为ProcessStatusEnum的成员名称：SUCCESS / UNKNOWN_REASON。  
16. **【参考】** 各层命名规约：  
    A) Service/DAO层方法命名规约  
        1） 获取单个对象的方法用get做前缀。  
        2） 获取多个对象的方法用list做前缀，复数形式结尾如：listObjects。  
        3） 获取统计值的方法用count做前缀。  
        4） 插入的方法用save/insert做前缀。  
        5） 删除的方法用remove/delete做前缀。  
        6） 修改的方法用update做前缀。  
    B) 领域模型命名规约  
        1） 数据对象：xxxDO，xxx即为数据表名。  
        2） 数据传输对象：xxxDTO，xxx为业务领域相关的名称。  
        3） 展示对象：xxxVO，xxx一般为网页名称。  
        4） POJO是DO/DTO/BO/VO的统称，禁止命名成xxxPOJO。
## (二) 常量定义  
1. 【强制】不允许任何魔法值（即未经预先定义的常量）直接出现在代码中。 反例：String key = "Id#taobao_" + tradeId; cache.put(key, value);  
2. 【强制】在long或者Long赋值时，数值后使用大写的L，不能是小写的l，小写容易跟数字1混淆，造成误解。 说明：Long a = 2l; 写的是数字的21，还是Long型的2?  
3. 【推荐】不要使用一个常量类维护所有常量，要按常量功能进行归类，分开维护。 说明：大而全的常量类，杂乱无章，使用查找功能才能定位到修改的常量，不利于理解和维护。  
正例：缓存相关常量放在类CacheConsts下；系统配置相关常量放在类ConfigConsts下。  
4. 【推荐】常量的复用层次有五层：跨应用共享常量、应用内共享常量、子工程内共享常量、包内共享常量、类内共享常量。 1） 跨应用共享常量：放置在二方库中，通常是client.jar中的constant目录下。 2） 应用内共享常量：放置在一方库中，通常是子模块中的constant目录下。 反例：易懂变量也要统一定义成应用内共享常量，两位攻城师在两个类中分别定义了表示“是”的变量： 类A中：public static final String YES = "yes";  
类B中：public static final String YES = "y"; A.YES.equals(B.YES)，预期是true，但实际返回为false，导致线上问题。  
3） 子工程内部共享常量：即在当前子工程的constant目录下。 4） 包内共享常量：即在当前包下单独的constant目录下。 5） 类内共享常量：直接在类内部private static final定义。  
5. 【推荐】如果变量值仅在一个固定范围内变化用enum类型来定义。 说明：如果存在名称之外的延伸属性应使用enum类型，下面正例中的数字就是延伸信息，表示一年中的第几个季节。 正例：  
public enum SeasonEnum {  
SPRING(1), SUMMER(2), AUTUMN(3), WINTER(4);  
private int seq;  
SeasonEnum(int seq){  
this.seq = seq;  
}  
}
### (三) 代码格式

1. **【强制】** 大括号的使用约定。
   - 如果是大括号内为空，则简洁地写成`{}`即可，不需要换行；
   - 如果是非空代码块则：
     1. 左大括号前不换行。
     2. 左大括号后换行。
     3. 右大括号前换行。
     4. 右大括号后还有`else`等代码则不换行；表示终止的右大括号后必须换行。

2. **【强制】** 左小括号和字符之间不出现空格；同样，右小括号和字符之间也不出现空格；而左大括号前需要空格。
   - 反例：`if ( 空格a == b空格 )`

3. **【强制】** `if/for/while/switch/do`等保留字与括号之间都必须加空格。

4. **【强制】** 任何二目、三目运算符的左右两边都需要加一个空格。
   - 说明：运算符包括赋值运算符`=、`逻辑运算符`&&、`加减乘除符号等。

5. **【强制】** 采用4个空格缩进，禁止使用tab字符。
   - 说明：如果使用tab缩进，必须设置1个tab为4个空格。IDEA设置tab为4个空格时，请勿勾选`Use tab character`；而在eclipse中，必须勾选`insert spaces for tabs`。
   - 正例：
   

     public static void main(String[] args) {
         // 缩进4个空格
         String say = "hello";
         // 运算符的左右必须有一个空格
         int flag = 0;
         // 关键词if与括号之间必须有一个空格，括号内的f与左括号，0与右括号不需要空格
         if (flag == 0) {
             System.out.println(say);
         }
         // 左大括号前加空格且不换行；左大括号后换行
         if (flag == 1) {
             System.out.println("world");
             // 右大括号前换行，右大括号后有else，不用换行
         } else {
             System.out.println("ok");
             // 在右大括号后直接结束，则必须换行
         }
     }

6. **【强制】** 注释的双斜线与注释内容之间有且仅有一个空格。
   - 正例：


     `// 这是示例注释，请注意在双斜线之后有一个空格`
     `String ygb = new String();`

7. **【强制】** 单行字符数限制不超过120个，超出需要换行，换行时遵循如下原则：
   - 第二行相对第一行缩进4个空格，从第三行开始，不再继续缩进，参考示例。
   - 运算符与下文一起换行。
   - 方法调用的点符号与下文一起换行。
   - 方法调用中的多个参数需要换行时，在逗号后进行。
   - 在括号前不要换行，见反例。
   - 正例：
   

     StringBuffer sb = new StringBuffer();
     // 超过120个字符的情况下，换行缩进4个空格，点号和方法名称一起换行
     sb.append("zi").append("xin")...
         .append("huang")...
         .append("huang")...
         .append("huang");
   - 反例：


     StringBuffer sb = new StringBuffer();
     // 超过120个字符的情况下，不要在括号前换行
     sb.append("zi").append("xin")...append
         ("huang");
     // 参数很多的方法调用可能超过120个字符，不要在逗号前换行
     method(args1, args2, args3, ...
         , argsX);

8. **【强制】** 方法参数在定义和传入时，多个参数逗号后边必须加空格。
   - 正例：下例中实参的`args1`，后边必须要有一个空格。
     `method(args1, args2, args3);`

9. **【强制】** IDE的text file encoding设置为UTF-8; IDE中文件的换行符使用Unix格式，不要使用Windows格式。

10. **【推荐】** 单个方法的总行数不超过80行。
    - 说明：包括方法签名、结束右大括号、方法内代码、注释、空行、回车及任何不可见字符的总行数不超过80行。
    - 正例：代码逻辑分清红花和绿叶，个性和共性，绿叶逻辑单独出来成为额外方法，使主干代码更加清晰；共性逻辑抽取成为共性方法，便于复用和维护。

11. **【推荐】** 没有必要增加若干空格来使某一行的字符与上一行对应位置的字符对齐。
    - 正例：
    

      int one = 1;
      long two = 2L;
      float three = 3F;
      StringBuffer sb = new StringBuffer();

- 说明：增加sb这个变量，如果需要对齐，则给a、b、c都要增加几个空格，在变量比较多的情况下，是非常累赘的事情。

12. **【推荐】** 不同逻辑、不同语义、不同业务的代码之间插入一个空行分隔开来以提升可读性。
    - 说明：任何情形，没有必要插入多个空行进行隔开。
## (四) 并发处理  
1. **【强制】** 获取单例对象需要保证线程安全，其中的方法也要保证线程安全。 说明：资源驱动类、工具类、单例工厂类都需要注意。  
2. **【强制】** 创建线程或线程池时请指定有意义的线程名称，方便出错时回溯。 正例：  
public class TimerTaskThread extends Thread { 
public TimerTaskThread() { 
super.setName("TimerTaskThread"); 
... 
} 
}
3. **【强制】** 线程资源必须通过线程池提供，不允许在应用中自行显式创建线程。 说明：使用线程池的好处是减少在创建和销毁线程上所消耗的时间以及系统资源的开销，解决资源不足的问题。如果不使用线程池，有可能造成系统创建大量同类线程而导致消耗完内存或者“过度切换”的问题。
4. **【强制】** 线程池不允许使用Executors去创建，而是通过ThreadPoolExecutor的方式，这样的处理方式让写的同学更加明确线程池的运行规则，规避资源耗尽的风险。说明：Executors返回的线程池对象的弊端如下：
1）FixedThreadPool和SingleThreadPool:允许的请求队列长度为Integer.MAX_VALUE，可能会堆积大量的请求，从而导致OOM。2）CachedThreadPool和ScheduledThreadPool:允许的创建线程数量为Integer.MAX_VALUE，可能会创建大量的线程，从而导致OOM。
5. **【强制】** SimpleDateFormat 是线程不安全的类，一般不要定义为static变量，如果定义为static，必须加锁，或者使用DateUtils工具类。 正例：注意线程安全，使用DateUtils。亦推荐如下处理：
private static final ThreadLocal<DateFormat> df = new ThreadLocal<DateFormat>() { 
@Override 
protected DateFormat initialValue() { 
return new SimpleDateFormat("yyyy-MM-dd"); 
} 
};
说明：如果是JDK8的应用，可以使用Instant代替Date，LocalDateTime代替Calendar，DateTimeFormatter代替SimpleDateFormat，官方给出的解释：simple beautiful strong immutable thread-safe。

6. **【强制】** 高并发时，同步调用应该去考量锁的性能损耗。能用无锁数据结构，就不要用锁；能锁区块，就不要锁整个方法体；能用对象锁，就不要用类锁。

说明：尽可能使加锁的代码块工作量尽可能的小，避免在锁代码块中调用RPC方法。

7. **【强制】** 对多个资源、数据库表、对象同时加锁时，需要保持一致的加锁顺序，否则可能会造成死锁。 说明：线程一需要对表A、B、C依次全部加锁后才可以进行更新操作，那么线程二的加锁顺序也必须是A、B、C，否则可能出现死锁。

8. **【强制】** 并发修改同一记录时，避免更新丢失，需要加锁。要么在应用层加锁，要么在缓存加锁，要么在数据库层使用乐观锁，使用version作为更新依据。 说明：如果每次访问冲突概率小于20%，推荐使用乐观锁，否则使用悲观锁。乐观锁的重试次数不得小于3次。

9. **【强制】** 多线程并行处理定时任务时，Timer运行多个TimeTask时，只要其中之一没有捕获抛出的异常，其它任务便会自动终止运行，使用ScheduledExecutorService则没有这个问题。

10. **【推荐】** 使用CountDownLatch进行异步转同步操作，每个线程退出前必须调用countDown方法，线程执行代码注意catch异常，确保countDown方法被执行到，避免主线程无法执行至await方法，直到超时才返回结果。 说明：注意，子线程抛出异常堆栈，不能在主线程try-catch到。

11. **【推荐】** 避免Random实例被多线程使用，虽然共享该实例是线程安全的，但会因竞争同一seed 导致的性能下降。

说明：Random实例包括java.util.Random 的实例或者 Math.random()的方式。 正例：在JDK7之后，可以直接使用API ThreadLocalRandom，而在 JDK7之前，需要编码保证每个线程持有一个实例。

12. **【推荐】** 在并发场景下，通过双重检查锁（double-checked locking）实现延迟初始化的优化问题隐患(可参考 The "Double-Checked Locking is Broken" Declaration)，推荐解决方案中较为简单一种（适用于JDK5及以上版本），将目标属性声明为 volatile型。 反例：
```
class LazyInitDemo { 
private Helper helper = null; 
public Helper getHelper() { 
if (helper == null) synchronized(this) { 
if (helper == null) 
helper = new Helper(); 
} 
return helper; 
} 
// other methods and fields...
}
```
13. **【参考】** volatile解决多线程内存不可见问题。对于一写多读，是可以解决变量同步问题，但是如果多写，同样无法解决线程安全问题。如果是count++操作，使用如下类实现：AtomicInteger count = new AtomicInteger(); count.addAndGet(1); 如果是JDK8，推荐使用LongAdder对象，比AtomicLong性能更好（减少乐观锁的重试次数）。
14. **【参考】** HashMap在容量不够进行resize时由于高并发可能出现死链，导致CPU飙升，在开发过程中可以使用其它数据结构或加锁来规避此风险。
15.  **【参考】** ThreadLocal无法解决共享对象的更新问题，ThreadLocal对象建议使用static修饰。这个变量是针对一个线程内所有操作共享的，所以设置为静态变量，所有此类实例共享此静态变量 ，也就是说在类第一次被使用时装载，只分配一块存储空间，所有此类的对象(只要是这个线程内定义的)都可以操控这个变量。
## (五) 控制语句
1. **【强制】** 在一个switch块内，每个case要么通过break/return等来终止，要么注释说明程序将继续执行到哪一个case为止；在一个switch块内，都必须包含一个default语句并且放在最后，即使空代码。
2. **【强制】** 在if/else/for/while/do语句中必须使用大括号。即使只有一行代码，避免采用单行的编码方式：if (condition) statements;
3. **【强制】** 在高并发场景中，避免使用”等于”判断作为中断或退出的条件。说明：如果并发控制没有处理好，容易产生等值判断被“击穿”的情况，使用大于或小于的区间判断条件来代替。反例：判断剩余奖品数量等于0时，终止发放奖品，但因为并发处理错误导致奖品数量瞬间变成了负数，这样的话，活动无法终止。
4. **【推荐】** 表达异常的分支时，少用if-else方式，这种方式可以改写成：
if (condition) {
...
return obj;
}
// 接着写else的业务逻辑代码;
说明：如果非得使用if()...else if()...else...方式表达逻辑，【强制】 避免后续代码维护困难，请勿超过3层。
- 正例：超过3层的 if-else 的逻辑判断代码可以使用卫语句、策略模式、状态模式等来实现，其中卫语句示例如下：
```
public void today() {
if (isBusy()) {
System.out.println("change time.");
return;
}
if (isFree()) {
System.out.println("go to travel.");
return;
}
System.out.println("stay at home to learn Alibaba Java Coding Guidelines.");
return;
}
5. **【推荐】** 除常用方法（如getXxx/isXxx）等外，不要在条件判断中执行其它复杂的语句，将复杂逻辑判断的结果赋值给一个有意义的布尔变量名，以提高可读性。 说明：很多if语句内的逻辑相当复杂，阅读者需要分析条件表达式的最终结果，才能明确什么样的条件执行什么样的语句，那么，如果阅读者分析逻辑表达式错误呢？ 
- 正例： // 伪代码如下
final boolean existed = (file.open(fileName, "w") != null) && (...)|| (...);
if (existed) {
...
}
```
- 反例：
```
if ((file.open(fileName, "w") != null) && (...)|| (...)) {
...
}
```
6. **【推荐】** 循环体中的语句要考量性能，以下操作尽量移至循环体外处理，如定义对象、变量、获取数据库连接，进行不必要的try-catch操作（这个try-catch是否可以移至循环体外）。
7. **【推荐】** 避免采用取反逻辑运算符。说明：取反逻辑不利于快速理解，并且取反逻辑写法必然存在对应的正向逻辑写法。正例：使用if (x < 628)来表达x 小于628。反例：使用if (!(x >= 628))来表达x 小于628。
8. **【推荐】** 接口入参保护，这种场景常见的是用作批量操作的接口。
9. **【参考】** 下列情形，需要进行参数校验： 1） 调用频次低的方法。 2） 执行时间开销很大的方法。此情形中，参数校验时间几乎可以忽略不计，但如果因为参数错误导致中间执行回退，或者错误，那得不偿失。 3） 需要极高稳定性和可用性的方法。 4） 对外提供的开放接口，不管是RPC/API/HTTP接口。 5） 敏感权限入口。
10. **【参考】** 下列情形，不需要进行参数校验： 1） 极有可能被循环调用的方法。但在方法说明里必须注明外部参数检查要求。 2） 底层调用频度比较高的方法。毕竟是像纯净水过滤的最后一道，参数错误不太可能到底层才会暴露问题。一般DAO层与Service层都在同一个应用中，部署在同一台服务器中，所以DAO的参数校验，可以省略。 3） 被声明成private只会被自己代码所调用的方法，如果能够确定调用方法的代码传入参数已经做过检查或者肯定不会有问题，此时可以不校验参数。
## (六) 注释规约
1. **【强制】** 类、类属性、类方法的注释必须使用Javadoc规范，使用/**内容*/格式，不得使用// xxx方式。 说明：在IDE编辑窗口中，Javadoc方式会提示相关注释，生成Javadoc可以正确输出相应注释；在IDE中，工程调用方法时，不进入方法即可悬浮提示方法、参数、返回值的意义，提高阅读效率。
2. **【强制】** 所有的抽象方法（包括接口中的方法）必须要用Javadoc注释、除了返回值、参数、异常说明外，还必须指出该方法做什么事情，实现什么功能。 说明：对子类的实现要求，或者调用注意事项，请一并说明。
3. **【强制】** 所有的类都必须添加创建者和创建日期。
4. **【强制】** 方法内部单行注释，在被注释语句上方另起一行，使用//注释。方法内部多行注释使用/* */注释，注意与代码对齐。
5. **【强制】** 所有的枚举类型字段必须要有注释，说明每个数据项的用途。
6. **【推荐】** 与其“半吊子”英文来注释，不如用中文注释把问题说清楚。专有名词与关键字保持英文原文即可。 反例：“TCP连接超时”解释成“传输控制协议连接超时”，理解反而费脑筋。
7. **【推荐】** 代码修改的同时，注释也要进行相应的修改，尤其是参数、返回值、异常、核心逻辑等的修改。 说明：代码与注释更新不同步，就像路网与导航软件更新不同步一样，如果导航软件严重滞后，就失去了导航的意义。
8. **【参考】** 谨慎注释掉代码。在上方详细说明，而不是简单地注释掉。如果无用，则删除。 说明：代码被注释掉有两种可能性：1）后续会恢复此段代码逻辑。2）永久不用。前者如果没有备注信息，难以知晓注释动机。后者建议直接删掉（代码仓库保存了历史代码）。
9. **【参考】** 对于注释的要求：第一、能够准确反应设计思想和代码逻辑；第二、能够描述业务含义，使别的程序员能够迅速了解到代码背后的信息。完全没有注释的大段代码对于阅读者形同天书，注释是给自己看的，即使隔很长时间，也能清晰理解当时的思路；注释也是给继任者看的，使其能够快速接替自己的工作。
10. **【参考】** 好的命名、代码结构是自解释的，注释力求精简准确、表达到位。避免出现注释的一个极端：过多过滥的注释，代码的逻辑一旦修改，修改注释是相当大的负担。 反例：
// put elephant into fridge  
put(elephant, fridge);  
方法名put，加上两个有意义的变量名elephant和fridge，已经说明了这是在干什么，语义清晰的代码不需要额外的注释。
11. **【参考】** 特殊注释标记，请注明标记人与标记时间。注意及时处理这些标记，通过标记扫描，经常清理此类标记。线上故障有时候就是来源于这些标记处的代码。 1） 待办事宜（TODO）:（ 标记人，标记时间，[预计处理时间]） 表示需要实现，但目前还未实现的功能。这实际上是一个Javadoc的标签，目前的Javadoc还没有实现，但已经被广泛使用。只能应用于类，接口和方法（因为它是一个Javadoc标签）。 2） 错误，不能工作（FIXME）:（标记人，标记时间，[预计处理时间]） 在注释中用FIXME标记某代码是错误的，而且不能工作，需要及时纠正的情况。
# 二、异常日志  
## (一) 异常处理  
1. **【强制】** Java 类库中定义的可以通过预检查方式规避的`RuntimeException`异常不应该通过`catch` 的方式来处理，比如：`NullPointerException`，`IndexOutOfBoundsException`等等。 说明：无法通过预检查的异常除外，比如，在解析字符串形式的数字时，不得不通过`catch NumberFormatException`来实现。 **正例**：`if (obj != null) {...}` **反例**：`try { obj.method(); } catch (NullPointerException e) {…}`  
2. **【强制】** 异常不要用来做流程控制，条件控制。 说明：异常设计的初衷是解决程序运行中的各种意外情况，且异常的处理效率比条件判断方式要低很多。  
3. **【强制】**`catch`时请分清稳定代码和非稳定代码，稳定代码指的是无论如何不会出错的代码。对于非稳定代码的`catch`尽可能进行区分异常类型，再做对应的异常处理。 说明：对大段代码进行`try-catch`，使程序无法根据不同的异常做出正确的应激反应，也不利于定位问题，这是一种不负责任的表现。 **正例**：用户注册的场景中，如果用户输入非法字符，或用户名称已存在，或用户输入密码过于简单，在程序上作出分门别类的判断，并提示给用户。  
4. **【强制】** 捕获异常是为了处理它，不要捕获了却什么都不处理而抛弃之，如果不想处理它，请将该异常抛给它的调用者。最外层的业务使用者，必须处理异常，将其转化为用户可以理解的内容。  
5. **【强制】** 有`try`块放到了事务代码中，`catch`异常后，如果需要回滚事务，一定要注意手动回滚事务。  
6. **【强制】**`finally`块必须对资源对象、流对象进行关闭，有异常也要做`try-catch`。 说明：如果JDK7及以上，可以使用`try-with-resources`方式。  
7. **【强制】** 不要在`finally`块中使用`return`。说明：`finally`块中的`return`返回后方法结束执行，不会再执行`try`块中的`return`语句。  
8. **【强制】** 捕获异常与抛异常，必须是完全匹配，或者捕获异常是抛异常的父类。 说明：如果预期对方抛的是绣球，实际接到的是铅球，就会产生意外情况。  
9. **【推荐】** 方法的返回值可以为`null`，不强制返回空集合，或者空对象等，必须添加注释充分说明什么情况下会返回`null`值。 说明：本手册明确防止`NPE`是调用者的责任。即使被调用方法返回空集合或者空对象，对调用者来说，也并非高枕无忧，必须考虑到远程调用失败、序列化失败、运行时异常等场景返回`null`的情况。  
10. **【推荐】** 防止`NPE`，是程序员的基本修养，注意`NPE`产生的场景： 1）返回类型为基本数据类型，`return`包装数据类型的对象时，自动拆箱有可能产生`NPE`。 **反例**：`public int f() { return Integer对象}`， 如果为`null`，自动解箱抛`NPE`。 2） 数据库的查询结果可能为`null`。 3） 集合里的元素即使`isNotEmpty`，取出的数据元素也可能为`null`。 4） 远程调用返回对象时，一律要求进行空指针判断，防止`NPE`。 5） 对于`Session`中获取的数据，建议`NPE`检查，避免空指针。 6） 级联调用`obj.getA().getB().getC()`；一连串调用，易产生`NPE`。 **正例**：使用JDK8的`Optional`类来防止`NPE`问题。  
11. **【推荐】** 定义时区分`unchecked` / `checked` 异常，避免直接抛出`new RuntimeException()`，更不允许抛出`Exception`或者`Throwable`，应使用有业务含义的自定义异常。推荐业界已定义过的自定义异常，如：`DAOException` / `ServiceException`等。  
12. **【参考】** 对于公司外的http/api开放接口必须使用“错误码”；而应用内部推荐异常抛出；跨应用间RPC调用优先考虑使用`Result`方式，封装`isSuccess()`方法、“错误码”、“错误简短信息”。 说明：关于RPC方法返回方式使用`Result`方式的理由： 1）使用抛异常返回方式，调用方如果没有捕获到就会产生运行时错误。 2）如果不加栈信息，只是`new`自定义异常，加入自己的理解的error message，对于调用端解决问题的帮助不会太多。如果加了栈信息，在频繁调用出错的情况下，数据序列化和传输的性能损耗也是问题。  
13. **【参考】** 避免出现重复的代码（Don’t Repeat Yourself），即DRY原则。 说明：随意复制和粘贴代码，必然会导致代码的重复，在以后需要修改时，需要修改所有的副本，容易遗漏。必要时抽取共性方法，或者抽象公共类，甚至是组件化。 **正例**：一个类中有多个public方法，都需要进行数行相同的参数校验操作，这个时候请抽取：  
`private boolean checkParam(DTO dto) {...}`
## (二) 日志规约
1. **【强制】**  应用中不可直接使用日志系统（Log4j、Logback）中的API，而应依赖使用日志框架SLF4J中的API，使用门面模式的日志框架，有利于维护和各个类的日志处理方式统一。
```
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
private static final Logger logger = LoggerFactory.getLogger(Abc.class);
```
2. **【强制】** 日志文件至少保存15天，因为有些异常具备以“周”为频次发生的特点。
3. **【强制】** 应用中的扩展日志（如打点、临时监控、访问日志等）命名方式：appName_logType_logName.log。
- logType:日志类型，如stats/monitor/access等；
- logName:日志描述。 这种命名的好处：通过文件名就可知道日志文件属于什么应用，什么类型，什么目的，也有利于归类查找。
- 正例：mppserver应用中单独监控时区转换异常，如： mppserver_monitor_timeZoneConvert.log 说明：推荐对日志进行分类，如将错误日志和业务日志分开存放，便于开发人员查看，也便于通过日志对系统进行及时监控。
4. **【强制】** 对trace/debug/info级别的日志输出，必须使用条件输出形式或者使用占位符的方式。
- 说明：logger.debug("Processing trade with id: " + id + " and symbol: " + symbol); 如果日志级别是warn，上述日志不会打印，但是会执行字符串拼接操作，如果symbol是对象，会执行toString()方法，浪费了系统资源，执行了上述操作，最终日志却没有打印。
- 正例：（条件）建设采用如下方式
if (logger.isDebugEnabled()) { 
    logger.debug("Processing trade with id: " + id + " and symbol: " + symbol); 
}
- 正例：（占位符）
logger.debug("Processing trade with id: {} and symbol : {} ", id, symbol);
5. **【强制】** 避免重复打印日志，浪费磁盘空间，务必在log4j.xml中设置additivity=false。
- 正例：<logger name="com.taobao.dubbo.config" additivity="false">
6. **【强制】** 异常信息应该包括两类信息：案发现场信息和异常堆栈信息。如果不处理，那么通过关键字throws往上抛出。
- 正例：logger.error(各类参数或者对象toString() + "_" + e.getMessage(), e);
7. **【推荐】** 谨慎地记录日志。生产环境禁止输出debug日志；有选择地输出info日志；如果使用warn来记录刚上线时的业务行为信息，一定要注意日志输出量的问题，避免把服务器磁盘撑爆，并记得及时删除这些观察日志。
- 说明：大量地输出无效日志，不利于系统性能提升，也不利于快速定位错误点。记录日志时请思考：这些日志真的有人看吗？看到这条日志你能做什么？能不能给问题排查带来好处？
8. **【推荐】** 可以使用warn日志级别来记录用户输入参数错误的情况，避免用户投诉时，无所适从。如非必要，请不要在此场景打出error级别，避免频繁报警。
- 说明：注意日志输出的级别，error级别只记录系统逻辑出错、异常或者重要的错误信息。
9. **【推荐】** 尽量用英文来描述日志错误信息，如果日志中的错误信息用英文描述不清楚的话使用中文描述即可，否则容易产生歧义。国际化团队或海外部署的服务器由于字符集问题，【强制】使用全英文来注释和描述日志错误信息。
# 四、安全规约  
1. **【强制】** 隶属于用户个人的页面或者功能必须进行权限控制校验。 说明：防止没有做水平权限校验就可随意访问、修改、删除别人的数据，比如查看他人的私信内容、修改他人的订单。  
2. **【强制】** 用户敏感数据禁止直接展示，必须对展示数据进行脱敏。 说明：中国大陆个人手机号码显示为:158****9119，隐藏中间4位，防止隐私泄露。  
3. **【强制】** 用户输入的SQL参数严格使用参数绑定或者METADATA字段值限定，防止SQL注入，禁止字符串拼接SQL访问数据库。  
4. **【强制】** 用户请求传入的任何参数必须做有效性验证。 说明：忽略参数校验可能导致：  
- page size过大导致内存溢出  
- 恶意order by导致数据库慢查询  
- 任意重定向  
- SQL注入  
- 反序列化注入  
- 正则输入源串拒绝服务ReDoS  
说明：Java代码用正则来验证客户端的输入，有些正则写法验证普通用户输入没有问题，但是如果攻击人员使用的是特殊构造的字符串来验证，有可能导致死循环的结果。  
5. **【强制】** 禁止向HTML页面输出未经安全过滤或未正确转义的用户数据。  
6. **【强制】** 表单、AJAX提交必须执行CSRF安全验证。 说明：CSRF(Cross-site request forgery)跨站请求伪造是一类常见编程漏洞。对于存在CSRF漏洞的应用/网站，攻击者可以事先构造好URL，只要受害者用户一访问，后台便在用户不知情的情况下对数据库中用户参数进行相应修改。  
7. **【强制】** 在使用平台资源，譬如短信、邮件、电话、下单、支付，必须实现正确的防重放的机制，如数量限制、疲劳度控制、验证码校验，避免被滥刷而导致资损。 说明：如注册时发送验证码到手机，如果没有限制次数和频率，那么可以利用此功能骚扰到其它用户，并造成短信平台资源浪费。  
8. **【推荐】** 发贴、评论、发送即时消息等用户生成内容的场景必须实现防刷、文本内容违禁词过滤等风控策略。