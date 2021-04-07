## Mybatis-Plus的使用

1. 在SpringBoot中导依赖(只需要导入Mybatis-plus就好,不需要再额外导入Mybatis)

   ```xml
   <dependency>
       <groupId>com.baomidou</groupId>
       <artifactId>mybatis-plus-boot-starter</artifactId>
       <version>3.4.2</version>
   </dependency>
   ```

2. 代码生成器依赖

   ```xml
   <!--导入代码生成器-->
   <dependency>
       <groupId>com.baomidou</groupId>
       <artifactId>mybatis-plus-generator</artifactId>
       <version>3.4.2</version>
   </dependency>
   
   <!--导入模板引擎-->
   <dependency>
       <groupId>org.freemarker</groupId>
       <artifactId>freemarker</artifactId>
       <version>2.3.31</version>
   </dependency>
   
   ```

3. 代码生成器示例

   ```java
   // 演示例子，执行 main 方法控制台输入模块表名回车自动生成对应项目目录中
   // 在控制台输入 m_user   m_blog
   public class CodeGenerator {
   
       /**
        * <p>
        * 读取控制台内容
        * </p>
        */
       public static String scanner(String tip) {
           Scanner scanner = new Scanner(System.in);
           StringBuilder help = new StringBuilder();
           help.append("请输入" + tip + "：");
           System.out.println(help.toString());
           if (scanner.hasNext()) {
               String ipt = scanner.next();
               if (StringUtils.isNotEmpty(ipt)) {
                   return ipt;
               }
           }
           throw new MybatisPlusException("请输入正确的" + tip + "！");
       }
   
       public static void main(String[] args) {
           // 代码生成器
           AutoGenerator mpg = new AutoGenerator();
   
           // 全局配置
           GlobalConfig gc = new GlobalConfig();
           String projectPath = System.getProperty("user.dir");
           gc.setOutputDir(projectPath + "/src/main/java");
   //        gc.setOutputDir("D:\\test");
           gc.setAuthor("陈天祥");
           gc.setOpen(false);
           // gc.setSwagger2(true); 实体属性 Swagger2 注解
           gc.setServiceName("%sService");
           mpg.setGlobalConfig(gc);
   
           // 数据源配置
           DataSourceConfig dsc = new DataSourceConfig();
           dsc.setUrl("jdbc:mysql://localhost:3306/自己连接的数据库?useUnicode=true&useSSL=false&characterEncoding=utf8&serverTimezone=UTC");
           // dsc.setSchemaName("public");
           dsc.setDriverName("com.mysql.cj.jdbc.Driver");
           dsc.setUsername("root");
           dsc.setPassword("密码");
           mpg.setDataSource(dsc);
   
           // 包配置
           PackageConfig pc = new PackageConfig();
           pc.setModuleName(null);
           pc.setParent("com.chen.vueblog");
           mpg.setPackageInfo(pc);
   
           // 自定义配置
           InjectionConfig cfg = new InjectionConfig() {
               @Override
               public void initMap() {
                   // to do nothing
               }
           };
   
           // 如果模板引擎是 freemarker
           String templatePath = "/templates/mapper.xml.ftl";
           // 如果模板引擎是 velocity
           // String templatePath = "/templates/mapper.xml.vm";
   
           // 自定义输出配置
           List<FileOutConfig> focList = new ArrayList<>();
           // 自定义配置会被优先输出
           focList.add(new FileOutConfig(templatePath) {
               @Override
               public String outputFile(TableInfo tableInfo) {
                   // 自定义输出文件名 ， 如果你 Entity 设置了前后缀、此处注意 xml 的名称会跟着发生变化！！
                   return projectPath + "/src/main/resources/mapper/"
                           + "/" + tableInfo.getEntityName() + "Mapper" + StringPool.DOT_XML;
               }
           });
   
           cfg.setFileOutConfigList(focList);
           mpg.setCfg(cfg);
   
           // 配置模板
           TemplateConfig templateConfig = new TemplateConfig();
   
           templateConfig.setXml(null);
           mpg.setTemplate(templateConfig);
   
           // 策略配置
           StrategyConfig strategy = new StrategyConfig();
           strategy.setNaming(NamingStrategy.underline_to_camel);
           strategy.setColumnNaming(NamingStrategy.underline_to_camel);
           strategy.setEntityLombokModel(true);
           strategy.setRestControllerStyle(true);
           strategy.setInclude(scanner("表名，多个英文逗号分割").split(","));
           strategy.setControllerMappingHyphenStyle(true);
           strategy.setTablePrefix("m_");
           mpg.setStrategy(strategy);
           mpg.setTemplateEngine(new FreemarkerTemplateEngine());
           mpg.execute();
       }
   }
   ```

   ``运行后,数据想要创建模板的表名,系统自动创建``

