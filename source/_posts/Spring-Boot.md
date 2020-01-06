---
title: Spring-Boot
date: 2019-12-16 15:46:13
tags:
---
约定大于配置
微服务：架构风格
一个应用可以是一组小型服务，可以通过HTTP互通

### Maven安装
http://maven.apache.org/download.cgi 解压
环境变量
M2_HOME XXXapache-maven-3.5.0
Path %M2_HOME%\bin
mvn -v
### Maven设置
XXXapache-maven-3.6.0\conf\settings.xml
~~~
<profile>
    <id>jdk-13.0.1</id>
    <activation>
        <activeByDefault>true</activeByDefault>
        <jdk>13.0.1</jdk>
    </activation>
    <properties>
        <maven.compiler.source>13.0.1</maven.compiler.source>
        <maven.compiler.target>13.0.1</maven.compiler.target>
        <maven.compiler.compilerVersion>13.0.1</maven.compiler.compilerVersion>
    </properties>
</profile>
~~~
本地仓库配置
~~~
<localRepository>XXXmaven-repository\repository</localRepository>
~~~
把配置好的settings.xml复制一份到maven-repository并配置阿里云仓库地址
~~~
<mirror>  
	<id>nexus-aliyun</id>  
	<mirrorOf>central</mirrorOf>    
	<name>Nexus aliyun</name>  
	<url>http://maven.aliyun.com/nexus/content/groups/public</url>  
</mirror>
~~~
mvn help:system测试
### Intellij IDEA设置
configure -> setting -> Build, Execution, Deployment -> Build Tool -> Maven
Maven home directory: 从IDE自带换成安装的Maven
User settings file: XXXmaven-repository\settings.xml 打勾
Local repository: XXXmaven-repository\repository 打勾
Ctrl + click 连接
Alt + Insert Getter and Setter 创建方法 
Ctrl + / 注释

### 创建Maven工程（jar）
### 导入依赖Spring Boot相关依赖
Maven project need to be imported 自动导入依赖
https://spring.io/projects/spring-boot/ Quick Start
~~~
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.2.2.RELEASE</version>
    <relativePath/> <!-- lookup parent from repository -->
</parent>
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
~~~
### 编写主程序：启动Spring Boot应用
src\main\java 路径下新建类 包名（groupId）+ .类名
~~~
@SpringBootApplication
public class Hello {
    public static void main(String[] args) {
        SpringApplication.run(Hello.class,args);
    }
}
~~~
### 编写相关的Controller、Service
包右键新建 controller.类名
~~~
@Controller
public class HelloController {
    @ResponseBody
    @RequestMapping("/hello")
    public String helloFun(){
        return "Hello World";
    }
}
~~~
运行main
http://localhost:8080/hello 传/hello到服务端 返回Hello World
### 简化部署
https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/html/getting-started.html#getting-started
Creating an Executable Jar 打包成一个jar包
~~~
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
~~~
Lifecycle package 打包
jar包可用压缩文件打开
java -jar 执行

## POM文件
###父项目
~~~
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.2.2.RELEASE</version>
    <relativePath/> <!-- lookup parent from repository -->
</parent>
~~~
它的父项目
~~~xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-dependencies</artifactId>
    <version>2.2.2.RELEASE</version>
    <relativePath>../../spring-boot-dependencies</relativePath>
</parent>
~~~
管理Spring Boot应用里所有依赖版本
版本仲裁中心：处理默认版本

 依赖关系图：右键 -> Diagrams -> Show Dependencies  Ctrl+滚轮 放大缩小

### 导入依赖

https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/html/using-spring-boot.html#using-boot

~~~
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
~~~
spring-boot-starter：Spring Boot场景启动器
@SpringBootApplication：Spring Boot主配置类（main方法）


@SpringBootConfiguration：Sring Boot配置类
@Configuration：配置类（一个组件@Componet）
@EnableAutoConfiguration：开启自动配置功能
@AutoConfigurationPackage：自动配置包 
由AutoConfigurationPackages.Registrar.class将主配置类所在包及子包所有组件加到Spring容器
@Import() 给容器导入组件
## Spring Initializer快速创建Spring Boot项目
https://start.spring.io/
@RestController = @Controller + @ResponseBody

resource文件夹

* static 静态资源（js css image）

* templates 保存所有的模板页面（Sping Boot默认jar嵌入Tomcat 默认不支持js p 模板引擎freemaker thymeleaf）
* application.properties Spring Boot应用配置文件，支持松散绑定（修改全局默认配置server.port=8081）

application.yml 另一种Spring Boot应用配置文件

