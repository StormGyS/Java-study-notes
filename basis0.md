0.下载JDK
1.配置环境变量
  JAVA_HOME
  Path
2.用记事本写第一个java程序
  Demo0:0.HelloWorld  javac Hello.java  java hello
3.eclipse的下载与使用
4.java基础 
  (1)用户输入:创建一个扫描器 Scanner sc = new Scanner(System.in);
     使用扫描器来获取用户输入的数据 int a = sc.nextInt();   Double b = sc.nextDouble();   String s = sc.nextLine();
     Demo0:1.计算a+b的值.
  (2)if语句用做条件判断
  (i)
     if(条件)
     {***}
  (ii)
     if(条件)
     {***}
     else{***}
   (iii)
     if(条件1)
     {***}
     else if(条件2)
     {***}
     else if(条件3)
     {***}
     ...
     else{***}
   (3)java中的循环语句  (i)while循环 (ii)for循环 (iii)do...while循环
      (i)while循环   while(条件) {***} //判断条件为真,执行语句.再判断,直到条件不成立为止.  Demo0:2.还我钱!
   (4)产生随机数  Random rd=new Random();  int n =rd.nextInt(100);//n是一个随机数,范围0~99.
   (5)Demo0:3.应用猜数
 5.基本数据类型
   (1)整数:  int 整数 32bit 4byte -21亿~21亿之间;  byte java中最小的数据单元 8bit -128~127;  short 短整数 16bit 2byte -32768~32767;  long 长整数 64bit 8byte; eg:1300000000用int,而6000000000用long表示,报错就要在末尾加上L.
   (2)小数:  double 64bit 8byte 双精度小数,精度高,准确性高;  float 32bit 4byte 单精度小数,同样末尾要加f,不然报错.
