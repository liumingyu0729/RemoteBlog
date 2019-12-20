---
title: Spring-Boot
date: 2019-12-16 15:46:13
tags:
---
Spring Boot CLI 安装
&emsp;Windows 解压到JAVA_HOME
&emsp;Unix 用Software Development Kit Manager(SDKAMN) (需要命令行补全)
&emsp;OS X Homebrew MacPorts
Spring Initializr
&emsp;Web界面 https://start.spring.io/
&emsp;Spring Tool Suite
&emsp;IntelliJ IDEA
&emsp;Spring Boot CLI
&emsp;构建工具 Gradle (Groovy) Maven
&emsp;src/main/java 应用程序
&emsp;src/main/resource 资源
&emsp;src/main/test 测试代码
&emsp;build.gradle Gradle构建文件说明
&emsp;XXXApplication.java 应用程序的启动引导类（bootstrap class）
&emsp;application.properties 用于配置应用程序和Spring Boot属性（server.port = 8000）
&emsp;XXXApplicationTests.java 基本测试类
&emsp;Thymeleaf
&emsp;Spring Data JPA

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