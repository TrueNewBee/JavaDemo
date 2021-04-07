![image-20210228102501219](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228102501219.png)

### 在web.xml中 

![image-20210228103319502](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228103319502.png)

### 上面监听器,了解就行

![image-20210228104033561](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228104033561.png)

**配置**

![image-20210228104153590](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228104153590.png)

### 监听器的使用

![image-20210228104500291](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228104500291.png)

![image-20210228104842268](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228104842268.png)

### Spring集成web环境如上

![image-20210228110133202](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228110133202.png)



![image-20210228110244972](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228110244972.png)

1. 

![image-20210228110851906](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228110851906.png)

2. web.xml

![image-20210228110831364](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228110831364.png)

3. 4.  创建controller文件/jsp文件

<img src="C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228111355331.png" alt="image-20210228111355331" style="zoom:150%;" />

5.扫描组件

![image-20210228111548171](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228111548171.png)

6. 在web.xml中配置

   ![image-20210228111717965](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228111717965.png)

**流程图**

![image-20210228112023419](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228112023419.png)

# Spring模型流程图

![image-20210228112628171](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228112628171.png)



# 底层组件流程 

![image-20210228112728405](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228112728405.png)



### SpringMVC注解解析

![image-20210228115608101](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228115608101.png)

![image-20210228115905717](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228115905717.png)

![image-20210228120726720](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228120726720.png)



![image-20210228121031578](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228121031578.png)

# Spring MVC 具体应用

![image-20210228132116518](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228132116518.png)



## 页面跳转

![image-20210228133236527](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228133236527.png)

### 仿佛Django中返回给模板数据,在模板中去取数据

![image-20210228133743572](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228133743572.png)

![image-20210228133824327](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228133824327.png)

![image-20210228133833036](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228133833036.png)

## 注入方式传递数据

![image-20210228134105209](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228134105209.png)



### 返回字符串

![image-20210228134909293](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228134909293.png)

![image-20210228135123008](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228135123008.png)

### 返回json数据

导包 

![image-20210228135552870](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228135552870.png)



代码逻辑

![image-20210228135946812](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228135946812.png)

## 通过Spring MVC 返回对象或集合

![image-20210228140531396](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228140531396.png)

![image-20210228140550890](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228140550890.png)

上述过程极其繁琐,,故通过 mvc的注解驱动即可

![image-20210228141313643](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228141313643.png)

![image-20210228141407656](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228141407656.png)

# 知识总结

![image-20210228142021280](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228142021280.png)

**获取的参数**

![image-20210228142316609](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228142316609.png)

### 基本数据类型参数

![image-20210228142829018](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228142829018.png)

### 封装一个实体 POJO类型参数

![image-20210228143608407](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228143608407.png)

### 获取数组类型参数

![image-20210228145540516](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228145540516.png)

**获取集合**

![image-20210228151933123](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228151933123.png)

### 静态资源访问权限:

![image-20210228152429320](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228152429320.png)

### 配置过滤得 filter

![image-20210228152840427](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228152840427.png)

### 注解绑定

![image-20210228153839612](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228153839612.png)

![image-20210228154208008](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228154208008.png)![image-20210228154600693](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228154600693.png)

![image-20210228154743913](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228154743913.png)



### 直接获得cookie值的注解

![image-20210228163710844](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210228163710844.png)



## 上传表单

![image-20210301093524854](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210301093524854.png)

![image-20210301112946622](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210301112946622.png)

![image-20210301112956012](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210301112956012.png)

![image-20210301172952272](C:\Users\Administrator\Desktop\SpringMVC框架\SpringMVC笔记.assets\image-20210301172952272.png)