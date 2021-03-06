<p align="center">
  <a href="https://getbootstrap.com/">
    <img src="https://files.cnblogs.com/files/selton/show.ico" alt="" width=72 height=72>
  </a>

  <h3 align="center">浅析 阿里巴巴 Java 开发规约</h3>
<p align="center">
    <strong>(未完成)</strong>
</p>
</p>

##contents
- [**为什么要学**](#why-use)
- [**编程规约**](#编程规约)
- [**P3C IDEA 插件**](#插件)


##why-use
我们知道,一般稍微大一点的公司,都会在系统架构设计完成之后,编码工作开始之前,给出一份属于自家公司,或是自家团队给出的编码规范文档,所有的编码工作人员都必须遵守其中的规范,避免规范不统一带来的不必要的沟通问题,而当你去到另一家公司的时候,可能又要学习另一种风格有差异的编码规范,阿里给我们带来了标准,相信用不了多久,会统一国内各java开发公司的规范,乃至击败Google,称为全球java开发者的规范

**养成良好的编程规范的作用(为何学习并养成编程风格)**  

1. 好的编码规范可以尽可能的减少一个软件的维护成本，并且几乎没有任何一个软件，在其整个生命周期中，均由最初的开发人员来维护；
2. 好的编码规范可以改善软件的可读性，可以让开发人员尽快而彻底地理解新的代码；
3. 好的编码规范可以最大限度的提高团队开发的合作效率；
4. 长期的规范性编码还可以让开发人员养成好的编码习惯，甚至锻炼出更加严谨的思维；  

**阿里java规范的作用(为何要学习阿里的java编码规范)**

就在不久前,5月17日，作为唯一的中国代表，阿里巴巴获邀加入Java全球管理组织*Java Community Process (JCP)*的最高执行委员会。

JCP是一个开放的国际组织，由Java开发者及被授权者组成，主要职能是发展和更新Java技术规范。

阿里此次能够入选JCP执行委员会主要缘于在电商、金融、物流等领域积累的丰富Java应用场景实践，让阿里巴巴有机会通过迭代式创新，将前沿Java技术应用于真实的生产环境。此外，阿里去年面向全球推出的《*阿里巴巴Java开发规约*》扫描插件，能够在Eclipse等著名开发工具中进行JAVA代码检测，极大推动了Java编程语言规范开发的进程。

此前在JCP组织当中，Java标准规范的制定主要由硅谷巨头牵头主导，此次阿里巴巴的加入，对于国内开发者、企业而言，将会使Java开发过程中容错与效率变得更高，**国内开发标准或将成为全球规范**。



##编程规约  
- [命名规约](#命名规约)
- [常量定义](#常量定义)
- [OOP规约](#OOP规约)



####命名规约

- **采用空格缩进，禁止使用tab字符。**  
> 这是Google和ali一致的规约，只不过前者是一个tab对应2个空格，后者则是4个空格。之所以不提倡tab键，是因为不同的IDE对tab键的“翻译”默认有所差异，容易因不同程序员的个性化而导致同一份代码的格式混乱。。  

- **POJO类中布尔类型的变量，都不要加is，否则部分框架解析会引起序列化错误。** 
> 定义为基本数据类型boolean isSuccess；的属性，它的方法也是isSuccess()，RPC框架在反向解析的时候，“以为”对应的属性名称是success，导致属性获取不到，进而抛出
异常。
  

- **包名统一使用小写，点分隔符之间有且仅有一个自然语义的英语单词。包名统一使用单数形式，类名若有复数含义，则可使用复数形式。**  
> 避免硬编码问题是每个程序员都应该具备的基本素养，硬编码所带来的可读性差、维护困难等问题。   

- **接口类中的方法和属性不要加任何修饰符号（public 也不要加），保持代码的简洁性**  
> 正例：接口方法签名：void f();   
反例：接口方法定义：public abstract void f();  

- **Service/DAO层方法命名规约**  
1)获取单个对象的方法用get做前缀。  
2)获取多个对象的方法用list做前缀。  
3)获取统计值的方法用count做前缀。  
4)插入的方法用save（推荐）或insert做前缀。  
5)删除的方法用remove（推荐）或delete做前缀。  
6)修改的方法用update做前缀。 

####常量定义
- **不要使用一个常量类维护所有常量，应该按常量功能进行归类，分开维护。**
如：缓存相关的常量放在类：CacheConsts下；系统配置相关的常量放在类：ConfigConsts下。
>说明：大而全的常量类，非得ctrl+f才定位到修改的常量，不利于理解，也不利于维护。


####OOP规约


- 相同参数类型，相同业务含义，才可以使用Java的可变参数，避免使用Object。

>说明：可变参数必须放置在参数列表的最后。（提倡同学们尽量不用可变参数编程）effective java中提倡慎用可变参数,在重视性能的情况下,使用可变参数需要特别小心,可变参数方法的每次调用都会导致进行一次数组分配和初始化。如果凭经验确定无法承受这一成本,但又需要可变参数的灵活性,还有一种模式可以让你如愿以偿。  
>假设确定对某个方法95%的调用会有3个或者更少的参数,就声明改方法的5个重载,每个重载方法带有0至3个普通参数,当参数的数目超过3个时,就使用一个可变参数方法:  例如: 
> 
    public void foo(){}
    public void foo(int a1){}
    public void foo(int a1,int a2){}
    public void foo(int a1,int a2,int a3){}
    public void foo(int a1,int a2,int a3,int ... rest){}
这种方法可能不太恰当,但是一旦需要它时,它可就帮上大忙了。  

>总之,在定义参数数目不定的方法时,可变参数方法是一种很方便的方式,但是它们不应该被过度滥用。如果使用不当,会产生混乱的结果。
- 构造方法里面禁止加入任何业务逻辑，如果有初始化逻辑，请放在init方法中。  

- POJO类必须写toString方法。使用工具类source> generate toString时，如果继承了另一个POJO类，注意在前面加一下super.toString。  

- 类内方法定义顺序依次是：公有方法或保护方法> 私有方法> getter/setter方法。
>说明：  
>公有方法是类的调用者和维护者最关心的方法，首屏展示最好；  
>保护方法虽然只是子类关心，也可能是“模板设计模式”下的核心方法；  
而私有方法外部一般不需要特别关心，是一
个黑盒实现；  
因为方法信息价值较低，所有Service和DAO的getter/setter方法放在类体最
后。


##插件

>**P3C是先进反潜海上巡逻机,译作猎户座,海神之子**  
阿里云栖大会最新开源的Java代码规范检查工具p3c,作用类似于CheckStyle,FindBugs的综合,是《阿里巴巴Java开发手册》的有效补充,阿里将代码规范检查插件命名为p3c，大概就是取其先进的猎杀,预防bug的能力

[Download P3C IDEA plugin](https://files.cnblogs.com/files/selton/AlibabaJavaCodingGuidelines-1.0.4.zip)  
安装步骤  
1. 点击工具栏File  
2. 点击Setting  
3. 点击Plugin  
4. 点击Install Plugin From disk  
5. 弹出对话框,找到你下载的插件  

>p3c、checkstyle都是代码规范检测工具,帮助java开发者**提高编码质量**,有效缩小菜鸟和大咖的代码差距，是少数Java开发者都应该安装的插件。