YAML 以数据为中心

~~~yml
friend:
  name: ls
  age: 20
friend: {name: ls,age: 20}
pets:
  - cat
  - dog
  - pig
pets: [cat,dog,pig]
~~~
key:空格value:空格 
缩进控制层级关系（左对齐）
字符串不用引号 “转义特殊字符 ‘不转义特殊字符
@Component
@ConfigurationProperties(prefix = "friend") 类中属性和配置文件绑定 乱码用setting格式转换
@RunWith(SpringRunner.class) 测试期间注入容器
application.properties
friend.name = ls
pets = cat,dog,pig
@Value(#{friend.name}) 环境变量、配置文件、#{} SpEL 获取值

|                      | @ConfigurationProperties |  @Value  |
| :------------------: | :----------------------: | :------: |
|         功能         |         批量注入         | 单个指定 |
| 松散绑定（松散语法） |           支持           |  不支持  |
|         SpEL         |          不支持          |   支持   |
|    JSR303数据校验    |           支持           |  不支持  |
|     复杂类型封装     |           支持           |  不支持  |

@PropertySource(value = {"classpath:XXX.properities"}) 加载指定的配置文件

@ImportResource(lacations= {"classpath:XXX.xml"}) 导入Spring配置文件

推荐使用配置类

* @Configuration 当前类是Spring Boot配置类 代替配置文件

* @Bean  

### 配置文件占位符

* ${random.value} 
* ${person.hello:hello}

### Profile 切换环境

application-XXX.properties/yml

application.properties 中激活 spring.profiles.active=XXX

yaml文件文档块

~~~yaml
server:
    port:8081
spring:
    profiles:
        active:dev
---
server:
    port:8082
spring:
    profiles:dev
---
server:
    port:8083
spring:
    profiles:prod
~~~

虚拟机参数 Run/Debug Configuration

VM options: -Dspring.profiles.active=dev

### 配置文件加载位置

优先级由高到低 互补配置

* file: ./config/
* file: ./
* classpath: /config/
* classpath: /

### 命令行更改配置

--server.port = 8082

由jar包外向jar包内寻找 优先加载pofile

### 自动配置

示例

~~~Spring Boot
@Configuration
@EnableConfigurationProperties(HttpEncodingProperties.class)
@ConfitionalOnWebApplication
@ConditionalOnClass(CharacterEncodingFilter.class)
@ConditionalOnProperty(prefix="spring.http.encoding", value="enabled", matchIfMissing=true)

@Bean //给容器添加组件
@ConditionalOnMissingBean(CharacterEncodingFilter.class)
~~~

Properties文件 debug = true #开启Spring Boot的debug模式

## 日志

|             日志门面              |          日志实现           |
| :-------------------------------: | :-------------------------: |
| ~~JCL~~、SLF4j、~~jboss-logging~~ | Log4j、JUL、Log4j2、Logback |

Spring默认JCL

Spring Boot选用SLF4j + Logback

### SLF4j

系统中使用SLF4j

~~~java
Logger logger = LoggerFactory.getLogger(XXX.class); //记录器
logger.info("XXX");
~~~

遗留问题：jar包将其他日志转为SLF4j  

引入其他框架时时，要移除原有日志框架

properties文件 logging.level.包 = trace debug 日志级别默认 info warn error

 logging.path  logging.file  默认只输出在控制台

### 日志指定配置

logback.xml 日志框架识别

logback.spring.xml 由Spring Boot识别，可以指定某段配置在某环境下识别

~~~xml
<sptingProfile name="dev">
</sptingProfile>sptingProfile>
~~~

静态资源映射

* classpath: /META-INF/resources/
* classpath: /resources/
* classpath: /static/
* classpath: /public/
* 当前项目根目录

欢迎页：静态资源文件夹下所有index.html

XXX/favicon.ico也是在静态资源文件夹下查找

properties文件指定静态路径（逗号分割） spring.resources.static-locations=classpath:/XXX,/XXX/XXX

以jar包引入资源：所有/webjars/** 在class path：/META-INF/resources/webjars/

查依赖 https://www.webjars.org/

“/**”访问当前项目任何资源  

* classpath:/HETA-INF/resources/
* classpath:/resources/
* classpath:/static/
* classpath:/public/
* / 项目根路径

### 模板引擎

JSP、Velocity、Freemarker、Thymeleaf

Thymeleaf

~~~java
private String prefix = "classpath:/templates/";
private String suffix = ".html";
//把html页面放在classpath:/templates/，Thymeleaf可以自动渲染
~~~