4. 分页插件

   ```java
   //Spring boot方式
   @Configuration
   @MapperScan("com.baomidou.cloud.service.*.mapper*")
   public class MybatisPlusConfig {
   
       // 旧版
       @Bean
       public PaginationInterceptor paginationInterceptor() {
           PaginationInterceptor paginationInterceptor = new PaginationInterceptor();
           // 设置请求的页面大于最大页后操作， true调回到首页，false 继续请求  默认false
           // paginationInterceptor.setOverflow(false);
           // 设置最大单页限制数量，默认 500 条，-1 不受限制
           // paginationInterceptor.setLimit(500);
           // 开启 count 的 join 优化,只针对部分 left join
           paginationInterceptor.setCountSqlParser(new JsqlParserCountOptimize(true));
           return paginationInterceptor;
       }
   }
   ```

5. Mybatis-Plus  **Service CRUD的接口** 使用

   ``ps:当传入是个wapper时候,可以用 new xxxWrapper<entity类> 包装一下xxx为想使用那种行为,,例如 查询Query,Update,在下面分页时候使用到了该方法``

   ### save

   ```java
   // 插入一条记录（选择字段，策略插入）
   boolean save(T entity);
   // 插入（批量）
   boolean saveBatch(Collection<T> entityList);
   // 插入（批量）
   boolean saveBatch(Collection<T> entityList, int batchSize);
   ```

   ##### 参数说明

   |     类型      |   参数名   |     描述     |
   | :-----------: | :--------: | :----------: |
   |       T       |   entity   |   实体对象   |
   | Collection<T> | entityList | 实体对象集合 |
   |      int      | batchSize  | 插入批次数量 |

   

   ### SaveOrUpdata

   ```java
   // TableId 注解存在更新记录，否插入一条记录
   boolean saveOrUpdate(T entity);
   // 根据updateWrapper尝试更新，否继续执行saveOrUpdate(T)方法
   boolean saveOrUpdate(T entity, Wrapper<T> updateWrapper);
   // 批量修改插入
   boolean saveOrUpdateBatch(Collection<T> entityList);
   // 批量修改插入
   boolean saveOrUpdateBatch(Collection<T> entityList, int batchSize);
   ```

   ##### 参数说明

   |     类型      |    参数名     |               描述               |
   | :-----------: | :-----------: | :------------------------------: |
   |       T       |    entity     |             实体对象             |
   |  Wrapper<T>   | updateWrapper | 实体对象封装操作类 UpdateWrapper |
   | Collection<T> |  entityList   |           实体对象集合           |
   |      int      |   batchSize   |           插入批次数量           |

   ### Remove

   ```java
   // 根据 entity 条件，删除记录
   boolean remove(Wrapper<T> queryWrapper);
   // 根据 ID 删除
   boolean removeById(Serializable id);
   // 根据 columnMap 条件，删除记录
   boolean removeByMap(Map<String, Object> columnMap);
   // 删除（根据ID 批量删除）
   boolean removeByIds(Collection<? extends Serializable> idList);
   ```

   ##### 参数说明

   |                类型                |    参数名    |          描述           |
   | :--------------------------------: | :----------: | :---------------------: |
   |             Wrapper<T>             | queryWrapper | 实体包装类 QueryWrapper |
   |            Serializable            |      id      |         主键ID          |
   |        Map<String, Object>         |  columnMap   |     表字段 map 对象     |
   | Collection<? extends Serializable> |    idList    |       主键ID列表        |

   ### Update

   ```java
   // 根据 UpdateWrapper 条件，更新记录 需要设置sqlset
   boolean update(Wrapper<T> updateWrapper);
   // 根据 whereEntity 条件，更新记录
   boolean update(T entity, Wrapper<T> updateWrapper);
   // 根据 ID 选择修改
   boolean updateById(T entity);
   // 根据ID 批量更新
   boolean updateBatchById(Collection<T> entityList);
   // 根据ID 批量更新
   boolean updateBatchById(Collection<T> entityList, int batchSize);
   ```

   ##### 参数说明

   |     类型      |    参数名     |               描述               |
   | :-----------: | :-----------: | :------------------------------: |
   |  Wrapper<T>   | updateWrapper | 实体对象封装操作类 UpdateWrapper |
   |       T       |    entity     |             实体对象             |
   | Collection<T> |  entityList   |           实体对象集合           |
   |      int      |   batchSize   |           更新批次数量           |

   ### Get

   ```java
   // 根据 ID 查询
   T getById(Serializable id);
   // 根据 Wrapper，查询一条记录。结果集，如果是多个会抛出异常，随机取一条加上限制条件 wrapper.last("LIMIT 1")
   T getOne(Wrapper<T> queryWrapper);
   // 根据 Wrapper，查询一条记录
   T getOne(Wrapper<T> queryWrapper, boolean throwEx);
   // 根据 Wrapper，查询一条记录
   Map<String, Object> getMap(Wrapper<T> queryWrapper);
   // 根据 Wrapper，查询一条记录
   <V> V getObj(Wrapper<T> queryWrapper, Function<? super Object, V> mapper);
   ```

   ##### 参数说明

   |            类型             |    参数名    |              描述               |
   | :-------------------------: | :----------: | :-----------------------------: |
   |        Serializable         |      id      |             主键ID              |
   |         Wrapper<T>          | queryWrapper | 实体对象封装操作类 QueryWrapper |
   |           boolean           |   throwEx    |   有多个 result 是否抛出异常    |
   |              T              |    entity    |            实体对象             |
   | Function<? super Object, V> |    mapper    |            转换函数             |

   ### List

   ```java
   // 查询所有
   List<T> list();
   // 查询列表
   List<T> list(Wrapper<T> queryWrapper);
   // 查询（根据ID 批量查询）
   Collection<T> listByIds(Collection<? extends Serializable> idList);
   // 查询（根据 columnMap 条件）
   Collection<T> listByMap(Map<String, Object> columnMap);
   // 查询所有列表
   List<Map<String, Object>> listMaps();
   // 查询列表
   List<Map<String, Object>> listMaps(Wrapper<T> queryWrapper);
   // 查询全部记录
   List<Object> listObjs();
   // 查询全部记录
   <V> List<V> listObjs(Function<? super Object, V> mapper);
   // 根据 Wrapper 条件，查询全部记录
   List<Object> listObjs(Wrapper<T> queryWrapper);
   // 根据 Wrapper 条件，查询全部记录
   <V> List<V> listObjs(Wrapper<T> queryWrapper, Function<? super Object, V> mapper);
   ```

   ##### 参数说明

   |                类型                |    参数名    |              描述               |
   | :--------------------------------: | :----------: | :-----------------------------: |
   |             Wrapper<T>             | queryWrapper | 实体对象封装操作类 QueryWrapper |
   | Collection<? extends Serializable> |    idList    |           主键ID列表            |
   |        Map<?String, Object>        |  columnMap   |         表字段 map 对象         |
   |    Function<? super Object, V>     |    mapper    |            转换函数             |

   ### Page

   ```java
   // 无条件分页查询
   IPage<T> page(IPage<T> page);
   // 条件分页查询
   IPage<T> page(IPage<T> page, Wrapper<T> queryWrapper);
   // 无条件分页查询
   IPage<Map<String, Object>> pageMaps(IPage<T> page);
   // 条件分页查询
   IPage<Map<String, Object>> pageMaps(IPage<T> page, Wrapper<T> queryWrapper);
   ```

   示例: 查询所有blogs为例

   ```java
   @GetMapping("/blogs")
       public Result list(@RequestParam(defaultValue = "1") Integer currentPage) {
           // 分页,按照created倒序
           Page page = new Page(currentPage, 5);
           IPage pageData = blogService.page(page, new QueryWrapper<Blog>().orderByDesc("created"));
           return Result.succ(pageData);
       }
   ```

   ##### 参数说明

   |    类型    |    参数名    |              描述               |
   | :--------: | :----------: | :-----------------------------: |
   |  IPage<T>  |     page     |            翻页对象             |
   | Wrapper<T> | queryWrapper | 实体对象封装操作类 QueryWrapper |

