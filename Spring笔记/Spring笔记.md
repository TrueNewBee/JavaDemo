### Spring笔记

ps:

2021-02-26 10:02:45

好紧脏 

2021-02-25 11:50:50

因为有课程笔记,故把主要东西截图

2021-02-24 21:37:10

头昏脑子,明天继续,,,md javaspring的配置好jb麻烦 怪不得有了spring boot



## Spring的介绍

![image-20210224175253536](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210224175253536.png)

![image-20210224190928025](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210224190928025.png)

![](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210224191007498.png)

![image-20210224194747050](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210224194747050.png)

```java
ps:  在导入坐标时候,刷新项目或者重启,这样右键才可以新建xml文件种有 spring的conf文件
    
```

Demo目录图:

![image-20210224195354834](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210224195354834.png)

1. 导入坐标 (pom.xml):

   ```java
       <dependencies>
           <dependency>
               <groupId>org.springframework</groupId>
               <artifactId>spring-context</artifactId>
               <version>4.2.8.RELEASE</version>
           </dependency>
       </dependencies>
   ```

2. 创建Bean(applicationContext.xml)

   ```java
   <bean id="userDao" class="com.itheima.dao.impl.UserDaoImpl"></bean>
   ```

3. 创建实体类

   接口:

   ```java
   public interface UserDao {
       public void save();
   }
   ```

   实现类:

   ```java
   public class UserDaoImpl implements UserDao {
       public void save() {
           System.out.println("save running..");
       }
   }
   
   ```

   Demo类:

   ```java
   public class UserDaoDemo {
       public static void main(String[] args) {
          ApplicationContext app= new ClassPathXmlApplicationContext("applicationContext.xml");
           UserDao userDao = (UserDao)app.getBean("userDao");
           userDao.save();
       }
   }
   ```

4. 运行结果

   ![image-20210224195526863](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210224195526863.png)

![image-20210224200402883](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210224200402883.png)

### 测试类

导入这个junit包:

```java
		<dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.11</version>
        </dependency>
```

在test/java下创建测试类(刷新下maven)

![image-20210224202831662](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210224202831662.png)

然后写测试类,右键运行即可

```java
public class SpringTest {

    @Test
    public void test1(){
        ApplicationContext app= new ClassPathXmlApplicationContext("applicationContext.xml");
        UserDao userDao = (UserDao)app.getBean("userDao");
        UserDao userDao2 = (UserDao)app.getBean("userDao");
        System.out.println(userDao);
        System.out.println(userDao2);
    }
}

```

![image-20210224203353430](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210224203353430.png)

![image-20210224204019914](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210224204019914.png)

![image-20210224211805660](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210224211805660.png)

![image-20210224211842385](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210224211842385.png)

![image-20210224213542433](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210224213542433.png)

这个需要与 set方法名字对应,直接在spring内部有对象传递,直接接收后用了

![image-20210224213601028](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210224213601028.png)

![image-20210224213442825](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210224213442825.png)

![image-20210225113941735](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210225113941735.png)

![image-20210225115039167](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210225115039167.png)

![image-20210225115313976](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210225115313976.png)

![image-20210225120041026](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210225120041026.png)



![image-20210225120305973](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210225120305973.png)



第一种是通过 ID获取,需要用类型强转,,, 第二种直接指明哪个类,适用于不同ID但有同种类的情形

![image-20210225120252509](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210225120252509.png)

![image-20210225120520614](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210225120520614.png)



 ![image-20210225120956995](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210225120956995.png)

![image-20210226110305091](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210226110305091.png)

![image-20210226110329061](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210226110329061.png)

![image-20210226115309347](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210226115309347.png)

![image-20210226112637915](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210226112637915.png)

![image-20210226115935790](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210226115935790.png)

![image-20210226141301539](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210226141301539.png)

![image-20210226141603905](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210226141603905.png)

![image-20210226143243699](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210226143243699.png)

```java
/**
 * 用于注解测试
 */
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("classpath:applicationContext.xml")
public class SpringJunitTest {

    @Autowired
    private UserService userService;

    @Test
    public void test1(){
        userService.save();
    }
}
```

![image-20210227132259228](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210227132259228.png)

![image-20210227133042150](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210227133042150.png)



cglib (了解AOP底层知识)

![image-20210227140558305](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210227140558305.png)

![image-20210227141021292](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210227141021292.png)

![image-20210227141529495](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210227141529495.png)

![image-20210227141646549](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210227141646549.png)

![image-20210227152918593](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210227152918593.png)

![image-20210227154022432](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210227154022432.png)

![image-20210227155316352](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210227155316352.png)

![image-20210227161508406](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210227161508406.png)

![image-20210227161844275](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210227161844275.png)

![image-20210227162024905](C:\Users\Administrator\Desktop\Spring笔记\README.assets\image-20210227162024905.png)

## 重点是 先弄懂xml再看注解

