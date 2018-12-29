


# 概述

作用 

	Java plugin插件提供了一系列的任务支持构建、编译、测试Java项目。
	
启用	

    apply plugin: 'java'


# 任务对比

默认任务

	在执行 gradle tasks --all 查看新证的任务
	可以看到一些非常基础的任务
    
    ```
    
    :tasks
     
    == All tasks runnable from root project
     
    == Build Setup tasks
    setupBuild - Initializes a new Gradle build. [incubating]
    wrapper - Generates Gradle wrapper files. [incubating]
     
    == Help tasks
    dependencies - Displays all dependencies declared in root project 'gs-gradle'.
    dependencyInsight - Displays the insight into a specific dependency in root project 'gs-gradle'.
    help - Displays a help message
    projects - Displays the sub-projects of root project 'gs-gradle'.
    properties - Displays the properties of root project 'gs-gradle'.
    tasks - Displays the tasks runnable from root project 'gs-gradle'.
     
    To see all tasks and more detail, run with --all.
     
    BUILD SUCCESSFUL
     
    Total time: 3.077 secs
    ```

新增任务


	在执行 gradle tasks --all 查看新证的任务

    ------------------------------------------------------------
    All tasks runnable from root project
    ------------------------------------------------------------
    
    Build tasks
    -----------
    assemble - Assembles the outputs of this project.
    build - Assembles and tests this project.
    buildDependents - Assembles and tests this project and all projects that depend on it.
    buildNeeded - Assembles and tests this project and all projects it depends on.
    classes - Assembles main classes.
    clean - Deletes the build directory.
    jar - Assembles a jar archive containing the main classes.
    testClasses - Assembles test classes.
    
    Build Setup tasks
    -----------------
    init - Initializes a new Gradle build.
    wrapper - Generates Gradle wrapper files.
    
    Documentation tasks
    -------------------
    javadoc - Generates Javadoc API documentation for the main source code.
    
    Help tasks
    ----------
    buildEnvironment - Displays all buildscript dependencies declared in root project '1'.
    components - Displays the components produced by root project '1'. [incubating]
    dependencies - Displays all dependencies declared in root project '1'.
    dependencyInsight - Displays the insight into a specific dependency in root project '1'.
    dependentComponents - Displays the dependent components of components in root project '1'. [incubating]
    help - Displays a help message.
    model - Displays the configuration model of root project '1'. [incubating]
    projects - Displays the sub-projects of root project '1'.
    properties - Displays the properties of root project '1'.
    tasks - Displays the tasks runnable from root project '1'.
    
    Verification tasks
    ------------------
    check - Runs all checks.
    test - Runs the unit tests.
    
    Other tasks
    -----------
    compileJava - Compiles main Java source.
    compileTestJava - Compiles test Java source.
    processResources - Processes main resources.
    processTestResources - Processes test resources.
    
    Rules
    -----
    Pattern: clean<TaskName>: Cleans the output files of a task.
    Pattern: build<ConfigurationName>: Assembles the artifacts of a configuration.
    Pattern: upload<ConfigurationName>: Assembles and uploads the artifacts belonging to a configuration.





# 常用任务

## 基础任务

compileJava

    编译源码
    目的文件夹一般为build\classes\java\main

processResources

    打包资源文件
    目的文件夹一般为build\resources\main
    
compileTestJava

    编译源码
    目的文件夹一般为build\classes\java\test

processTestResources

    打包资源文件
    目的文件夹一般为build\resources\test


## classes  

作用

    classes = compileJava + processResources

过程

```
:compileJava
:processResources NO-SOURCE
:classes
```

## jar *

作用

    jar = classes + 生成jar
    (目的文件夹一般为build\libs,
    jar的名称一般为 group - version )


过程

```
:compileJava UP-TO-DATE
:processResources NO-SOURCE
:classes UP-TO-DATE
:jar
```


## assemble  

作用

    将源码和依赖一起打包


过程
	

```
qianhuis-Mac-mini:1228_1 qianhui$ gradle assemble  
:compileJava UP-TO-DATE  
:processResources UP-TO-DATE  
:classes UP-TO-DATE  
:jar  
:assemble  
```

## testClasses

作用

    testClasses = classes + compileTestJava + processTestResources

过程
	

```
:compileJava UP-TO-DATE
:processResources UP-TO-DATE
:classes UP-TO-DATE
:compileTestJava
:processTestResources NO-SOURCE
:testClasses  
```

## test * 

作用

    test = testClasses + 运行单元测试 + 生成测试报告

过程
	

```
:compileJava
:processResources
:classes
:compileTestJava
:processTestResources
:testClasses
:test
```

## check 

作用

    暂时不知道和test的区别

过程
	

```
:compileJava
:processResources
:classes
:compileTestJava
:processTestResources
:testClasses
:test
:check
```

## build  *

作用

    build = assemble + check 


过程

```
qianhuis-Mac-mini:1228_1 qianhui$ gradle build  
:compileJava UP-TO-DATE  
:processResources UP-TO-DATE  
:classes UP-TO-DATE  
:jar  
:assemble  
:compileTestJava UP-TO-DATE  
:processTestResources UP-TO-DATE  
:testClasses UP-TO-DATE  
:test UP-TO-DATE  
:check UP-TO-DATE  
:build  
```


## clean

作用

	清除上次的所有构建    
	删除 build目录


## 发布


```
uploadArchives {
    repositories {
        flatDir {
            dirs 'repos'
        }
    }
}
```

# 设置

## 常用属性

sourceCompatibility
	
	指定源码jdk版本
	例如 sourceCompatibility = 1.8
    
targetCompatibility
	
	指定目标jdk版本
	例如 targetCompatibility = 1.8

Jar


```
JAR或ZIP的名称和Manifest
例如
jar {
    baseName = 'java-gradle'
    version =  '0.1.0'
    manifest {
        attributes 'Main-Class':'com.john.bo.Tjava1'
    }
}
JAR文件的名字为：java-gradle-0.1.0.jar。
指定main文件
```





## 项目布局

默认布局

```
项目文件的布局和maven是一样的

src/main/java			产品的Java源代码
src/main/resources		产品的资源
src/test/java			Java 测试源代码
src/test/resources		测试资源
src/sourceSet/java		给定的源集的Java源代码
src/sourceSet/resources	给定的源集的资源
```

更改布局


```
你可以通过配置适当的源集，来配置项目的布局(一般不改变)。

build.gradle

sourceSets {
    main {
        java {
            srcDir 'src/java'
        }
        resources {
            srcDir 'src/resources'
        }
    }
}
```



	
	
# 例子	



build.gradle
	

```
group 'com.john.bo'
version '1.0-SNAPSHOT'

apply plugin: 'java'

sourceCompatibility = 1.8
targetCompatibility = 1.8

jar {
    baseName = 'java-gradle'
    version =  '0.1.0'
    manifest {
        attributes 'Main-Class':'com.john.bo.Tjava1'
    }
}

repositories {
    mavenCentral()
}

dependencies {
    testCompile group: 'junit', name: 'junit', version: '4.12'
    compile "joda-time:joda-time:2.2"
}

```










#参考

常用任务
http://www.importnew.com/15881.html

http://blog.csdn.net/maosidiaoxian/article/details/45361971

http://blog.csdn.net/itfootball/article/details/42672271



