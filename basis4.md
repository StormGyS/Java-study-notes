四.继承

 4.1 继承的概述
 4.2 继承的特点
 4.3 super关键字
 4.4 函数覆盖
 4.5 子类的实例化过程
 4.6 final关键字
 4.7 抽象类
 4.8 接口
 
  4.1 继承的概述
  
   (1)先来看一个实例,student类与worker类,他们都有姓名和年龄,也分别有study()功能和work()功能;我们之前学习了把每个学生对象的共性提取出来,抽象成为
   student类,现在student类与worker类也有了共性,我们也把它们提取出来抽象成为一个新的类,叫person类,让类与类之间产生(eg:继承家产)关系.
   即:
   class person   //父类或超类
   {
       String name;
       int age;
   }
   class student extends person //子类继承父类成员
   {
       public void study(){}
   }
   class worker extends person //子类继承父类成员
   {
       public void work(){}
   }
   /*
   从上面可以得出
   
  4.2 继承的特点 
   (i)提高了代码的复用性(少些代码)
   (ii)使类与类之间产生了关系,有了这些关系,于是有了多态这一特性
   注意:不能随便使用extends,不能因为想用你的东西,就喊一声爹吧,这就不太合适了.
   */
   
   java中,只支持单继承,不支持多继承,支持多层继承.
    (i)单继承说白了就是一个孩子只能有一个父亲,拿上面的说就是student类继承了person类,就不能继承其他类了.
    (ii)不支持多继承是因为,如果一个子类同时有两个父类,而父类中都有相同的函数名,不同的函数功能时,当创建子类对象时,去调用父类功能时,不知道要执行
    哪个功能.
    (iii)支持多层继承,说白了就是孩子有父亲,父亲有父亲,孩子有爷爷,组成继承体系.那么问题来了如何去使用继承体系里的功能,一句话就是,查阅父类功能,
    建立子类对象去使用功能(包括父类的共性功能和子类的特有功能).
    
   聚集关系:
    分析类与类之间的关系不一定都是继承关系,还有聚集关系.啥是聚集关系,又分为聚合和组合,这两个是以事物间的紧密联系程度划分的.
    聚合: eg:球队里有许多球员,球员是球队中的一员.
    组合: eg:手是身体的一部分,心脏也是身体的一部分.
    显然组合比聚合形容事物间的关系更紧密.
    
 4.3 super关键字
  this与super(超)要联系起来,this最常用的就是区分局部变量与新建对象中的属性同名情况.而super也大致相同.
  使用了extends出现了子父类之后,类中的成员有什么特点?
  类中成员:(i)变量 (ii)函数 (iii)构造函数
  (i)变量
   如果子父类中出现非私有的同名成员变量时,子类方法想要访问本类中的变量,用this.变量名;子类方法想要访问父类中的同名变量,用super.变量名;
   super与this使用几乎一致,this代表本类对象的引用,super代表父类对象的引用.
   注:一般情况下父类有了该变量,子类不会再定义同名变量了.
 
  4.4 函数覆盖
   (ii)函数
    当子类出现和父类一模一样(包括返回值类型和参数)时,子类创建对象调用该函数时,只会运行子类函数的内容,这种情况是函数的另一个特性:重写(覆盖).
    利用重写特性可以对子类函数进行功能扩展,完善子类功能的特有功能内容.
    class Tel  //第一代电话
    {
        void show() //方法1
        {
            System .out.println("number"); //打印号码
        }
    }
     class NewTel extends Tel  //第二代电话
    {
        void show() //方法2
        {
            System .out.println("number"); //打印号码
            System .out.println("name"); //打印姓名
            System .out.println("picture"); //打印头像      
        }
    }
    /*
    分析:(a)当子类建立对象调用show方法,执行方法2,叫做覆盖;二代手机进行重写,拓展了函数内容.
        (b)子父类都出现了打印number,应该对其进行优化,父类show方法有了功能内容,直接调用即可.
           super.show(); //super是父类引用,如果写成show()或者是this.show(),会死循环,要注意.
        (c)覆盖: 子类覆盖父类,必须保证子类权限大于等于父类权限,才可以覆盖,否则编译失败.
                 静态只能覆盖静态.
        (d)权限:public private 不加这两个关键字,是默认权限,介于两者之间.
        (e)注意:父类搞一个函数show,将其private,子类也搞个一模一样的函数show,将其public或者默认权限,这叫覆盖吗?不,这不是覆盖,因为父类私有化了,
               子类都不知道有其成员(变量和函数)了,无法覆盖.
    */
    
   4.5 子类的实例化过程
    (iii)构造函数
     首先肯定不存在覆盖了,因为子父类的构造函数名就不一样了.
     当子类继承父类时,在对子类对象初始化时,父类的构造函数也会运行.因为子类的构造函数默认第一行有一条隐式的语句 super(); //会运行父类中空参数的构造函数
     //对子类对象做初始化,即先父初始化再子初始化,而且子类中所有的构造函数(空参和有参)默认第一行都是super();
     区分 super. 与 super() 
     为什么子类一定要访问父类中的构造函数?
     因为父类中的数据子类可以直接获取,所以子类对象在建立并初始化时,需要先查看父类是如何对这些数据进行初始化的.
     如果要访问父类中指定(带参)的构造函数,可以通过手动定义super语句的方式来指定.
     注意:super语句手动定义时,一定要在子类构造函数内的第一行.且子类的某一个构造函数不能同时出现this();和super();因为都要在第一行.因为初始化要先做.
     class Person
     {
         String name;
         Person()
         {
             System.out.println("person");
         }
         Person(String name)
         {
             this.name=name;
         }   
     }
     class Student extends Person
     {
         Student()
         {
             //默认Person()
             System.out.println("student");
         }
         Student(int x)
         {
             System.out.println(x); //运行到这会打印person 4(假设传的是4),因为这句话前默认super();
         }
         Student(String name)
         {
             //因为父类的带参构造函数已经实现建立对象进行赋值了,所以直接调用即可
             super(name); //运行这句话,会调用父类Person(String name),对name赋值
         }
     }
     class ZiLeiInstance
     {
         public static void main(String[] args)
         {
             Student s1=new Student();  
             Student s2=new Student("zhangsan");  
             System.out.println("name="+s2.name);
         }
     }
     //打印person 
           student
     //打印name=zhangsan
     结论:
     (a)子类中的所有构造函数,默认都会访问父类中空参数的构造函数,除了指定super语句.
     (b)因为子类每一个构造函数内的第一行都有一句隐式super();当父类中没有空参数的构造函数时,子类必须手动通过super语句形式来指定
        要访问父类的构造函数.
     (c)当然,子类的构造函数第一行也可以手动指定this语句来访问本类中的构造函数,不用担心该构造函数访问不到父类的构造函数,因为子类
        中至少会有一个构造函数会访问到父类中的构造函数,即间接访问.
     (d)子类一实例化就会走父类.
     
  4.6 final关键字
   final:最终
   (1)final可以修饰类,方法和变量;
   (2)final修饰的类不可以被继承;
   (3)final修饰的方法不可以被覆盖(复写);
   (4)final修饰的变量(包括成员变量和局部变量)是一个常量,只能被赋值一次,且变量名要取得有意义,便于阅读,且所有字母大写,如果由多单词组成,每个单词
   字母都大写,并用下划线连接.
   (5)内部类只能访问被final修饰的局部变量;
   注:现在可以修饰类的关键字学了public和final.
   
  4.7 抽象类
   先看一个例子,有基础班学生类和高级班学生类,他们都可以学习,但是学习的内容不同,即
   class BaseStudent extends Student  //向上抽取相同功能,不抽取内容后再继承父类
   {
       void study()
       {
           System.out.println("study base");
       }
   }
   class AdvancedStudent extends Student
   {
       void study()
       {
           System.out.println("study advanced");
       }
   }
   /*
   分析上面两个类,是不是都有相同的功能,但是功能主体不同;当然也可以用子类继承父类,在父类中定义,子类实现复写;但是比较麻烦,要定义父类的功能和功能主体;
   于是,有了抽象类;任然可以向上提取,但是但是但是,只提取功能定义,而不提取功能主体;抽象:看不懂.用abstract(抽象)来修饰.即
   abstract class Student
   {
       abstract void study(); //没有大括号,即没有功能主体,就用;表示结束.
   } 
   总结:抽象类的特点
   (i)抽象方法一定在抽象类中;
   (ii)抽象方法和抽象类必须被abstr修饰;
   (iii)抽象类不可以用new创建对象,因为对象调用抽象方法无意义;
   (iv)抽象类中的抽象方法要被使用,必须由子类复写所有抽象方法后,建立子类对象调用;
       如果子类只复写了部分抽象方法,那么该子类还是一个抽象类.eg:现在父类里还有一个study1();子类继承了父类,相当于子类也有一个抽象方法study1();
       这时子类要加上abstract修饰.当然在子类中复写如 void study1(){} //即有函数主体了,但主体里啥也没有,这也是复写.
   (v)抽象类中也可以没有抽象方法(此时就是为了不让你建立对象,即实例化使用),当然一般方法就正常提取(既有函数,又有函数体)也可以在抽象类中存在(不加abstract).
   */
   
   练习1.某一个公司,有员工和经理,他们都有姓名,工号和工资,但是经理有奖金;他们都要工作;要求用继承去实现他们.
    abstract class Staff
    { 
        //共有属性设计
        private String name;
        private String id;
        private int pay;
        //构造函数很重要,提供了对象在初始化时的属性.要学会设计一个好的好的好的构造函数,学习下面方式
        Staff(String name,String id,int pay) //设计带参构造函数
        {
            this.name=name;
            this.id=id;
            this.pay=pay;
        }
        //都要工作?是不是工作内容都不同应该这样设计
        public abstract void work();
    }
    class CommonStaff extends Staff
    {
        CommonStaff(String name,String id,int pay)
        {
            super(name,id,pay);
        }
        void work(){}
    }
    class Manager extends Staff
    {
        private int bonus;
        Manager(String name,String id,int pay,int bonus)
        {
            super(name,id,pay);
            this.bonus=bonus;
        }
        void work(){}
    }
    ...
    
   练习2.获取一段程序的运行时间.
   没分析前,先来介绍一下啥是模板方法设计模式?
   模板方法:在类中设计功能时,一部分是确定的,另一部分是不确定的,当确定的部分使用到了不确定的部分时,这时就将不确定的部分暴露出去,由该类的子类去完成.
   注:不确定的部分是否就一定是抽象的,不需要,也可以父类中有完整的函数,子类覆盖也行;定义父类不确定的为抽象,那就在子类复写.
   思路:先获取程序未运行时的时间,程序执行完了,再获取执行后的时间,打印两者的差即可.
       如何获取:jdk提供了类库中有方法currentTimeMillis().
   abstract class GetTime
   {
       public final void getTime()
       {
       //获取未运行时间
       long start=System.currentTimeMillis();
       //要执行的程序,注意这里是不是不知道运行哪段代码,根据 模板方法设计模式 思想,先暴露出去,由子类完成,再调用即可
       code();
       long end=System.currentTimeMillis();
       System.out.println("time="+(end-start));
       }
       public abstract void code(); //暴露出去    
   }
   class Code extends GetTime
   {
       public void code()  //求循环打印i的运行时间
       {
           for(int i=1;i<100;i++)
           {
               System.out.print(i);
           }
       }    
   }
   class Time
   {
       public static void main(String[] args)
       {
           Code c=new Code();
           c.getTime();
       }
   }
   /*
   分析:我们称类GetTime中的getTime方法就是模板方法,他可以解决求某段程序的运行时间.可以解决某一类问题.
   而code()方法就是不确定的部分,这里不确定的就是求哪段程序运行时间,暴露出去,由子类完成.
   */
   
 4.8 接口
  接口:初期理解,就把他认为是一个特殊的抽象类.
      抽象类中有抽象函数和一般函数,如果抽象类中的方法都是抽象的,那么该类可以通过接口的形式来表示.
  class用于定义类;
  interface用于定义接口;
  格式:
   (i)接口中常见的定义就是常量和抽象方法;
   (ii)接口中的成员都有固定的修饰符: 常量 public static final 即全局静态常量; 抽象方法 public abstract;
  记住:接口中的成员都是public的;
  注:接口是不可以创建对象的,因为有抽象方法;所以想使用接口里的方法就需要被子类实现,子类对接口中的抽象方法完全覆盖后,子类才可以实例化,否则,子类要加
     abstract修饰,子类是一个抽象类.
  interface Inter  //给接口起个名为Inter
  {
      public static final int NUM=3.14;
      public abstract void study();
  }
  class Test implements Inter  //类Test是子类,这里不使用继承了,而是使用关键字implements(实现)接口
  {
      public void study(){} //复写study函数 
  }
  ......
  //调用NUM可以有三种方式,即新建对象t.NUM或Test.NUM或Inter.NUM;
  //接口的出现将"多继承"通过另一种形式体现出来,即"多实现".
  //类与类之间是继承关系
  //类与接口之间是实现关系,而且可以多实现
  class Test implement InterA,InterB,InterC
  //而且可以先继承,再实现
  class Test extends Test0 implements Inter
  //接口与接口之间是继承关系,而且可以多继承,因为没方法体,即使继承同一方法,复写该方法,两个都覆盖了,不冲突.
  interface C extends A,B  
  
 (1)接口的特点:
  (i)接口是对外暴露的规则 对外暴露就是任何一个子类可以实现它,规则就是接口里规定了你子类要实现的方法
  (ii)接口是程序的功能拓展
  (iii)接口可以用来多实现
  (iv)类与接口之间是实现关系,而且一个类可以继承一个类的同时实现多个接口
  (v)接口与接口之间可以有继承关系
 /*
 问题来了,现在我们知道抽象类和接口都可以放抽象方法,那么什么时候该定义抽象类,什么时候定义接口?是不是只要我定义的都是抽象方法,我就拿接口
 来定义?不是,只要记住这句话 基本功能定义在类中,拓展功能定义在接口中. eg:现在有一个学生类,他的基本功能有study();和sleep();,现在要增加
 smoke();而smoke();就属于拓展功能了,要定义在接口中,因为有的学生不吸烟,如果把smoke();定义在类中,其子类就会强制都吸烟了,这就不合适了.
 */
 
  
  
  
  
  
  
  
  
  
  
  
  
 
   
      
