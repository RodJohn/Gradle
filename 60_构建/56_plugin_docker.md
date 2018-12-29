
# 作用

    执行docker build
    将项目的构建结果,在docker服务器中安装


# 启用

    指定gradle-docker插件的版本
    
    buildscript {
        ... ...
        dependencies {
            classpath('se.transmode.gradle:gradle-docker:1.2')
        }
    }    
    
    启用插件

    apply plugin: 'docker'


 docker daemon -H tcp://0.0.0.0:2375 -H C:/docker.sock


# 新建任务


```
task buildDocker(type: Docker, dependsOn: build, group: "custom") {
    push = true
    applicationName = jar.baseName
    dockerfile = file('src/main/docker/Dockerfile')
    doFirst {
        copy {
            from jar
            into stageDir
        }
    }
}
```


## 参数解释

group

    任务分组
    
type

    类型

dependsOn  

    指定依赖的前置task；
    在开始docker build之前，需要依赖gradle build的执行结果，

push 

    是否向注册服务器推送

applicationName

    镜像名称
    因为docker的repository名字不能用大写，所以jar.baseName只能使用中划线的方式。

dockerfile 

    指定dockerfile
    
doFirst

    自定义的doFirst，将gradle build生成的jar包也复制到build/docker下。  
    
## 过程解析    

    gradle build之后  
    将生成的jar包复制到build\docker目录下  
    将src/main/docker中的文件复制到build/docker下
    发送数据到 后台进行构建
    在build/docker下构建docker镜像；生成的镜像是$group/$jar.baseName:$version。
    并启动容器



# 整体结合


注意dockerfile和jar包的名称 一致 使用常量

用为镜像名$group/$jar.baseName:$version。  

发布的就是镜像  而且 能够展示当前的信息

这个时候的jar 是一个 带有依赖的包

Successfully tagged com.john.www/bo:1.0


已经生产镜像 只是无法启动容器

SECURITY WARNING: You are building a Docker image from Windows against a non-Windows Docker host.
 All files and directories added to build context will have '-rwxr-xr-x' permissions. 
 It is recommended to double check and reset permissions for sensitive files and directories.


# 参考

https://www.jianshu.com/p/5b5c034e1da9


https://www.cnblogs.com/hei12138/p/ideausedocker.html