# SpringBoot初始化

打开IDEA，新建Maven模块，设置组名和工件名：
![2024-11-22_15-33](https://github.com/user-attachments/assets/27683b25-05eb-4706-8c8c-0ac32906454d)

在pom.xml中添加springboot相关依赖（下面的示例来自[Spring Boot Reference Guide](https://docs.spring.io/spring-boot/docs/2.1.6.RELEASE/reference/html/getting-started-installing-spring-boot.html#getting-started-maven-installation)）：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.example</groupId>
	<artifactId>myproject</artifactId>
	<version>0.0.1-SNAPSHOT</version>

	<!-- Inherit defaults from Spring Boot -->
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.1.6.RELEASE</version>
	</parent>

	<!-- Add typical dependencies for a web application -->
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
	</dependencies>

	<!-- Package as an executable jar -->
	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

</project>
```


# 最小应用
注解`@SpringBootApplication`是SpringBoot项目的入口：
_HelloApplication.java_
```java
@SpringBootApplication
public class HelloApplication {
    public static void main(String[] args) {
        SpringApplication.run(HelloApplication.class);
    }
}
```
使用`@RestController`和`@RequestMapping`进行路由：
_HelloController.java_
```java
@RestController
public class HelloController {
    @RequestMapping("/hello")
    public String hello() {
        return "Hello, SpringBoot!\n";
    }
}
```

# 读取YAML配置文件
三种方法：
1. `@Value`
2. `@Autowired` + `Environment`
3. `@Autowired` + `@ConfigurationProperties`

_my `application.yml` config example:_
```yaml
spring:
  profiles:
    active:
      dev # -> application-dev.yml
      # pro -> application-pro.yml
      # one-file-dev -> 下面---里面的配置
---
spring:
  profiles: one-file-dev
server:
  port: 8083
name1: 'chito'
student: { name: "xlx",gender: "male",age: 22 }
sentence1: 'test \n test'
sentence2: "test \n test" # 双引号才识别转义
array1:
  - 0
  - 1
  - 2
array2: [ 1,2,3,4,5 ]
---
```
_SpringBoot读取`application.yml`：_
_ReadFromYAMLController.java_
```java

@RestController
public class ReadFromYAMLController {
    @Value("${name1}")      // 这个名字和yml中的字段名一致
    private String name_1;  // 这个名字不需要一致

    @Autowired
    private Environment env; // 导入yml中的所有内容
    @Autowired
    private Student stu;

    @RequestMapping("/hello")
    public String hello() {
        String res = "\nname1: " + name_1;
        res += "\nsentence1: " + sentence1;
        res += "\nsentence2: " + sentence2;
        return "Hello, SpringBoot!\n" + res;
    }

    @RequestMapping("/env")
    public String env() {
        String sentence = env.getProperty("sentence1");
        return sentence;
    }

    @RequestMapping("stu")
    public String stu(){
        return stu.toString();
    }
}
```
_Student.java：_
```java
@Component  // 表明这是一个Java Bean
@ConfigurationProperties(prefix = "student")  // 将application.yml中的student及其成员注入进来
public class Student {
    private String name;
    private String gender;
    private int age;

    /*
     * 省略Getter、Setter、toString
     */
}

```
