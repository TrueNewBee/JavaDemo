# java基础笔记

2021-02-23 22:49:05

明天吧java的集合和Tomcat看了 其他的继续,明天差不多java进阶完了

继续后面spring和spring boot

2021-02-23 21:02:56

集合先放那,我想先看maven

2021-02-23 20:09:46

继续,晚上和小翔一块吃了饭

2021-02-22 18:51:54

看到了  集合 剩下还有 集合 反射 泛型 IO 注解 基础语法就完了

剩下就是进阶东西了  然后是Spring框架!

## 6. java的高级特性

### 6.1 泛型

### 6.2 反射

###  6.3 注解

### 6.4 IO操作



## 5.网络编程部分

### 5.1 Tomcat

这就是个web服务器而已,只是其他框架直接在内部封装了

### 5.2 server ,request,reponese HTTP

这都是框架底层东西,都类型,也都是用socket连接的

了解,知道是啥,然后主要还是框架

## 4. maven

### 4.1 下载maven 

1. 下载maven 
2. 新建MAVEN_HOME到环境变量(系统变量) maven所在目录
3. Path中增加%MAVEN_HOME%\bin变量  (系统变量)
4. 成功后:
   1. ![image-20210223211857953](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210223211857953.png)



### 4.2 配置maven的本地仓库

![image-20210223214914321](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210223214914321.png)

### 4.3 Maven的工作目录

![image-20210223214853289](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210223214853289.png)

### 4.4 maven命令

1. mvn  compile    

   ```java
    compile 是 maven 工程的编译命令，作用是将 src/main/java 下的文件编译为 class 文件输出到 target 目录下。
   ```

2. mvn test

   ```java
   test 是 maven 工程的测试命令 mvn test，会执行 src/test/java 下的单元测试类
   ```

3. mvn  clean : **clean 是 maven 工程的清理命令，执行 clean 会删除 target 目录及内容。**

4. mvn  package: **package 是 maven 工程的打包命令，对于 java 工程执行 package 打成 jar 包，对于 web 工程打成 war 包。**

5. mvn install 

   ```java
   install 是 maven 工程的安装命令，执行 install 将 maven 打成 jar 包或 war 包发布到本地仓库。
   从运行结果中，可以看出：
   当后面的命令执行时，前面的操作过程也都会自动执行
   ```

### 4.5 配置maven仓库

![image-20210223223253785](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210223223253785.png)

#### 配置远程地址

![image-20210223223319580](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210223223319580.png)

### 4.6 maven总结

#### 添加东西好麻烦,,还没有go mod 省事

![image-20210223224812162](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210223224812162.png)

![image-20210223224822902](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210223224822902.png)

![image-20210223224829837](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210223224829837.png)

需要啥添加啥!! 反正有本地和远程仓库

```java
如果 报错java版本错误5  ,就在 maven的settings中加入
        <profile>
      <id>development</id>
      <activation>
        <jdk>11</jdk>
        <activeByDefault>true</activeByDefault>
      </activation>
      <properties>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
        <maven.compiler.compilerVersion>11</maven.compiler.compilerVersion>
      </properties>
    </profile>
    
    并且把该文件复制一份到 c:user\当前用户\.m2中 重启项目即可解决
```



## 3. 进阶部分

### 3.1 集合

 Collection

![image-20210223201602510](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210223201602510.png)



#### lterator 接口 

![image-20210223201631035](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210223201631035.png)

### ArrayList:

ArrayList是实现了List接口的  可扩容数组(动态数组), 它的内部是基于数组实现的

### Vector :

和ArrayList一样,都是基于数组实现的,只是Vector是一个线程安全的容器,它的内部的每个方法都简单粗暴地上锁,避免多线程引起的安全问题   开销大,效率低

### LinkedList:

双向链表

### Stack:

栈

### HashMap:

是一个利用哈希表原理存储的集合,并且允许空的key-value键值对,但是非线程安全的,多线程环境下会存在问题,而Hashtable是线程安全的容器. HashMap也支持fail-fast机制.

![image-20210224153058102](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210224153058102.png)





### 2.1 构造方法

![image-20210222145406223](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210222145406223.png)

其实就是在初始化 这个类,在new的时候,自动调用了构造方法,如果在类里面没有重写构造方法,就直接调用默认的构造方法.

### 2.2 作用域

![image-20210222151958902](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210222151958902.png)

### 2.3封装

