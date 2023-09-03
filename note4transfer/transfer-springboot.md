# springboot

## 参考
- [java学习路线](https://zhuanlan.zhihu.com/p/379041500)
- [javaGuide](https://github.com/Snailclimb/JavaGuide)
- [springBoot官方文档](https://docs.spring.io/spring-boot/docs/current/reference/html/)
  - [starters](https://docs.spring.io/spring-boot/docs/current/reference/html/using.html#using.build-systems.starters)
  - [配置项](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#appendix.application-properties)
- 网课
  - [网课：尚硅谷Spring Boot2 零基础入门](https://www.bilibili.com/video/av885722084)
  - [网课文档](https://www.yuque.com/atguigu/springboot)
  - [网课源码](https://gitee.com/leifengyang/springboot2)

## java8安装与配置
- mac
  - [安装java8](https://www.java.com/zh-CN/)
  - dmg格式，直接安装即可，无需配置
  - `java -help` 检测是否安装成功
  - `java -version` 返回 `java version "1.8.0_321"`
  - 安装maven `brew install maven`
  - `mvn -version` 返回 `Apache Maven 3.8.4`
- win
  - 参考[maven教程](http://c.biancheng.net/maven2/install-configure.html)

## 杂
- [JVM vs JDK vs JRE](https://javaguide.cn/java/basis/java-basic-questions-01/#jvm-vs-jdk-vs-jre)
  - JVM：Java 虚拟机（JVM）是运行 Java 字节码的虚拟机。JVM 有针对不同系统的特定实现（Windows，Linux，macOS），目的是使用相同的字节码，它们都会给出相同的结果。JVM 实现是 Java 语言“一次编译，随处可以运行”的关键所在。
  - JRE：Java 运行时环境。它是运行已编译 Java 程序所需的所有内容的集合，包括 Java 虚拟机（JVM），Java 类库，java 命令和其他的一些基础构件。但是，它不能用于创建新程序。
  - JDK：Java Development Kit 缩写，它是功能齐全的 Java SDK。它拥有 JRE 所拥有的一切，还有编译器（javac）和工具（如 javadoc 和 jdb）。它能够创建和编译程序。如果你只是为了运行一下 Java 程序的话，那么你只需要安装 JRE 就可以了。如果你需要进行一些 Java 编程方面的工作，那么你就需要安装 JDK 了。
  - SDK：是Software Development Kit的缩写，中文意思是“软件开发工具包”。这是一个覆盖面相当广泛的名词，可以这么说：辅助开发某一类软件的相关文档、范例和工具的集合都可以叫做“SDK”。
  - 自从Java推出以来，JDK已经成为使用最广泛的Java SDK。可以认为jdk只是sdk的一种(子集)，因为它是开发java程序的一个平台，开发其他程序的sdk可以没有jdk。
- [版本称呼](https://cloud.tencent.com/developer/article/1873446)
  - Java有3个版本：J2SE(Java Platform，Standard Edition)、J2EE(Java Platform，Enterprise Edition)、J2ME(Java Platform，Micro Edition)，所以J2SE是3个版本中的其中一个，即标准版本。
  - Java与JDK的区别与关系：这个应该是看问题的角度不同，在用户眼中，Java是Java应用，而在程序员眼中，JDK是Java开发工具，所以Java等价于JDK。
  - JDK8与JDK1.8的区别与关系：JDK8或者JDK1.8是由于自从JDK1.5/JDK5命名方式改变后遗留的新旧命令方式问题，所以JDK8或者JDK1.8也是同一个东西。
- java Bean：一种JAVA语言写成的可重用组件，类必须是具体的和公共的，并且具有无参数的构造器。可以被Applet、Servlet、JSP等Java应用程序调用．也可以可视化地被Java开发工具使用。它包含属性(Properties)、方法(Methods)、事件(Events)等特性。

## IDEA
- [官网下载: Community Edition](https://www.jetbrains.com/idea/download)
- 插件搜索`Chinese`下载中文语言包
- 插件搜索`Spring Intilializr and Assistant`下载

### IDEA配置maven
- 配置maven(mac下)
```sh
mvn -v #查看Maven home地址，例如 /opt/homebrew/Cellar/maven/3.8.4/libexec
# 找到对应的settting.xml，例如 /opt/homebrew/Cellar/maven/3.8.4/libexec/conf/settings.xml
# 在conf目录下新建repo目录，得到仓库目录，例如/opt/homebrew/Cellar/maven/3.8.4/libexec/conf/repo
vim /opt/homebrew/Cellar/maven/3.8.4/libexec/conf/settings.xml
```
- 编辑maven配置文件settings.xml
```xml
<!-- 根据注释找到对应位置，添加 -->
<localRepository>/opt/homebrew/Cellar/maven/3.8.4/libexec/conf/repo</localRepository>

<!-- 在</mirrors>前添加如下内容 -->
  <mirror>
		<id>alimaven</id>
		<name>aliyun maven</name> 
		<url>http://maven.aliyun.com/nexus/content/groups/public/</url> 
		<mirrorOf>central</mirrorOf>
	</mirror>
```
- 打开idea -> 左上角idea -> preferences -> maven -> 填写对应地址
```
主路径：/opt/homebrew/Cellar/maven/3.8.4/libexec
用户设置文件：/opt/homebrew/Cellar/maven/3.8.4/libexec/conf/settings.xml
本地仓库：/opt/homebrew/Cellar/maven/3.8.4/libexec/conf/repo
```

### 语法
- IDEA -> 新建空项目 -> 新建java类 HelloWorld -> 输入以下代码 -> 运行main函数（旁边绿色三角）
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("你好，世界！");
    }
}
```
- 其他基础语法见 `/Users/zeng/code/backend/java/0-java_base/HelloWorld.java`

## 网课笔记
- v1.0 只记录了看懂并且需要用到的

### P1~4 介绍
- 略

### P5 - hello world
- 注意：以下是创建maven项目的步骤，实际开发使用Spring Initialzr构建springboot项目会更加方便(参考P16-19)
- 环境要求
```sh
# java8及以上
java -version
# maven 3.3+
mvn -v
```
- maven设置，修改maven路径下的setting.xml（/opt/homebrew/Cellar/maven/3.8.4/libexec/conf/settings.xml），添加或者修改以下信息
```xml
<mirrors>
      <mirror>
        <id>nexus-aliyun</id>
        <mirrorOf>central</mirrorOf>
        <name>Nexus aliyun</name>
        <url>http://maven.aliyun.com/nexus/content/groups/public</url>
      </mirror>
</mirrors>
 
<profiles>
        <profile>
            <id>jdk-1.8</id>
            <activation>
              <activeByDefault>true</activeByDefault>
              <jdk>1.8</jdk>
            </activation>
            <properties>
              <maven.compiler.source>1.8</maven.compiler.source>
              <maven.compiler.target>1.8</maven.compiler.target>
              <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
            </properties>
        </profile>
</profiles>
```
- 配置idea中的maven路径: preferences -> maven -> 填写对应地址
- idea -> 新建项目 -> maven直接下一步 -> [新建maven项目](https://tree0312.com/img/img-202302241216.png)
- 修改pom.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.atguigu</groupId>
    <artifactId>boot-01-helloworld</artifactId>
    <version>1.0-SNAPSHOT</version>
    <!--  使用spring boot  -->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.3.4.RELEASE</version>
    </parent>
    <!--  web开发相关依赖  -->
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>
    <!--  打包成jar包  -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

</project>
```
- 等待maven安装依赖
- [新建MainApplication类，编写主程序代码](https://tree0312.com/img/img-202302241217.png)
```java
package com.atguigu.boot;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
/**
 * 主程序类
 * @SpringBootApplication：这是一个SpringBoot应用
 */
@SpringBootApplication
public class MainApplication {

    public static void main(String[] args) {
        SpringApplication.run(MainApplication.class,args);
    }
}
```
- [新建helloController](https://tree0312.com/img/img-202302241218.png)
```java
package com.atguigu.boot.controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
@RestController
public class HelloController {
    @RequestMapping("/hello")
    public String handle01(){
        return "Hello, Spring Boot 2!";
    }
}
```
- 新建 resources/application.properties，修改配置项
```java
server.port = 8888
```
- 点击主程序main函数左边的三角，运行项目
- 访问 [网址](http://localhost:8888/hello)
- 检验成功后，点击右上角红框，停止项目
- 打包：右侧maven栏 -> 生命周期选择clean和package（按住command进行多选）-> 上面绿三角 -> 生成target文件夹
```sh
# 进入target文件夹的终端
java -jar boot-01-helloworld-1.0-SNAPSHOT.jar
```
- 访问 `http://localhost:8888/hello`
- mac下终止jar包的运行
  - 使用命令 sudo lsof -i :xxxx (xxxx即为端口号)查看进程号
  - 使用命令 kill -9 aaaa (aaaa为PID)
- 可以通过压缩工具打开jar包，查看jar包里面的内容，例如pom.xml、生成的class文件、引用的lib、
- 后续
    - 在pom.xml中引用相关依赖，通过右侧maven查看依赖性层级关系
    - 在application.properties修改配置
    - 规划目录结构，编写业务代码
    - 调试、启动、打包


### P6~P15 - 自动配置原理
- 略

### P16~P19 - 实践技巧
- 基础
    - 引入场景依赖starter
    - 查看场景自动配置了什么东西（可选项，需要分析依赖源码、配置项debug = true查看报告）
    - 自动配置不满足需求，可以修改配置项
    - 依赖无法满足需求，可以自定义组件或功能
    - 业务逻辑

- lombok
    - [如果搜索不到插件，那应该是新版本的IDEA已经集成了lombok](https://plugins.jetbrains.com/plugin/6317-lombok/versions)
    - 作用：利用注解简化javabean开发
      - @Data 自动生成属性的get和set方法
      - @ToString 自动重写ToString方法
      - @AllArgsConstructor 自动生成全参构造器
      - @NoArgsConstructor 自动生成无参构造器
      - @Slf4j 日志打印功能，可以用`log.info`代替`System.out.println`
      - 省略某个参数的构造器需要自己写

- dev-tools
    - 修改代码后，点击 绿色锤子 图标可以重新构建然后变更就生效了
    - 实际上是自动重启，真正热更新需要用到付费的 JRebel

- Spring Initialzr
    - 初始化向导 default
    - 选择 projectType（Maven）、java8、
    - 勾选 springboot2.x \ Develper Tools(全选，里面会有lombok和dev-tools) \ Web(Spring Web) \ 可选SQL(JDBC API, MYSQL) \ 其他自选
    - 如果是打开项目的时候构建失败
      - 可以尝试删除根目录多余文件（剩下src/和pom.xml），然后文件 -> 清除缓存饼重新启动idea，然后再重新构建
      - 如果还不行
        - 查看 preferences -> maven配置，把项目的maven路径从包装器改回本地
        - 查看 文件 -> 项目结构 -> 模块，把sdk换一下


### P20~P21 - 配置文件
- [yaml的用法](https://www.yuque.com/atguigu/springboot/rg2p8g)

### p22 - Web开发
- 对应代码：/Users/zeng/code/backend/java/boot-05-web-01

#### P23 - 访问静态资源
- 在 resource/static 下存放的资源文件(图片、视频、网页等),例如 xxx.png 可以通过 ip:port/xxx.png 访问
- 如果静态资源等路径和接口请求的路径冲突，需要根据顺序处理请求：先看controller能否动态映射，再看静态映射，再404
- 为了方便后续处理（拦截、区分等），可以在 配置项中 加上访问前缀
```properties
# 默认值 /** 表示静态映射
spring.mvc.static-path-pattern=/res/**
```

#### P24 - 设置index.html和favicon
- 前提：如果配置项设置了static-path-pattern，需要先注释掉
- 在 resource/static 下存放 index.html 和 favicon.ico 就可以通过 ip:port 访问

#### P26 - REST风格
- 对应代码：/Users/zeng/code/backend/java/boot-05-web-01/.../UserController
- Rest风格支持（使用HTTP请求方式动词来表示对资源的操作）
  - 以前：/getUser 获取用户     /deleteUser 删除用户    /editUser 修改用户       /saveUser 保存用户
  - 现在： /user   GET-获取用户    DELETE-删除用户     PUT-修改用户      POST-保存用户
- 可以用postman测试，例如 `PUT请求` - `http://localhost:8080/user`

#### P28 - 请求映射原理
- 略

#### P29 - 参数处理
- 对应代码：/Users/zeng/code/backend/java/boot-05-web-01/.../RequestController
- 获取参数：路径变量、请求头、请求param、请求体
  - 方法一：通过注解
  - 方法二：通过Servlet API


#### P37~42 - 内容协商策略
- 同一个接口可以返回不同的内容，例如给pc返回json、给手机返回xml...

### P43 - 视图解析(Thymeleaf)
- 对应代码：/Users/zeng/code/backend/java/boot-05-web-01/.../ThymeleafController
- 引入 Thymeleaf
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```
- 在 @/resources/templates/ 下新建html页面(需要给html标签添加xmlns:th属性)


### P48 - 拦截器
- 例子：登录拦截
- 对应代码：/Users/zeng/code/backend/java/boot-05-web-01/.../
  - UserController
  - LoginInterceptor
  - AdminWebConfig

### P50 - 文件上传
- 略

### P60 -  数据访问
- 对应代码：/Users/zeng/code/backend/java/boot-06-data-01/
- 安装mysql
- Spring Intilializr新建项目 boot-06-data-01
- 选择lombook \ web等， 暂时不用选SQL，后续自行添加
- pom.xml导入jdbc和mysql驱动（版本选择：https://mvnrepository.com/artifact/mysql/mysql-connector-java）

```xml

<!--		导入JDBC-->
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jdbc</artifactId>
		</dependency>
<!--		导入MYSQL驱动，需要选择与数据库版本对应的驱动版本-->
		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<version>5.1.49</version>
		</dependency>
```

- 刷新maven安装上述依赖
- application.properties 填写数据库连接信息

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/db_account?useSSL=true
spring.datasource.username=root
spring.datasource.password=MYSQLmysql123456?
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
spring.jdbc.template.query-timeout=3000
```

- 测试：修改test/java/.../Boot06Data01ApplicationTests.java，运行contextLoads()
```java
@Slf4j
@SpringBootTest
class Boot06Data01ApplicationTests {
  @Autowired
  JdbcTemplate jdbcTemplate;
  @Test
  void contextLoads() {
//        jdbcTemplate.queryForObject("select * from account_tbl")
//        jdbcTemplate.queryForList("select * from account_tbl",)
    Long aLong = jdbcTemplate.queryForObject("select count(*) from account_tb1", Long.class);
    log.info("记录总数：{}",aLong);
  }
}
```

#### P61~P62 - 数据库整合Druid
- 作用：数据库连接池、sql监控、sql防火墙、
- [官方github](https://github.com/alibaba/druid)
- 对应代码：/Users/zeng/code/backend/java/boot-06-data-01/.../
  - pom.xml 引入druid的starter
  - application.yaml 配置 druid
  - DataController 使用druid，访问 http://localhost:8080/sql 发送请求
- 访问Druid监控页面：http://localhost:8080/druid/index.html

#### P65~68 - 数据库整合MyBatis-Plus
- 作用：简化数据库增删查改
- 对应代码：/Users/zeng/code/backend/java/boot-06-data-01/.../
  - pom.xml 引入MyBatis-Plus的starter
  - application.yaml 配置 MyBatis-Plus
  - 创建MyBatisConfig，添加自定义的配置
  - 创建自定义Bean之 Account_tb1，用来接收account_tb1表
  - 创建接口 AccountMapper，绑定 Account_tb1
  - 创建服务层之 AccountService
  - 创建 AccountService 的实现类 AccountServiceImpl
  - 以上几步完成后，服务层的AccountService就能自动获得CRUD的功能
  - DataController 使用 服务层的AccountService，实现增删查改
- 访问 http://localhost:8080/mp-sql 发送请求

### 自行扩展
- 返回图片：/Users/zeng/code/backend/java/boot-05-web-01/.../RequestController
- MyBatis-Plus使用自定义的sql语句：待定