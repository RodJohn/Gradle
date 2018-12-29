
#war

WAR插件扩展了Java插件,支持web应用组装成War文件.它默认禁用了Java插件JAR归档任务，并增加了一个默认的WAR归档任务。

#启用
apply plugin 'war'



为了能够将依赖包也以一起打包，比如，我们希望构建一个WAR包，可以包含第三方的打包格式，我们可以使用Gradle的WAR插件。如果我们使用Spring Boot并且希望得到一个可执行的JAR文件，我们可以使用spring-boot-gradle-plugin插件。在我们的示例中，gradle没有足够的信息来了解我们的目标系统。




#参考

war插件
http://blog.csdn.net/roymuste/article/details/51322206
