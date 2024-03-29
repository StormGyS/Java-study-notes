三. 面向对象(核心)

 3.1 面向对象概念
 3.2 类与对象的关系
 3.3 封装
 3.4 构造函数
 3.5 this关键字
 3.6 static关键字
 3.7 单例设计模式
  
  3.1 面向对象概念
   3.1.1 理解面向对象
    (1)面向对象是相对面向过程而言
    (2)面向对象和面向过程都是一种思想
    (3)面向过程:强调的是功能行为
    (4)面向对象:将功能封装进对象,强调具备了功能的对象
    (5)面向对象是基于面向过程的
  eg:用把大象装进冰箱里来理解.三步:打开冰箱,存储进冰箱,关闭冰箱.(i)面向过程就是强调打开冰箱,存储进冰箱和关闭冰箱这三个动作,也可以理解为定义了三个函      数(功能),然后再噼里啪啦的去依次执行.(ii)面向对象就是将这三个功能放进冰箱里,有了冰箱就有了这些功能,即冰箱.打开,冰箱.存储和冰箱.关闭.
  总结:面向对象将一个问题是不是简单化了(那吃饭来说),从执行者(先买菜,再烧菜,最后才能吃)转变为指挥者(我去饭店找服务员点菜,不管买菜和怎样烧菜了,直接端   上来,就可以吃了)了,所以写程序时,有对象就拿过来用,没对象我就new一个出来,把要用的功能封装进对象里,有对象就有功能了,万物皆对象.
  
  /*
  拿"人开门"来分析一下哪些是对象,哪些是对象里要有的功能?  名词提炼法
    人
    {
      开门(门)   //人具有开门这个行为,把门传进来
      {
        门.开();  //开门这个行为就调用门打开的这个功能即可 
      }
        }
    门
    {
      开(){操作门轴等;}  //开这个行为动作为什么定义在门这个事物中,因为开门这个行为是不是要操作门轴,弹簧等具体配件,这些配件都在门这个事物里边,是不是
                        //具体怎么开,门最清楚的,开这个功能就操作门轴等;即谁(对象)最清楚这个动作,就定义在谁里面.(*****)
    }
  */
  
   面向对象:三个特征:封装,继承,多态.  开发中,其实就是找对象使用,没对象,就创建一个对象.  找对象,建立对象,使用对象(涉及封装);维护对象之间的关系(涉及            继承和多态).
  
  3.2 类与对象的关系
   
   类:就是对现实生活中事物的描述.
   对象:就是这类事物,实实在在存在的个体.
   
   现实生活中的对象:张三和李四;想要描述:就是提取对象中的共性内容.对具体的抽象.描述时:这些对象的共性内容有:姓名,年龄,性别和学习java的功能.
   
   映射到java中,描述的就是class定义的类.
   具体对象就是对应java在堆内存中用new建立的实体.
   
   /*
   需求:描述汽车(颜色,轮胎数,运行). 描述事物其实就是在描述事物的属性和行为.
   属性对应的是类中的变量,行为对应的是类中的函数(方法).
   其实定义类,就是在描述事物,就是在定义属性和行为,属性和行为共同成为类中的成员(成员变量和成员方法).
   
   class Car    //描述车这类事物                                                                ---------->图纸
   {
       //描述颜色
       String color="红色";//字母,数字和符号用char,汉字用String.
       //描述轮胎数
       int num=4;
       //运行行为
       void run()
       {
           System.out.println(color+" "+num);
       }
   }
   
   class CarDemo
   {
       public static void main(String[] args)
       {
           //java中通过new操作符来建立对象,其实就是在堆内存中产生一个实体
           //c就是一个类类型变量,类类型变量c(在栈内存中,c放的是对象首地址)指向对象(在堆内存中),就认为c是一个对象
           Car c=new Car();                                                                    ----------->生产汽车        
           //改变车颜色为蓝色,.指挥该对象做使用,在java中指挥方式是: 对象.对象成员
           c.color="biue";
           //运行
           c.run();
           Car c1=c; //假设c中存的堆内存地址为0x0097,c在栈内存中的地址是0x0867,则c1里存的是0x0097,c1也指向堆中的对象.     
       }
   }
   */
   
   当然也可以在Car类中写主函数,不建议,有多个类,主函数写在一个类中.
   
   成员变量和局部变量: (i)作用范围:成员变量作用于整个类中.局部变量作用于函数中或者语句中.  (ii)在内存中的位置:成员变量在堆内存中,因为对象的存在,
   才在内存中存在(通过new,才有了color,num等).局部变量存在于栈内存中.
   
  3.2.6 匿名对象
   (1)匿名对象是对象的简化形式 eg: new Car(); //这就是匿名对象,即不给对象起名
   (2)匿名对象的两种使用情况:
    (i)当对对象方法仅进行一次调用时 eg: new Car().run();//我就想打印颜色和轮胎数,new Car()就相当于c.
       那么, new Car().color="blue";new Car().num=5;new Car().run();//当这三句话执行完之后,任然打印红色和4个轮胎,这是因为每执行前面一句话
       之后,就建立一个对象,执行完之后就是垃圾了,不是在操作同一个对象.
    (ii)为了节省写代码时间,提高编程效率,直接来 show(new Car());//show方法可以改变车颜色和轮胎数,在主函数中,这句话将调用show方法,new Car()这个
       新建立的对象作为实际参数传给形参使用.
       
 3.3 封装
    先来看一个例子-主机箱,主机箱里有芯片,电路线和内存等乱七八糟的东西对吧,拿个机箱壳子把这些东西都装里去,你看不见,透明的,外壳给你留几个孔,插头孔,里面的东西你管不着,好了.
    封装:是指隐藏(只能看到机箱壳子)对象(主机)的属性(主板和内存等)和实现细节(线路之间咋连得),仅对外提供公共访问方式(机箱壳子是不是给你留了几个孔,
         对吧,你拿着鼠标键盘往里一插,直接用就完事了.)
    好处:便于使用(插上就能用),提高重用性(谁用插上就行了),提高安全性(是不是有了外壳防止你拿个螺丝刀,就破坏了线路),将变化隔离(机箱内部各元件如何使用
    和运行与你无瓜.)
    封装的原则:  (i)将不需要对外提供的内容都隐藏起来  (ii)把属性(比如age)都隐藏,提供公共方法(比如set和age)对其访问.
    函数就是最小的封装体,类也是封装体.放大就有包,还有框架是由几百或几千个类组成,拿来用就行了.   
    /*
    private:私有,权限修饰符:用于修饰类中的成员(包括变量和方法),私有只在本类中有效.
    常用之一:将成员变量私有化,对外提供对应的set成员变量名,get成员变量名方法对其进行访问,提高对数据访问的安全性.
    注意:私有仅仅是封装的一种表现形式.
    eg:在person类中将age私有化(即private int age;),那么在main函数中,用 对象.age 就不能直接进行访问了.那就可以利用上面说的定义两种方法set(设置)和
    get(获取)进行访问,具体如下:
    class Person
    {
        private int age;
        public void setAge(int a)
        {
            if(a>0&&a<100)
                {age=a;}
            else
                {System.out.println("error!")}
        }
        public int getAge()
        {
            return age;
        }
        void speak()  //仅仅为打印,所以为void,没有形参是因为这个函数在执行过程中没有未知变量要参与运算(*****)
        {
            System.out.println("age="+age);
        }
    }
    ...
    {main
    {
        Person p=new Person();
        p.age=20;//错误
        p.setAge(20); //age为20
        p.speak();
    }
    }    
    之所以将属性age私有化,就是为了防止直接利用p.age进行访问,将其赋值为-20,对于年龄这显然不对,将其私有化,再提供公共的set和get访问方式(这里的公共
    的就是用public权限修饰符来修饰这两个方法),就是可以在访问方式中加入逻辑判断等语句,排除掉赋值为-20的可能性,提高代码的健壮性(eg:对于年龄来说,赋
    值-20就是非法的).   
    注意:记住凡是set打头的方法的返回值类型肯定为void,set什么东西要带参数,而get仅是获取,没有参数,return返回的类型与变量一致.看到类中有setxxx,
    getxxx就肯定有一个私有属性xxx.
    */
    
 3.4 构造函数
 
  特点:(1)函数名与类名相同 (2)不写返回值类型 (3)不可以写return语句 但是可以用修饰符,比如私有
  作用:给对象进行初始化
  注意:(1)默认构造函数的特点 (2)多个构造函数以重载的形式存在
  
  /*
  拿 人 举例
  class Person  
  {
      private String name; //养成习惯要加private
      //注意到没名字的孩子哭,有名字的孩子也哭,于是产生了以下代码,叫做 构造代码块 作用就是给对象初始化,与构造函数的区别:对象一建立,构造代码块就执行         //了,去给所有的对象初始化;然后再找对应形参的构造函数去执行,对应形参的构造函数分别给自己对应的对象初始化;即构造代码块里的是不同对象的共性内容. 
      {
          cry();
      }
      Person()  //符合特点(1)和(2)       -------当不定义构造函数时,系统默认生成Person(){}构造函数     --------没名字孩子哭
      {
          cry(); //符合(3)    我们知道人一生下来就会哭,所以对对象p进行了哭的初始化,故符合作用
      }
      Person(String n)  //加上参数,以重载的形式存在                                                 --------有名字孩子哭
      {
          name=n;
          System.out.println("name="+name);
          cry();
      }
      public void cry()  //一般函数,且定义为public
      {
           System.out.println("cry");  
      }
  }
  class PersonDemo
  {
      public static void main(String[] args)
      {
          Person p=new Person();  //新建一个对象,当执行完本语句后,就可打印cry,不需要语句p.Person();
          Person p1=new Person("zhangsan"); //执行本语句,又又又新建对象的同时,去找Person类里的构造函数Person(String n),将zhangsan传给n
      }
  }
  */
  
  总结:构造函数与一般函数的区别
  (i)写法格式不同
  (ii)运行上不同: 构造函数在对象一建立就运行,给对象初始化,具体要不要写形参根据是否有未知参数参与运算,且只运行一次
                 一般函数是对象调用才执行,是给对象添加对象具备的功能,可以被对象多次调用
           
  定义构造函数的场景:当分析事物时,该事物具备一些特定的特征或者行为,那么将这些内容定义在构造函数中.
  
  定义了类,只有在main函数中,new一个对象,类中的内容才有可能被执行(属性肯定被建立在堆内存中,且有初始化值;方法要被调用[构造除外]才执行),要注意执行顺序.
  
 3.5 this关键字
 
  this关键字:
  用法一就是区分同名变量,代表本类中的对象,具体就代表本函数所属对象的引用
  上面的构造函数Person(String n){name=n;}是不是发现n是字符串,但是他到底代表什么,不知道,阅读性阅读性阅读性极差,如果将n改为name就一目了然了,但是有问   题了,我们知道构造函数Person中的String name是局部变量,而name=name;语句中的左端name是对象中的name(注意这里左端的name不是图纸成员变量privata
   String name;里的name,左端的name是存在于堆内存新建对象里的name,要区别),左右都是name,不作任何处理,新建p1对象时,不能实现赋值,即name为null,为了解   决这个问题,为了以示区分成员变量和局部变量,加上this.关键字,即this.name=name;就可实现赋值了.此处this就是p1.说白了用this就是为了区分同名情况.
   
   this关键字的应用:
   需求:比较是否是同龄人
   Person类中:
   public boolean compare(Person p)
   {
       return this.age==p.age;  //(i)执行main函数时,运行此语句,this就是p1,p就是p2; (ii)别搞if...else了,相等就返回true,不等就返回false,直接                                   //return就完事了.
   }
   main函数中:
   打印 p1.compare(p2);
   //分析上面代码:比较是否是即真和假用boolean合理,传的形参是Person p,为什么不是int age或者Person p1,Person p2?(i)我们将compare方法定义在Person
   //类中,new了p1和p2对象,有了对象p1,是不是就可以调用方法了,现在我们学了面向对象,比较年龄,对象中有年龄属性,是不是有了对象就可以了,不用考虑年龄了,
   //故不传int age;那么为什么不传两个对象,是不是这是因为p1(或者p2)对象有了age属性和compare方法了,我拿p1(或者p2)的compare方法与p2(或者p1)这个对象
   //作比较就可以了,所以传一个对象就可以了.面向对象面向对象就是不管是使用属性还是方法都是对象打头(*****).
   
   用法二: this关键字在构造函数之间的调用
   再在Person类中定义一个构造函数
   Person(String name,int age)
   {
       this.name=name;  //(m)
       this.age=age;
   }
   //分析:是不是两个构造函数里都有语句this.name=name,就重复了,我们知道在一般函数间来个调用,即Person(name).但是构造函数间的调用必须要用this语句,
   即将语句(m)改为this(name);即可.注意this语句必须必须必须要写在第一行.
   
   注意:记住一般函数不能直接调用构造函数,因为this语句不能用于一般函数中,只能用于构造函数之间.但是this关键字能用于一般函数中,即应用.
  
 3.6 static(静态)关键字
  
  (1)用于修饰成员(成员变量和成员函数)
  (2)被修饰后的成员具备以下特点:
   (i)随着类的加载而加载  也就是说随着类的消失而消失,生命周期最长(与类共存亡)
   (ii)优先于对象存在  静态成员先存在,对象后存在
   (iii)被所有对象所共享
   (iv)可以直接被类名调用 类名.静态成员  当然也可以被对象调用,本来非静态成员就是被对象所调用的.
  (3)使用注意:
   (i)静态方法只能访问静态成员  非静态即可以访问静态,也可以访问非静态
   (ii)静态方法中不可以写this,super关键字  因为静态优先于对象存在,this代表对象
   (iii)主函数是静态的 
  (4)实例变量(成员变量)和类变量(静态变量)的区别:
   (i)存放位置: 类变量随着类的加载而存在于方法区(共享区,数据区)
               实例变量随着对象的建立而存在于堆内存中
   (ii)生命周期: 类变量生命周期最长,随着类的消失而消失
                实例变量生命周期随着对象的消失而消失
  (5)利弊:
   (i)利:对对象的共享数据进行单独空间的存储,节省空间,没有必要每一个对象中都存储一份
   (ii)弊:生命周期过长.访问出现局限性.(静态虽好,只能访问静态) 
  /*
  用下面例子理解
  class Person
  {
      String name;  //名字为对象特有,不能用static
      static String country="CN";  //国籍为共享属性,定义为static
      public static void speak()
      {
          System.out.println("0.0"+country);   //将country换为name编译试试
      }     
  }
  class StaticDemo
  {
      public static void main(String[] args)
      {
          Person.speak(); //不创建对象,直接用类名调用
      }
  }
  */
  
  /*
  需求:分析主函数 public static void main(String[] args)
  主函数:是一个特殊的函数,作为程序的入口,可以被jvm调用
  主函数的定义:
  public:代表着该函数访问权限是最大的
  static:代表着主函数随着类的加载就已经存在了
  void:主函数没有具体的返回值(换成int,jvm调用主函数,返回一个整数给jvm是不是不合适啊)
  main:不是关键字,但是是一个特殊的单词,可以被jvm识别
  (String[] args):参数为字符串类型的数组,名为args,是arguments(参数)的缩写,当然也可以换个其他名字,比如x
  jvm调用主函数时,传的是什么?长度多大? 打印args和args.length看看. 显示一个数组实体,长度为0;
  主函数是固定格式:jvm识别
  jvm调用主函数时,传入的是 new String[0].
  拓展:想要往主函数里传值 在运行字节码文件时,加入即可 eg:java MainTest hehe haha  打印args[0] args.length 输出hehe 2.
  不想在Dos窗口里输入hehe haha,可以定义两个类,分别有一个主函数,类1中定义字符串数组,类2中打印,类1中来个 类2.main(arr);//main是被static定义的
  //当然能用类名调用,即可以学习使用static,又可以往main函数中传值(String类型).
  
  //调用主函数
  public class MainTest
  {
      public static void main(String[] args)
      {
          String[] arr={"haha","hehe","heihei"};
          MainDemo.main(arr); //调用类MainDemo中的主函数main,实现打印数组arr.
      }
  }
  class MainDemo
  {
      public static void main(String[] args)
      {
          for(int i=0;i<args.length;i++)
          {
              System.out.println(args[i]);
          }
      }
  } 
  */
  
 (6)什么时候使用static?
    定义静态变量:当对象中出现共享数据时,该数据被静态所修饰;对象中的特有数据要定义为非静态存在于堆内存中.
    定义静态函数:当功能内部没有访问到非静态数据时,就可以定义为静态的.(因为静态会被存于方法区中,优先于对象,所以静态函数内部不能有特有数据[eg:不能访问
    对象的name数据]
    
 (7)先讲一个小插曲:在同一个java文件中,写ArrayTool类(用于产生对象)和ArrayToolDemo类(写主函数的类),编译ArrayTool文件,就产生ArrayToolDemo和
    ArrayTool字节码文件,运行ArrayToolDemo即可.由于每一个应用程序(eg:ArrayToolDemo1和ArrayToolDemo2)中都有共性的功能(eg:都要求最值和排序)
    可以将这些功能进行抽取,独立封装,以便复用(eg:就是将求最值和排序放在ArrayTool类中,再作为一个独立的java程序,而ArrayToolDemo类又作为一个java
    程序;不管是用javac先编译ArrayTool再编译ArrayToolDemo;还是直接编译ArrayToolDemo.java文件,都可产生ArrayTool和ArrayToolDemo字节码文件
    最后java ArrayToolDemo即可.)
    static的应用:虽然可以通过建立ArrayTool的对象使用这些工具方法,对数组进行操作(求最值和排序),发现了问题:
    (i)对象是用于封装数据的,可是ArrayTool对象并未封装特有数据.
    (ii)操作数组的每一个方法都没有用到ArrayTool对象中的特有数据.
    这时考虑,为了让程序更严谨,是不需要对象的,可以将ArrayTool中的方法定义为static,方便使用,直接通过类名调用即可.
    但是该类还是可以被其他程序建立对象的,为了更严谨,强制让该类不能建立对象,可以在(eg:ArrayTool类)中将构造函数私有化.
    当然,选择和冒泡排序都要swap()函数,我就可以将其private,不需要暴露给外界,把他藏起来(即private static void swap()),只需要提供要使用的函数.
    习题:求数组[3,2,87,43,1,68]的最值和排序?
    情景:我写好ArrayToolDemo.java文件和ArrayTool.java文件;现在另一个人只写好了ArrayToolDemo.java文件,要我的ArrayTool字节码文件直接去使用,
         他直接将类文件ArrayTool存于c:\myclass目录下,如果直接编译他写的ArrayToolDemo.java文件,会报错,因为他的目录下没有ArrayTool类文件,
         要告诉jvm去找,即set classpath=c:\myclass,再编译,通过后,运行ArrayToolDemo类文件,又报错,因为jvm去找设置路径下的ArrayToolDemo类文件去执行
         但是设置路径下没有ArrayToolDemo类文件,所以设置路径正确的应为现在当前路径下找,没有再去设置的下去找 set classpath=.;c:\myclass 回车,直接运行
         即可(无需编译了,因为都有了两个字节码文件了).
    上面情境中,你会用(ArrayTool)类文件了吗?不,你不会,因为你根本不知道里面写的是啥?于是就有了下面:
    程序的说明(帮助)文档,可以给上面的ArrayTool.java文件搞一个说明文档,即使用文档注释和工具javadoc提取文档注释生成网页.但是必须要被public或protected
    修饰.
    eg:给类说明
    /**
    这是一个可以提供求最值和排序的工具类
    @author 张三
    @version v1.1
    */
    public class ArrayTool
    {
    /**
    该功能可以对数组求最大值
    @param arr 接收一个int类型的数组
    @return    返回该数组的最大值
    */
    public static int getMax(int[] arr)
    {}
    ......
    /**
    写了也不被提取,因为是private,交换不需要暴露,故隐藏起来就行.
    对数组元素位置进行置换
    @param arr 接收一个int类型数组
    @param a   对元素位置进行置换
    @param b  对元素位置进行置换   
    */
    private static void swap(int[] arr,int a,int b)
    {}
    }
  注:此类会被系统默认生成一个构造函数,而默认的构造函数的权限(public或private)与所属类一致.
  上面写完文档注释后,在Dos窗口下 javadoc -d 指定文档注释所生成的网页文件的存放目录 -author -version xxx.java
  eg:javadoc -d myhelp -author -version ArrayTool.java 回车即可.
  注:-d:指目录   -author -version可以不写   然后在所指定的目录下查看双击 index.html 即可
     形成的说明文档就是程序的API(应用程序接口)说明帮助文档,当然所使用的jdk也提供了API,里面有很多工具可以直接使用,里面有很多的类,类又存放在不同的包中,
     常见的lang包中就有经常使用的输出打印类System,天天写的System.out.println(),而且里面类中的方法全是静态的,不用创建对象就可以使用,非常方便,之前学的排      序,查找方法里面都有,直接拿来用就行,所以说你不懂算法可以,你会看API,使用API里的工具就o了.
  
  /*
  静态代码块
  格式:
  static
  {
      静态代码块中的执行语句;
  }
  特点:随着类的加载而执行,只执行一次,并优先于主函数运行.
      使用于不需要创建对象时,给类进行初始化.
  class StaticCode
  {
      static
      {
          System.out.println("a");
      }
  }
  class StaticCodeDemo          //运行(java)该类时,该类被加载进内存,所以会打印 b c a over,为什么不是打印bcaaover,创建多个对象也不行,
  {                             //因为静态代码块只执行一次.
       static
      {
          System.out.println("b");
      }
      public static void main(String[] args)
      {
          new StaticCode();
          new StaticCode();
          System.out.println("over");       
      }
       static
      {
          System.out.println("c");
      }
  }
  打印b c a over
  
  class StaticCode
  {
      int num=9;
      StaticCode()  //构造函数
      {
          System.out.println("a"); 
      }
      static     //静态代码块
      {
          System.out.println("b");
      }
      {     //构造代码块
          System.out.println("c"+this.num);
      }
       StaticCode(int x) //构造函数重载
      {
          System.out.println("d"); 
      }   
  }
  class StaticCodeDemo  
  {
       public static void main(String[] args)
      {
            new StaticCode(4);   
      }
  }
  打印b c d
  拓展:在静态代码块中加上this.num不可以,那么在构造代码块中加this.num可以吗?可以,打印b c9 d
  */
  
  /*
  对象的初始化过程: Person p =new Person("zhangsan",20);//执行该语句会做下面的步骤
  (i)因为new用到了Person.class,所以会先找到Person.class文件并加载到内存中;
  (ii)执行该类中的static代码块,如果有的话,给Person类进行初始化;
  (iii)在堆内存中开辟空间,分配内存地址;
  (iv)在堆内存中建立对象的特有属性,并进行默认初始化;
  (v)对对象进行显示初始化;
  (vi)对对象进行构造代码块初始化;
  (vii)对对象进行对应的构造函数初始化;
  (viii)将内存地址赋给栈内存中的p变量.
  */
  
3.7 单例设计模式
 先来看一个例子,讲有张三,李四和王五三人,只有张三有一百块钱,三个人分别想买可乐,雪碧和冰红茶,好了,没花之前有一百块,张三买了可乐,钱就只剩下97了,到了李四
 使用的时候就只有97了,只能用97元钱了,李四买完雪碧,到了王五使用的时候钱就只能剩90了.
 设计模式:解决某一类问题最行之有效的方法.
 java中有23种设计模式.
 先学习其中一种: 单例设计模式:解决一个类在内存中只能存在一个对象.
 想要保证对象唯一:
 (i)为了避免其他程序建立该类对象,就要先禁止其他程序建立该对象.
    其他程序之所以能建立本类对象,是因为系统默认生成构造函数,禁止只需要私有化构造函数即可,这样其他程序就不能建立对象了.
 (ii)为了让其他程序可以访问该类对象,就需要在本类中自定义建立一个对象;
 (iii)为了方便其他程序访问本类对象,就需要对外提供访问方式.
 代码提现:
 class Single  //单例
 {
     private Single(){} //函数体可写可不写,就是对本类对象进行初始化的        由于用了private,禁止建立对象了             -------对应(i)
     private static Single s=new Single(); //创建本类对象,以便其他程序使用该类的唯一对象                              -------对应(ii)
     public static Single getInstance()  //对外提供访问方式  由于不能创建对象调用该方法了,只能用类名调用,故用static     -------对应(iii)
     {
         return s; //返回变量s所指向的new Single()对象的堆内存地址,如0x0045
     }    
 }
 好了,其他程序要想使用本类对象,见下面:
 ......
 main()
 {   Single s1=Single.getInstance();//通过类名调用方法返回0x0045赋给s1.
     Single s2=Single.getInstance();//s2也指向同一个对象,即值为0x0045.
 }
 注:根据实际情况,类名Single可换为xxx.
 上面的代码提现是一开始就建立对象,对对象进行初始化,很饥渴,一开始就要有对象,称为--->饿汉式.
 还有一种体现,就是我很懒,等我有需要的时候(啥是需要时候,就是在其他程序用类名调用方法获得本类对象时),才想要建立对象,称为--->懒汉式.
 class Single
 {
     private static Single s=null;  //很懒,现在不想要对象,s不指向对象new Single().
     private Single(){}
     public static Single getInstance()
     {
         if(s==null)
             s=new Single;
         return s;
     }
 }
 Single s1=Single.getInstance(); //当执行到Single类时,调用方法,此时s不指向对象,地址为空,如果为空,建立new Single()对象,s指向他,再返回s所存对象地址
                                 //给s1,s1指向new Single()对象.
 开发中玩单例一般使用饿汉式.
                       
