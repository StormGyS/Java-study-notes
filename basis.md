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
     对于整数,有三种表现形式:十进制,0~9,满10进1;八进制,0~7,满8进1,用0开头表示;十六进制,0~9,A~F,满16进1,用0x开头表示.
   
  
  
  
  
 