6. **MapperCRUD接口**

   ### insert

   ```java
   // 插入一条记录
   int insert(T entity);
   ```

   ##### 参数说明

   | 类型 | 参数名 |   描述   |
   | :--: | :----: | :------: |
   |  T   | entity | 实体对象 |

   ### Delete

   ```java
   // 根据 entity 条件，删除记录
   int delete(@Param(Constants.WRAPPER) Wrapper<T> wrapper);
   // 删除（根据ID 批量删除）
   int deleteBatchIds(@Param(Constants.COLLECTION) Collection<? extends Serializable> idList);
   // 根据 ID 删除
   int deleteById(Serializable id);
   // 根据 columnMap 条件，删除记录
   int deleteByMap(@Param(Constants.COLUMN_MAP) Map<String, Object> columnMap);
   ```

   ##### 参数说明

   |                类型                |  参数名   |                描述                |
   | :--------------------------------: | :-------: | :--------------------------------: |
   |             Wrapper<T>             |  wrapper  | 实体对象封装操作类（可以为 null）  |
   | Collection<? extends Serializable> |  idList   | 主键ID列表(不能为 null 以及 empty) |
   |            Serializable            |    id     |               主键ID               |
   |        Map<String, Object>         | columnMap |          表字段 map 对象           |

   ### Update

   ```java
   // 根据 whereEntity 条件，更新记录
   int update(@Param(Constants.ENTITY) T entity, @Param(Constants.WRAPPER) Wrapper<T> updateWrapper);
   // 根据 ID 修改
   int updateById(@Param(Constants.ENTITY) T entity);
   ```

   ##### 参数说明

   |    类型    |    参数名     |                             描述                             |
   | :--------: | :-----------: | :----------------------------------------------------------: |
   |     T      |    entity     |               实体对象 (set 条件值,可为 null)                |
   | Wrapper<T> | updateWrapper | 实体对象封装操作类（可以为 null,里面的 entity 用于生成 where 语句） |

   ### Select

   ```java
   // 根据 ID 查询
   T selectById(Serializable id);
   // 根据 entity 条件，查询一条记录
   T selectOne(@Param(Constants.WRAPPER) Wrapper<T> queryWrapper);
   
   // 查询（根据ID 批量查询）
   List<T> selectBatchIds(@Param(Constants.COLLECTION) Collection<? extends Serializable> idList);
   // 根据 entity 条件，查询全部记录
   List<T> selectList(@Param(Constants.WRAPPER) Wrapper<T> queryWrapper);
   // 查询（根据 columnMap 条件）
   List<T> selectByMap(@Param(Constants.COLUMN_MAP) Map<String, Object> columnMap);
   // 根据 Wrapper 条件，查询全部记录
   List<Map<String, Object>> selectMaps(@Param(Constants.WRAPPER) Wrapper<T> queryWrapper);
   // 根据 Wrapper 条件，查询全部记录。注意： 只返回第一个字段的值
   List<Object> selectObjs(@Param(Constants.WRAPPER) Wrapper<T> queryWrapper);
   
   // 根据 entity 条件，查询全部记录（并翻页）
   IPage<T> selectPage(IPage<T> page, @Param(Constants.WRAPPER) Wrapper<T> queryWrapper);
   // 根据 Wrapper 条件，查询全部记录（并翻页）
   IPage<Map<String, Object>> selectMapsPage(IPage<T> page, @Param(Constants.WRAPPER) Wrapper<T> queryWrapper);
   // 根据 Wrapper 条件，查询总记录数
   Integer selectCount(@Param(Constants.WRAPPER) Wrapper<T> queryWrapper);
   ```

   ##### 参数说明

   |                类型                |    参数名    |                   描述                   |
   | :--------------------------------: | :----------: | :--------------------------------------: |
   |            Serializable            |      id      |                  主键ID                  |
   |             Wrapper<T>             | queryWrapper |    实体对象封装操作类（可以为 null）     |
   | Collection<? extends Serializable> |    idList    |    主键ID列表(不能为 null 以及 empty)    |
   |        Map<String, Object>         |  columnMap   |             表字段 map 对象              |
   |              IPage<T>              |     page     | 分页查询条件（可以为 RowBounds.DEFAULT） |



### 到此,Mybatis-Plus总结告一段落,足够开发中用的了!