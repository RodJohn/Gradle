


#概述

	Spring Boot Gradle插件在Gradle中提供Spring Boot支持，
	允许您打包可执行的jar或war,并使用提供的依赖关系管理



#配置插件


```
buildscript {
    ext {
        springBootVersion = '1.5.2.RELEASE'
    }
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}")
    }
}

apply plugin: 'java'
apply plugin: 'org.springframework.boot'

```


#依赖管理


spring-boot插件会自动应用 依赖管理插件并将其配置为导入spring-boot-starter-parentbom。
这为Maven用户提供了一个类似的依赖管理经验。
例如，它允许您在声明bom中管理的依赖项时省略版本号

```
dependencies {
    compile("org.springframework.boot:spring-boot-starter-web")
    compile("org.thymeleaf:thymeleaf-spring4")
    compile("nz.net.ultraq.thymeleaf:thymeleaf-layout-dialect")
}
```


#打包

通过命令 gradle build 可以打包为可执行的 jar和war文件

一旦spring-boot插件已经被应用到你的项目中，它将自动尝试重写归档，使它们可以使用 bootRepackage任务执行。您应该配置您的项目以通常的方式建立一个罐子或战争（如适用）。

要启动的主类可以使用配置选项指定，也可以通过向Main-Class清单添加属性来指定。如果不指定主类，插件将使用public static void main(String[] args)方法搜索类 。


#例子

	配置
	

```
buildscript {
    ext {
        springBootVersion = '1.5.2.RELEASE'
    }
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}")
    }
}

apply plugin: 'java'
apply plugin: 'org.springframework.boot'

jar {
    baseName = 'SpringBootDemo'
    version = '0.0.1-SNAPSHOT'
}

sourceCompatibility = 1.8
targetCompatibility = 1.8

repositories {
    mavenCentral()
}

dependencies {
    compile("org.springframework.boot:spring-boot-starter-web")
}

```

	代码
```
@Controller
@SpringBootApplication
public class SimpleController {

    @RequestMapping("/")
    @ResponseBody
    String home() {
        return "Hello World!";
    }

    public static void main(String[] args) throws Exception {
        SpringApplication.run(SimpleController.class, args);
    }

}
```

打包

	gradle build
	将在build目录中生成 SpringBootDemo-0.0.1-SNAPSHOT.jar

运行

	java -jar SpringBootDemo-0.0.1-SNAPSHOT.jar
	以内置tomcat启动


#wrapper 高级功能

使用Gradle Wrapper 不生成jar包运行;

运行

```
gradlew bootRun

```

项目启动了,但是build/lib中没有相应的jar包
当然也可以生成jar包,使用java -jar 命令启动


#参考

简单例子
https://www.jianshu.com/p/605d74794a08

好用
https://docs.spring.io/spring-boot/docs/current/reference/html/build-tool-plugins-gradle-plugin.html