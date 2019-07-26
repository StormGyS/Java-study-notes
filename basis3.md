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
    getxxx就肯定有一个私有属性.
    */
    
 
    
    
    
    
    
 
    
    
    
  
    
    
         
  
   
   
   
   
   
   
   
   
   
   
  
  
   
  
  
  
  
  
  
  
  



