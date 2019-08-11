四.继承

 4.1 继承的概述
 4.2 继承的特点
 4.3 super关键字
 4.4 函数覆盖
 4.5 子类的实例化过程
 4.6 final关键字
 4.7 抽象类
 4.8 接口
 4.9 多态
 4.10 JDK API使用
 4.11 内部类和匿名内部类
 4.12 异常
 
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
 
4.9 多态
 定义:某一类事物的多种存在形态.
 例子:动物中猫,狗.
  猫这个对象对应的类型是猫类型;
   猫 x=new 猫();
  同时猫也是动物中的一种,也可以把猫称为动物;
   动物 y=new 猫(); //在动物类中,建立猫类型的对象,起名叫y.
  动物是猫和狗具体事物中抽象出来的父类型;
  父类型引用指向了子类对象.
 
 /*
 需求:动物中有猫和狗
 abstract class Animal
 {
     abstract void eat();
 }
 class Cat extends Animal
 {
     public void eat()
     {
         System.out.println("吃鱼");
     }
     public void Catch()
     {
         System.out.println("抓老鼠");
     }
 }
 class Dog extends Animal
 {
     public void eat()
     {
         System.out.println("吃骨头");
     }
     public void kanJia()
     {
         System.out.println("看家");
     }    
 }
 ......
 main()
     Cat c =new Cat();
     c.eat();
     Dog d =new Dog();
     d.eat();
     //开始优化,注意到猫狗对象都调用eat()方法,对eat方法进行封装,即
     public static void function(Cat c) //传猫对象名进来,不就和传普通变量或数组一样?想想是不是?
     {
         c.eat();
     }
     public static void function(Dog d)
     {
         d.eat();
     }
     //再调用,即
     function(new Cat()); //实参新建对象猫传给形参猫类型的变量c
     function(new Dog());
     //问题来了,现在过了一年,又有了Pig类,他也要吃,即
     class Pig extends Animal
     {
         public void eat()
         {
             System.out.println("吃饲料");
         }
     }
     //重点来了,我们知道上面新建对象都是本类类型引用指向本类对象,即Cat c=new Cat();对吧?又注意到,现在猪对象也想要调用eat方法,去打印吃饲料,
     //是不是还要再写一段function函数,传猪类型和变量,函数体再调用吃,这样是不是以后每有不同的动物对象,都要再重复写function,再调用?
     //这显然增加了代码量,不合适了.
     //注意到是不是每个动物的子类都继承了父类Animal,从这里入手,即
     Animal c=new Cat(); //这里子类类型改为父类类型
     //再把function()里形参,改为父类类型和父类变量,即
     public static void function(Animal a)
     {
         a.eat();
     }
     //优化到了这里,不管是哪种动物的子类,想eat(),新建对象作为实参往里丢就行了,少写了很多句function,即
     function(new Cat());   //实参猫对象传给形参动物类型的a变量
     function(new Dog());
     function(new Pig());
 */
  
  总结:
   (i)多态的体现,就是代码提现,即 父类的引用指向了子类对象.
   (ii)多态的前提,即 必须类与类之间有关系,继承或实现,还有就是子类要覆盖父类方法.
   (iii)多态的好处,即 提高了程序的拓展性 eg:是不是现在来个老虎类对象,丢进function函数里就吃了.
   (iv)多态的弊端,即 只能使用父类的引用访问父类的成员 eg:function里加上a.catch();这就不行了,Animal类没有成员catch方法.
 以上就可以归纳为(1)多态的扩展性.
 
  (2)多态的转型
   eg:
   //在main函数中有
   Animal a=new Cat(); //这叫父类的引用指向了子类对象,之前是本类类型,本类对象的,现在猫类型的对象的类型提升了,称为 向上转型
   a.eat();
   //问题来了,现在想要调用猫的特有方法,如何操作?
   有人说好办,即
   Cat c=new Cat();然后 c.catch(); //注意了现在是两只猫了,一只是a猫,一只是c猫,不是实现让a猫抓老鼠了,这不合适.
   当然a.catch();也是不行的.怎么办?见下
   //强制将父类的引用,转变成子类类型,称为 向下转型 即
   Cat c=(Cat)a;//父类的引用a和子类变量c都指向了子类对象,现在都是对同一个猫对象操作了,然后
   c.catch();
   //注:不能出现将父类对象,转变为子类类型,即
   Animal a=new Animal(); //假设可建立父类对象
   Cat c=(Cat)a; //错误
   //多态自始至终都是子类对象在做着变化.
   //在function函数中.可以强制实现向下转型实现catch方法,即
   function(new Cat());
   public static void function(Animal a)
   {
       a.eat();
       Cat c=(Cat)a;
       a.catch();   //到了这里,就实现了猫吃鱼和抓老鼠了
   }
   //问题来了,如果传狗类对象进去,会如何?答案肯定是,不行,怎么能将狗类型转变为猫呢.
   //可以加入判断,如果传进来的是猫类型对象,就吃鱼,否则干些其他的,介绍新的关键字 instanceof 用法:x instanceof y,叫x是y的实例,即
   function(new Cat());
   function(new Dog());
   public static void function(Animal a) //父类引用做形参,只要是其子类对象,都可丢进去操作
   {
      a.eat();
      if(a instanceof Cat)
      {
          Cat c=(Cat)a;
          c.catch();
      }
      else if(a instanceof Dog)
      {
          Dog d=(Dog)a;
          d.kanJia();
      }
   }
   //现在丢猫对象进来,就吃和抓老鼠,丢狗对象进来就吃和看家.
   //假如先判断是否是动物的实例?即if(a instanceof Animal){打印叫};这样一来,不管丢进来哪种对象,都是符合动物的实例,就不能执行else语句了,
   //这是一个细节,不能先判断是否是父类类型.
   
   //好了到了这里,我们基本上就算完成了实现具体子类的操作了,注意了注意了注意了,我们学的是面向对象的思想,那你想一想把function()函数定义在
   //主函数中合适吗?不合适的,我们对其优化,任然向上抽取,就是把function()函数单独封装成一个工具类,然后再在主函数里建立工具类的对象,让该对象
   //调用所属工具类的方法,传子类对象进来是不是就完事了,即
   class AnimalDo
   {
      public static void function(Animal a) //父类引用做形参,只要是其子类对象,都可丢进去操作
      {
      a.eat();
      if(a instanceof Cat)
      {
          Cat c=(Cat)a;
          c.catch();
      }
      else if(a instanceof Dog)
      {
          Dog d=(Dog)a;
          d.kanJia();
      }
      }  
   }
   然后在main函数中:AnimalDo ad=new AnimalDo();ad.function(new Cat());ad.function(new Dog());
   /*
   总结:
   (i)上面这个例子突出强调在分析事物或者建立工具时,一定要从面向对象的思想出发,逐步向上抽取形成类(可以认为有事物类和工具类),在主函数中建立
   类的对象去让对象去完成.强调面向对象.
   (ii)可以利用多态这一特性,使调用对象做事变得简单了;原来只能分批调用每一个对象去做事,现在可以利用父类的引用,去指挥很多不同对象统一做事了,
   这是因为我们找到了这些具体子类所属的统一父类,虽然只能使用父类成员,但是可以向下转型.
   */
   
  (3)多态时的调用成员的特点
   学到这,要知道,提到多态,就是父类的引用指向子类对象,即 Fu f=new Zi();
   (i)多态时调用非静态成员函数的特点,即
   Fu f=new Zi();
   f.study(); //父子类都有study方法
   f.method1();//父类没有,子类有该方法,编译失败
   f.method2();//父类有,子类没有,有继承,没问题
   即多态时 编译看左边,运行看右边.     看左边是如果父引用变量(即f)所属类中没有要调用的方法,就会编译失败;而看右边是当编译通过时,则会运行子类对象
   所属类中的非静态成员函数.
   (ii)调用静态成员函数时,即
   不管编译还是运行,都看左边.  eg:就是父子类中都有同名静态函数,就看左边,就编译和运行父类的静态成员函数.
   (iii)调用成员变量(不管是否静态)时,即 不管编译还是运行,都看左边.
   打印f.num;//这里f是父类型引用变量,num是父子类同名成员变量. 都会打印父类的变量.
   /*
   当然了,不用多态时,就使用本类类型本类对象,即Zi z=new Zi();z.xxx;都会运行子类成员(包括继承来的).
   在开发中,一般不会覆盖静态成员的,这是愚蠢的,因为覆盖没用啊,调用时只会执行父类成员;
   还有也不会出现父子类中出现同名变量,都可以继承来的变量,还声明干啥?
   */
   
   /*
   需求:张三想玩李四的手机
   class ZhangSan
   {
       public void play(LiSi ls)
       {
           ls.play1();
       }
   }
   class LiSi
   {
       public void play1()
       {
           System.out.println("play iPhone")
       }
   }
   main函数中:
   ZhangSan zs=new ZhangSan();
   zs.play(new LiSi()); //运行到这张三就可以玩iPhone了.
   //分析上面,类与类之间,互相调用成员时,声明A类函数的形参,即A类调用B类方法时,即形参就是B类类型,B类类型变量;在主函数中传实参就是B类对象.
   //不要想复杂了.即一个类调用另一个类成员时,在本类声明形参就是另一个类的类型和变量,主函数调用本类方法时,实参就是另一个类的对象.即操作对象
   //操作对象操作对象.就只是在声明函数时形参写为 某类类名+某类类型变量;实参写为 new 某类类名(),即新建要调用某类的对象;或给某类对象起个名字,
   //调用该对象名也可.
   */
   
   /*
   需求:我想要一只猫叫
   interface Jiao
   {
       public abstract void jiao();
   }
   class Person
   {
       public void maoJiao(Jiao j)
       {
           if(j!=null)
               j.jiao();
       }
   }
   class Cat implements Jiao
   {
       public void jiao()
       {
           System.out.println("喵喵");
       }
   }
   class JiaoTest
   {
       public static void main(String[] args)
       {
           Person p=new Person();
           p.maoJiao(null); //不传对象,不想让他叫
           p.maoJiao(new Cat());
       }
   }
   分析本需求
   总结:
   (i)在Person类中,声明函数形参改变了 Jiao j即为Jiao j=new Cat();即为 接口引用指向子类对象 (可以类比父类引用指向子类对象,只是设计时关键字不同);
      这也是多态的应用,以后不管让狗汪汪叫还是其他的,就只是声明狗类,传狗对象即可,即实现指挥多个对象了.
   (ii)设计jiao()方法为接口,是不是拓展了程序的功能,对吧.以后来了一个狗类,让狗类也可以实现jiao方法,对其进行复写,好让我让狗叫,这就完事了.
   
   本需求就是接口和多态的应用了. 接口暴露规则,子类实现复写,多态让我统一指挥.
   接口的好处之一就是降低了类与主类之间的 耦合性(紧密联系程度).
   举个例子来理解耦合性,现在就是仍然拿猫叫来说,不使用接口,就是声明猫类,声明猫叫方法,主函数建立猫对象,对象名调用猫叫方法.这是不是有一个问题,
   该程序毫无拓展性啊,猫类与主函数联系很紧密.现在想要狗叫,利用接口和多态就好办了.
   interface Jiao
   {
       public abstract void jiao();  
   }
   class Cat implements Jiao
   {
       public void jiao()
       {
           System.out.println("喵喵");
       }
   }
   class JiaoTest1
   {
       public static void main(String[] args)
       {
          Jiao j=new Cat(); //接口引用指向子类对象,类比父类的引用指向子类对象就完事了.
          j.jiao();
       }
   }
   本例就强调,以后在设计程序时,要考虑程序的扩展性,现在是不是就可以在子类Cat里的方法想咋改就咋改,哪怕你是改成汪汪,我也是不管,即利用接口.
   */
   /*
   小知识:数据库的连接常见时JDBC,Hibernate(框架,一个类,里面有了数据库连接);对数据库操作即crud,增删改查,create,read,update,delete.
          先连接数据库,再操作数据库,最后关闭数据库连接.
   */
   
  4.10 JDK API使用 
  现在来学习如何使用JDK API 
   先来介绍java中的所有类的上帝类 Object类
   eg: class Demo   //这里就是省略了继承语句,即 class Demo extends Object
       {}
       Object:是所有对象的直接或者间接父类(超类,根类);
       该类中定义了所有对象都具备的方法.
   (1)Object类中的 equals() 相等,返回boolean类型,java认为所有对象都是可以比较的,Object类中已经提供了对对象是否相同的比较方法.
    (i)同类下不同对象的比较,即比较的是内存地址值.
     因为Demo类默认继承了超类Object,方法拿来用就完事了,即
     main函数中: Demo d1=new Demo(); Demo d2=new Demo(); 打印 d1.equals(d2) 输出false,因为不同对象,所占地址不同
    (ii)同类下不同对象的成员比较
     eg: class Demo
         {
             int age;
             Demo(int age)
             {
                 this.age=age;
             }
             public boolean compare(Demo d)
             {
                 return this.age==d.age;
             }
         }
         class EqualsTest
         {
             public static void main(String[] args)
             {
                Demo d1=new Demo(20);
                Demo d2=new Demo(21);
                System.out.println(d1.compare(d2)); //执行到这打印 false
             }
         }
         //分析:傻不傻啊,虽然可以实现比较,但是子类Demo是不是已经继承了超类Object了?已经有了比较方法了,进行复写不就完事了,只有沿袭超类的功能,
         //建立自己的特有比较内容即可.好了,所以不要重新定义compare函数了,对equals方法进行复写
         类Demo中: public boolean equals(Object obj)
                   {
                       if(!(obj instanceof Demo))
                           return false;
                       Demo d=(Demo)obj;
                       return this.age==d.age;
                   }
                   //分析上面代码
                   //(i)形参为什么不是Demo d,因为在API中,equals方法里的形参就是父类类型的引用,这里是不是体现了多态,增加了程序的扩展性,对吧.
                   //Object obj这里就代表了d2.
                   //(ii)为什么加入判断语句,刚好学习使用关键字instanceof,这是因为,是不是如果比较不同类的对象,传进来一个Person类对象p,先判断
                   //是否是Demo类,不是就返回false了,这是不是增加了代码的健壮性啊,对吧.
                   //(iii)为什么返回前要向下转型,因为如果要是返回this.age=obj.age,出现什么问题,请问,超类有变量age这一成员吗?肯定没有,
                   //所以要先向下转型.
                   //总结,使用equals方法,如果使用了特有数据(这里就是age),就先进行判断动作,防止把Person类转变为Demo类,再进行转型动作.
    (2)toString() 返回任一对象的字符串形式,即
     对象名.toString()
     好了,学习了这两种方法就可以得出(i)我想直接使用超类方法,直接对象名.超类方法(形参)就完事了;(ii)我想使用超类方法,但是想定义特有内容直接覆盖就完事      了.
  
  4.11 内部类和匿名内部类
  /*
  内部类
   之前如果两个类要想互相访问是不是都要建立对象,通过对象去访问别人.
   而内部类就是将一个类定义在另一个类的里面,里面的类就叫内部类(内置类,嵌套类).
   访问特点:
   (i)内部类可以直接访问外部类的成员,包括私有.(私有只在本类有效,本类可用,其他类不可访问);
   (ii)外部类要访问内部类,必须建立内部类对象.
   class Outer //外部类
   {
       private int x=3; //外部类成员变量
       class Inner //内部类作为外部类成员
       {
           int x=4; //内部类成员变量
           void method()
           {
               int x=5; //方法中的局部变量
               System.out.println(x);  
           }
       }
       public void function()
       {
           Inner i=new Inner();  //符合访问特点(ii)
           i.method();
       }
   }
   class InnerTest
   {
             public static void main(String[] args)
             {
                 Outer o=new Outer();
                 o.function();
             }
   }
   分析: o.function()执行完打印的是3还是4,还是5?答案是5.
   这是因为function有变量x了,就访问局部变量了;如果打印 this.x,输出4,因为this代表的是内部类的对象;如果想打印3,就指定,即Outer.this.x,即
   外部类对象的成员x;如果没有int x=5,打印x,要知道前面都默认省略了this或Outer.this;如果想在主函数中直接访问内部类,就是不需要
   在function中建立Inner对象,格式如下:
   Outer.Inner i=new Outer().new Inner();
   i.method();
   
   访问格式:
   (1)当内部类定义在外部类的成员位置时,而且非私有,可以在外部其他类中,可以直接建立内部类对象.外部其他类举个例子如InnerTest类.
      格式: 外部类名.内部类名 变量名 = new 外部类名().new 内部类名(); 如:main中的Outer.Inner i=new Outer().new Inner();
   (2)当内部类被修饰符修饰时:
      private,将内部类在外部类中进行了封装;
      static,内部类就具备了static的特性:
      (i)此时,内部类只能访问外部类的静态成员了,访问出现局限;
      (ii)在外部其他类中,如何直接访问静态内部类中的非静态成员,思考,不是静态,就必须要对象,所以格式为 new Outer.Inner().xxx,xxx为变量或方法;
      (iii)在外部其他类中,如何直接访问静态内部类中的静态成员,更简单,静态的,来类名就完事了,格式为 Outer.Inner.xxx;
      注意:当内部类中定义了静态成员,那么内部类必须也是静态的.跟抽象方法一样;
           当外部类中的静态方法想要访问内部类时,内部类必须是静态的.格式有:Inner.xxx或new Inner().xxx;
     上面规则很好记,静态的直接拿类名用就完事了,非静态的就搞对象啊,静态的+非静态的,就类名加搞对象一起啊.
     
  内部类定义原则,即啥时定义内部类:
  class是干嘛的?描述事物的,在描述时,是不是要让类与类之间有更好的联系啊,对吧,比如继承,实现.现在当描述某一类事物时,事物内部又有许多类事物,就把他们
  定义为内部类.举个例子,拿人体(body)这类事物来说,描述body类时,现在又想要描述人体的各个器官,比如说心脏(xinzang)类,是不是把xinzang类定义为body类
  的内部类更好,因为xinzang类还要访问body类里的其他类,如胃部,对吧.更好的显示了类与类的联系.定义在外部类中,可以对其进行封装(即可以使用private)
  不让外部其他类随便访问了,想访问就提供公共的访问方法,还要进行判断,不是谁都可以访问本私有内部类的.想想是不是?板砖的想访问xinzang,疯了哦.
  
  注意了注意了注意了,上面说内部类定义在成员位置时,可以被static修饰,现在在上面的method方法中定义一个内部类,此时该内部类也是内部类,但是叫他
  局部内部类,局部内部类不能被static修饰了只有成员才行.该内部类也不能有静态成员了,想想就对的,但是,访问方式是不变的.
  总结:当内部类定义在局部时 (i)不可以被成员修饰符修饰了;(ii)该内部类只能访问外部成员和被final修饰的局部变量了;eg:在method方法中,定义int x=4;
  同在该method方法里的局部内部类不能访问x,想要访问,必须是final int x=4;
  小知识:现在往method方法里搞个形参,有method(int a),局部内部类也不能访问,必须是形参final int a;我们知道被final修饰的变量为常量,那么在main
  函数中,新建一个对象调用method方法,传o.method(7)和o.method(8),可以吗,答案是可以的,因为a不是成员变量被final修饰了,当运行新建对象o了,传7进去,
  开始进栈,执行结束就出栈了;同样传8进去,a被锁住了,值为8了,执行完就出栈了,a就释放了.如果传a进去,a被锁住了,为7,实现a++,就出现问题了.当然了,新建
  两个对象,即o1.method(7);和o2.method(8);也可以.
  */
  
  /*
  匿名内部类:
   我们知道如果想要使用对象一次,那就是 new 类名();即可,想要使用对象多次就给他起个名即可.
   仍然拿body和心脏来理解匿名内部类,人体这类事物里有心脏这类事物,同样的猫体内也有心脏,好了,就提取心脏这类事物,形成父类(接口),本例只定义人体和
   人体心脏,不定义猫了.即
   abstract class XinZang
   {
       abstract void tiao();
   }
   class PersonBody
   {
       //代码段a
       class PersonXinZang extends XinZang  //内部类可以直接继承外部其他类      
       {
           void tiao()
           {
               System.out.println("跳动");
           }
       }
       public void function()
       {
           //代码段b
           new PersonXinZang().tiao();
       }
   }
   main中: new PersonBody().function();  //到这就完事了
   //开始介绍匿名内部类了:
   //(i)匿名内部类就是内部类的简写格式;
   //(ii)写匿名内部类的前提是必须要继承一个类(有父类)或者实现接口;
   //(iii)格式: new 父类(或接口)名(){子类要对父类(或接口)复写的内容}.要调用的方法()
          eg:现在开始简写了,不要代码段a和b了,直接在function里实现复写和调用,即
          匿名内部类即只有class了,没有匿名内部类名了,当然就不能建立对象了,所以考虑建立父类对象,又因为父类里有抽象方法,建立没意义,所以在建立父类对
          象的同时,声明子类对父类要复写的内容,即
          public void function()
          {
              new XinZang()
              {
                   void tiao()
                   {
                       System.out.println("跳动");
                   }
                   void show() //声明show方法,匿名子类对象中的一个特有功能
                   {}
              }.tiao();
          }
          注意:也可以建立父类对象时,起个名,即 XinZang xz=new XinZang(){......},记住起名后,大括号后要加符号 ; 然后xz.tiao();也行,但是xz.show()           就不行,因为父类引用只能使用父类成员.
    //(iv)其实匿名内部类就是一个匿名子类对象,而且这个对象有点胖,胖是因为带对象内容.
          即匿名内部类就是先建立父类对象,再实现子类对象对父类(多个)方法的复写,最后在调用子类对象所需的方法,简写就是  一步到位.
    //(v)匿名内部类中定义的方法最好不要超过三个.因为复写时会导致代码长,阅读性差,如果不给父类对象起名,会出现多个相同的代码段,只是调用时 .xxx不同,
         阅读性就差了,代码谁写的,太烂了. 
    练习1:通过匿名内部类补足在主函数中的语句 Outer.function().method();这里method()定义在接口A中;
          分析:Outer.function()到这可以发现什么,是不是Outer类有一个成员function(),并且是静态的,没有形参,对吧,但是不知道返回值类型;
               .method()就是返回值.method(),好了,返回值要么是类名,要么是对象.
               又因为接口为:
               interface A
               {
                   void method(); //系统默认加上public abstract
               }
               所以不是静态的,类名排除,确定了function返回值类型为A,因为要用匿名内部类,不能有别的类,返回对象只能是接口类型,综合得出即
               class Outer
               {
                   public static A function()
                   {
                       return new A()
                       {
                           public void method()
                           {}
                       };  //注意这里为什么不加.method,因为要求返回的只是一个对象,又要求用匿名内部类,所以返回一个胖对象,不需要调用匿名子类对象的                            //method方法,主函数里返回值.method()已经实现调用了好吧.
                   }
               }
     练习2:没有父类也没有接口,要求使用匿名内部类.
      想到了超类Object,即
      main中 new Object()
             {
                 void function()
                 {}
             }.function();
      所以讲到这,只要父类成员少,使用匿名内部类,一步到位即可;注意一下,结束要么是大括号要么是";",而使用匿名内部类都要加符号";".
  */
  
  4.12 异常
   异常:就是程序在运行时(编译通过)出现的不正常情况.
   异常的由来:现实生活中,出现的许多问题也是一个具体的事物,也可以通过java中的类进行描述,并封装成对象.
   异常分为严重情况和非严重情况,严重的问题为Error类,非严重的问题为Exception类,对着两个类向上抽取,形成了一个异常体系,即
   异常体系
    Throwable类 (所有问题的超类)
     Error类
      通常出现重大问题,如运行的类不存在(java haha,无haha类)或者内存溢出等;
      不编写针对代码对其处理
     Exception类
      在运行时出现的一些情况,如角标越界或类转变异常等,可以通过try catch finally
   Error和Exception的子类名都是以父类名作为后缀的
   java中对于这些抛出的异常情况都可以在JDK API 中的lang Throwable类中查看.
  
  
  
  
  
  
                   
  
   
                 
     
   
       
   
