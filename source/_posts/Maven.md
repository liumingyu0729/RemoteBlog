---
title: Maven
date: 2019-12-23 11:34:57
tags:
---
### Maven：Java项目管理和构建工具
a-maven-project
├── pom.xml
├── src
│   ├── main
│   │   ├── java
│   │   └── resources
│   └── test
│       ├── java
│       └── resources
└── target
a-maven-project 是项目名
src/main/java Java源码的目录
src/main/resources 存放资源文件的目录
src/test/java 存放测试源码的目录
src/test/resources 存放测试资源的目录
pom.xml 项目描述文件
~~~
<project ...>
	<modelVersion>4.0.0</modelVersion>
	<groupId>com.itranswarp.learnjava</groupId>
	<artifactId>hello</artifactId>
	<version>1.0</version>
	<packaging>jar</packaging>
	<properties>
        ...
	</properties>
	<dependencies>
        <dependency>
            <groupId>commons-logging</groupId>
            <artifactId>commons-logging</artifactId>
            <version>1.2</version>
        </dependency>
	</dependencies>
</project>
~~~
groupId 类似于Java的包名，通常是公司或组织名称
artifactId 类似于Java的类名，通常是项目名称
Maven工程 groupId、artifactId和version作为唯一标识（引用其他第三方库）
环境变量
~~~
M2_HOME=/path/to/maven-3.6.x
PATH=$PATH:$M2_HOME/bin
~~~
Windows可以把%M2_HOME%\bin添加到系统Path变量中
mvn -version
### 依赖关系

scope | 说明 | 示例
:-: | :-: | :-:
compile | 编译时需要用到该jar包（默认）| commons-logging
test | 编译Test时需要用到该jar包 | junit
runtime | 编译时不需要，但运行时需要用到 | mysql
provided | 编译时需要用到，但运行时由JDK或某个服务器提供 | servlet-api

Maven从中央仓库（repo1.maven.org）所需依赖下载到本地（或镜像仓库）
~~~
<settings>
    <mirrors>
        <mirror>
            <id>aliyun</id>
            <name>aliyun</name>
            <mirrorOf>central</mirrorOf>
            <!-- 国内推荐阿里云的Maven镜像 -->
            <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
        </mirror>
    </mirrors>
</settings>
~~~
以SNAPSHOT-开头的版本号会被Maven视为开发版本
### 构建流程
lifecycle 生命周期
phase 阶段（内置的生命周期default）（对应plugin）
mvn package
mvn compile
mvn clean 清理所有生成的class和jar
mvn clean compile 先清理，再执行到compile
mvn clean test 先清理，再执行到test，因为执行test前必须执行compile，所以这里不必指定compile
mvn clean package 先清理，再执行到package
### 使用插件
Goal 执行一个phase又会触发一个或多个goal（执行Phase test 对应执行的Goal compiler:testCompile surefile:test）
自定义插件（内置插件）
maven-shade-plugin可以创建一个可执行的jar，要使用这个插件，需要在pom.xml中声明它
~~~
<project>
    ...
	<build>
		<plugins>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-shade-plugin</artifactId>
                <version>3.2.1</version>
				<executions>
					<execution>
						<phase>package</phase>
						<goals>
							<goal>shade</goal>
						</goals>
						<configuration>
                            ...
						</configuration>
					</execution>
				</executions>
			</plugin>
		</plugins>
	</build>
</project>
~~~
自定义插件配置
~~~
<configuration>
    <transformers>
        <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
            <mainClass>com.itranswarp.learnjava.Main</mainClass>
        </transformer>
    </transformers>
</configuration>
~~~
### 模块
对于Maven工程来说，原来是一个大项目可以分拆成多个模块：

single-project
├── pom.xml
└── src

single-project
├── module-a
│   ├── pom.xml
│   └── src
├── module-b
│   ├── pom.xml
│   └── src
└── module-c
    ├── pom.xml
    └── src

pom.xml共同部分作为parent（parent的packaging是pom而不是jar）

single-project
├── parent
│   └── pom.xml
├── module-a
│   ├── pom.xml
│   └── src
├── module-b
│   ├── pom.xml
│   └── src
└── module-c
    ├── pom.xml
    └── src

mvnw是Maven Wrapper的缩写