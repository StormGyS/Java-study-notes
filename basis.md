一:人机交互
1.图形化界面
2.命令行方式
(1)Dos命令 
   dir(目录):列出当前目录下的文件与文件夹
   md:创建目录
   rd:删除目录
   cd :进入指定目录
   cd..:退到上一级目录
   cd/:返回到根目录
   del:删除文件
   exit:退出Dos窗口
   切换盘符直接就是D:即可.
二:java语言概述
  1.java语言的特点:跨平台性(java程序可在不同的操作系统下运行,即可移植性好.得益于有Windows的jvm和Linux的jvm)
  2.jre:java运行环境 =jvm+核心类库等
  3.jdk:java开发工具包 =java的一些开发工具+jre; 常见的开发工具有编译工具(javac.exe)和打包工具(jar.exe)等.
       总之就是用jdk开发java程序,交给jre运行.
  4.配置环境变量就是让开发工具在任一目录下运行,也可以连带bin文件夹一起复制放到Path变量里,放在最前面用;隔开即可.
  5.不用public那么文y件名.java就不用与类名一致.
  6.空格按多了是不是就废了,按Tab键(制表符).
  7.在一个java文件中,写两个不同的class,用javac编译后会生成两个.class字节码文件,用java分别运行这两个字节码文件.
  8.写类之前先写一个多行注释,有需求:  思路:1. 2.  步骤:1. 2. ...,再写类,关键代码要加注释(一是解释说明,二是调试用的).
三:java语言基础组成
  1.关键字:被java语言赋予了特殊含义的单词,都小写.
  (1)用来定义数据类型:class,interface,byte,short,int,long,float,double,char,boolean,void.
  (2)用来定义数据类型的值:true,false,null.
  (3)用来定义流程控制:if,else,switch,case,default,while,do,for,break,continue,return.
  (4)用来定义访问权限的修饰符:public,private,protected.
  (5)用来定义类,函数,变量的修饰符:abstract,final,static,synchronized.
  (6)用来定义类与类之间的关系:extends,implements.
  (7)用来定义建立实例及引用实例和判断实例:new,this,super,instanced.
  (8)用来异常处理:try,catch,finally,throw,throws.
  (9)用来包:package,import.
  (10)其他修饰符:native,strictfp,transient,volatile,assert.
  2.标识符:程序中自定义的一些名称,由字母,数字0~9和_与$组成,数字不可以开头,不能使用关键字,严格区分大小写,要有意义.
  (1)包名:多单词组成时都小写,xxxyyyzzz.
  (2)类名接口名:多单词组成时,所有单词首字母大写,XxxYyyZzz.
  (3)变量名和函数名:多单词组成时,第一个单词首字母小写,其他大写,xxxYyyZzz.
  (4)常量名:所有字母都大写,多单词时用下划线连接,XXX_YYY_ZZZ.
  3.注释://  /**/  /***/(文档注释):注释内容可以被jdk提供的工具javadoc所解析,生成一套以网页文件形式体现的该程序的说明文档.
  /**
  这是我的Hello World程序.
  @author GyS
  */
  public class Demo
  {
     /*
     这是主函数,程序的入口.
     它可以保证程序的独立运行.
     */
     public static void main(String[] args)
     {
           //输出Hello World!
           System.out.println("Hello World");
     }
  }
  4.常量与变量
  (1)常量:不能改变的数值.分类有整数常量;小数常量;布尔型常量,数值有true和false;字符常量将一个数字字母符号用单引号''标识;字符串常量将一个或者多个字符
  用双引号""标识;null常量只有一个数值就是null.
     对于整数,有三种表现形式:十进制,0~9,满10进1;八进制,0~7,满8进1,用0开头表示;十六进制,0~9,A~F,满16进1,用0x开头表示.还有二进制,计算机中表示数据就用二进制,为什么用十,八,十六进制,就是为了更方便的表示一个整数,十进制60,和十六进制0x3c输出都是整数60.
  (i)整数6用int定义,32bit,4个byte,前面都补0,那么负整数-6就是正整数6的取反加1.
  (2)变量:数值可变,内存中开辟多少位的二进制来存变量的数值由数据类型决定.
  (i)基本数据类型:数值型(又分整数类型[byte,short,int,long]和浮点类型[float,double])与字符型(char)及布尔型(boolean).
  (ii)引用数据类型:类(class),接口(interface)及数组([]).
  整数默认int,小数默认double.所以要加L与f.
  (iii)强制类型转换,byte b=3,b=b+2,打印b,会报错,为什么?因为b是byte,而2是int,计算b+2,会将b提升为int型再与2计算,为int(32bit),赋给b(8bit),导致丢失精度,故报错.而(byte)(b+2),则将b+2的值(int)强制转换为byte,即干掉前三个格子,留最后一个格子.应用就是可以把小数保留整数部分吧;打印字符a:System.out.println('a'),输出a;那么System.out.println('a'+1),因为字符a在ASCii编码表对应数值97,所以输出数值98.则打印c,用强制类型转换有System.out.println((char)('a'+2)),输出字符c.
  5.运算符
  (1)算数运算符: 正号(+)  负号(-)  加减乘除(+-*/)  取模(取余数%)  自增(++)  自减(--)  字符串相加(+)
  eg:(i)5%5为0,1%5为1,5%1为0;-1%5为-1,1%(-5)为1,符号取决于被模数. (ii)a=2,b=++a,则b=3,a=2; a=2,b=a++,则b=2,a=3; a=2,b=--a,则a=1,b=1; a=2,b=a--,则a=1,b=2. (iii)"he"+"llo"为hello. (iv)int i=4567,i=i/1000*1000,为4000吧,不为4567了,因为4567/1000为4.567,而为int,结果为4,而4*1000即为4000,要注意.
     字符串数据与所有数据使用+号相连接,结果为字符串.eg:System.out.println("a="+a+",b="+b);输出a=4,b=4.
     转义字符:通过\转变后面字符的含义. \n:换行 \b:退格,相当于backspace \r:按下回车键(注意Windows系统下回车符用两个表示\r\n) \t:制表符,相当于Tab键 \":打印" \':打印' char ch ='你';//可以,因为char类型为2byte,而一个汉字也为2byte. println中的ln就是换行,直接为print则不换行.
     
     

  
  
  
  
  
 
