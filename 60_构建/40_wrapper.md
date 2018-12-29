

#概述

	Gradle Wrapper是开始一个Gradle构建的首选方式,他可以
	1.免安装gradle
	2.统一gradle版本




#安装


##开启

```
	build.gradle
	
	task wrapper(type: Wrapper) {
	    gradleVersion = '3.0'
	}
```

##初始化

```
执行命令
gradle wrapper
```


	命令会去下载相关的文件.
	执行完后，我们可以看到增加了一些新文件。


```
└── initial
    └── gradlew
    └── gradlew.bat
    └── gradle
        └── wrapper
            └── gradle-wrapper.jar
            └── gradle-wrapper.properties
```


现在Gradle Wrapper已经可以用来构建系统了。
把这些文件增加到版本控制系统中，然后再任何时候、任何地方只要迁出这些文件就一个按照同样的方式构建系统。


#使用


##一般命令

	比如 gradle assemble  == gradlew assemble
	比如 gradle build  == gradlew build  


#原理
	
	 wrapper 只是 gradle的一层包装
	
	核心还是调用gradle-wrapper.jar


# 特别说明

    每次都要去下载新包
    还不如使用本地gradle


#参考

https://www.jianshu.com/p/605d74794a08
https://docs.gradle.org/current/userguide/gradle_wrapper.html
wrapper 原理
http://blog.csdn.net/xiaoyur347/article/details/54313246