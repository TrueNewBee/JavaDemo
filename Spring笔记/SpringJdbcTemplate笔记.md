### 2021-02-27 23:17:50

已经把spring配置方面弄完了

发现,,,配置好麻烦,啥都交给了 spring  

java程序员好懒,,,仿佛就只剩spring了  

明天mvc结束,,然后 项目 然后boot 可以整理java简历了!

越努力,越幸运!!!!! 三技之长!!!!加油!!

![image-20210227162742226](C:\Users\Administrator\Desktop\Spring笔记\SpringJdbcTemplate笔记.assets\image-20210227162742226.png)

![image-20210227174347939](C:\Users\Administrator\Desktop\Spring笔记\SpringJdbcTemplate笔记.assets\image-20210227174347939.png)



![image-20210227174308806](C:\Users\Administrator\Desktop\Spring笔记\SpringJdbcTemplate笔记.assets\image-20210227174308806.png)



用配置文件的模板

![image-20210227175223066](C:\Users\Administrator\Desktop\Spring笔记\SpringJdbcTemplate笔记.assets\image-20210227175223066.png)

![image-20210227175242332](C:\Users\Administrator\Desktop\Spring笔记\SpringJdbcTemplate笔记.assets\image-20210227175242332.png)

![image-20210227175255014](C:\Users\Administrator\Desktop\Spring笔记\SpringJdbcTemplate笔记.assets\image-20210227175255014.png)

![image-20210227203043619](C:\Users\Administrator\Desktop\Spring笔记\SpringJdbcTemplate笔记.assets\image-20210227203043619.png)

![image-20210227203124911](C:\Users\Administrator\Desktop\Spring笔记\SpringJdbcTemplate笔记.assets\image-20210227203124911.png)

Account类:

```java
public class JdbcTemplateTest {
    // 飘红是因为 这个pox文件有点错,,逻辑代码对
    @Test
    // 测试jdbcTemplate开发步骤
    public void test1(){
        // 创建数据源对象
        ComboPooledDatasource datasource = new ComboPoolDataSource();
        datasource.setDriverClass("com.mysql.jdbc.Driver");
        datasource.setJdbcUrl("jdbc:mysql://localhost:3306/test");
        datasource.setUser("root");
        datasource.setPassword("123456");

        JdbcTemplate jdbcTemplate = new JdbcTemplate();
        // 设置数据源对象 知道数据库在哪
        jdbcTemplate.setDataSource(dataSource);
        // 执行操作
        int row = jdbcTemplate.update("insert into account values(?.?)", "tom", 5990);
        System.out.println(row);
    }
}
```

```java

public class JdbcTemplateTestCRUD {

    /**
     * 通过jdbcTemplate配置的对象事项增删改查
     */
    @Autowired
    private JdbcTemplate jdbcTemplate;

    @Test
    public void testQueryAll(){
       // 查询所有数据
        List<Account> account = jdbcTemplate.query("select *from account", new BeanPropertRowMapper<Account .class>);

    }

    @Test
    public void testUpdate(){
        jdbcTemplate.update("update account set money=? where name="?", 10000, "tom"");

    }

}

```



# 事务

![image-20210227211509429](C:\Users\Administrator\Desktop\Spring笔记\SpringJdbcTemplate笔记.assets\image-20210227211509429.png)

![image-20210227212148863](C:\Users\Administrator\Desktop\Spring笔记\SpringJdbcTemplate笔记.assets\image-20210227212148863.png)

![image-20210227223001038](C:\Users\Administrator\Desktop\Spring笔记\SpringJdbcTemplate笔记.assets\image-20210227223001038.png)

## 事务常用于 转账业务

用AOP实现:

比如转账前先事务控制,,转账后事务控制,如有异常直接回滚了

**配置**

![image-20210227225357679](C:\Users\Administrator\Desktop\Spring笔记\SpringJdbcTemplate笔记.assets\image-20210227225357679.png)

###  上述三部分基本是配死的

![image-20210227230007182](C:\Users\Administrator\Desktop\Spring笔记\SpringJdbcTemplate笔记.assets\image-20210227230007182.png)

![image-20210227230608724](C:\Users\Administrator\Desktop\Spring笔记\SpringJdbcTemplate笔记.assets\image-20210227230608724.png)



### 其实注解就是@加xml中的名字,,  替代了xml的配置而已 更省事了

### 不过需要组件,给spring说是哪个包

![image-20210227231230939](C:\Users\Administrator\Desktop\Spring笔记\SpringJdbcTemplate笔记.assets\image-20210227231230939.png)

![image-20210227231049363](C:\Users\Administrator\Desktop\Spring笔记\SpringJdbcTemplate笔记.assets\image-20210227231049363.png)

### 需要给注解加上驱动

![image-20210227231131729](C:\Users\Administrator\Desktop\Spring笔记\SpringJdbcTemplate笔记.assets\image-20210227231131729.png)

1,先该上面的文件

 ![image-20210227231347721](C:\Users\Administrator\Desktop\Spring笔记\SpringJdbcTemplate笔记.assets\image-20210227231347721.png)

2. 扫描文件

   ![image-20210227231230939](C:\Users\Administrator\Desktop\Spring笔记\SpringJdbcTemplate笔记.assets\image-20210227231230939.png)

3. 在相应方法上添加注解就好了 

4. 就替代了xml

5. ![image-20210227231704222](C:\Users\Administrator\Desktop\Spring笔记\SpringJdbcTemplate笔记.assets\image-20210227231704222.png)

6. 先把XMl配置弄懂,,,,注解小kiss



*******