![image-20210222153202592](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210222153202592.png)

### 2.4 继承

![image-20210222153223873](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210222153223873.png)

### 2.5多态

![image-20210222154921071](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210222154921071.png)

其实java类 就是go中的类型  无非是go中分开了把方法和类和对象分开了,java中整合了

### 2.6 组合

这个就像go中的结构体可以组合在一块

![image-20210222155723073](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210222155723073.png)

![image-20210222155740992](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210222155740992.png)

### 2.7代理

![image-20210222162547903](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210222162547903.png) 

调用时候, 传进去Destination对象就好

``` java
// 代理

class  A {
    public void todo(){
        System.out.println("这是A类");
    }
}

class Device{
    private String name;
    private A a;
    public void control(A a){
        a.todo();
    }
}

main {
     Device device = new Device();
	 A a = new A();
 	device.control(a);
}

```

### 2.8 初始化顺序

![image-20210222164327168](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210222164327168.png)

### 2.9 static 静态的 

类似于go中的常量

### 2.10 接口 interface

就是提供了一些规范

![image-20210222165657119](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210222165657119.png)

### 2.11 抽象类

![image-20210222171615865](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210222171615865.png)

### 2.12 内部类

![image-20210222184402521](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210222184402521.png)

### 2.13 集合

![image-20210222184624282](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210222184624282.png)

#### 2021-02-22 18:51:34

****

## 1.  java语法

### 1.1 bug

1. 具备识别BUG的能力：多看
2. 具备分析BUG的能力：多思考，多查资料
3. 具备解决BUG的能力：多尝试，多总结

### 1.2 数据类型

![image-20210218223711386](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210218223711386.png)

### 1.3 变量的使用注意事项

1. 在同一对花括号中，变量名不能重复。  
2. 变量在使用之前，必须初始化（赋值）。 
3. 定义long类型的变量时，需要在整数的后面加L（大小写均可，建议大写）。因为整数默认是int类型，整数太 大可能超出int范围。 
4. 定义float类型的变量时，需要在小数的后面加F（大小写均可，建议大写）。因为浮点数的默认类型是 double， double的取值范围是大于float的，类型不兼容。

### 1.4 常量的使用

常量：在程序运行过程中，其值不可以发生改变的量。 类似于go中的`const `

**Java中的常量分类：**

1. 字符串常量 用双引号括起来的多个字符（可以包含0个、一个或多个），例如"a"、"abc"、"中国"等
2. 整数常量 整数，例如：-10、0、88等
3. 小数常量 小数，例如：-5.5、1.0、88.88等
4. 字符常量 用单引号括起来的一个字符，例如：'a'、'5'、'B'、'中'等
5. 布尔常量 布尔值，表示真假，只有两个值true和false
6. 空常量 一个特殊的值，空值，值为null
7. 除空常量外，其他常量均可使用输出语句直接输出。

```java
public class Demo {
    public static void main(String[] args) {
        System.out.println(10); // 输出一个整数
        System.out.println(5.5); // 输出一个小数
        System.out.println('a'); // 输出一个字符
        System.out.println(true); // 输出boolean值true
        System.out.println("欢迎来到黑马程序员"); // 输出字符串
    }
}
```

看到了标识符 发现有java基础看java好轻松

2021-02-18 22:54:46

2021-02-19 22:46:39继续

### 1.5 标识符

- 第一个字符不能是数字
- 区分大小写
- 小驼峰式(变量,方法)
- 大驼峰(类名)

### 1.6 类型转换

##### 自动转换和强制转换

1. 自动转换

   ![image-20210219224911942](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210219224911942.png)

2.强转

​	![image-20210219224949060](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210219224949060.png)

3. ```java
   // boolean类型不能与其他基本数据类型相互转换。
   boolean s = true;
   ```

### 1.7 三元运算

![image-20210219230155819](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210219230155819.png)

### 1.8 数据输入

```java
        // 数据输入
        Scanner sc = new Scanner(System.in);
        int i = sc.nextInt(); // 表示键盘输入
```

### 1.9 if流程

```java
// if流程
        if (条件) {
           执行语句
        }else{
           执行语句
        }
```

2021-02-19 23:09:04 明天继续 发现看文档技术比看视频快!!!!!



### 1.20 java的内存分配

![image-20210221121813878](C:\Users\Administrator\Desktop\java笔记\README.assets\image-20210221121813878.png)









