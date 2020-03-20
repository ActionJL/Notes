##### 简介

Spring Boot是一个简化Spring开发的框架。用来监护Spring应用的开发

约定大于配置，去繁就简，它做了那些没有它你也会做的Spring Bean配置

##### 优点

- 快速创建独立运行的Spring项目以及与主流框架集成
- 使用嵌入式Servlet容器，应用无需打成WAR包
- starters自动依赖于版本控制
- 大量的自动配置，简化开发，也可修改默认值
- 无需配置xml，无代码生成，开箱即用
- 准生产环境的运行时应用监控
- 与云计算的天然集成

##### 启动

pom配置

```xml
    <!-- 父组件 -->
		<parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.0.4.RELEASE</version>
    </parent>
		<!-- web应用启动器 -->
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>
```



