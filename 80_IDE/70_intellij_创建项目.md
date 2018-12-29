


#选择gradle


默认是idea内置的gradle
可以选择外部gradle
或者gradle wrapper




#建立项目

	1.新建一个 Gradle 项目

![这里写图片描述](http://img.blog.csdn.net/20171227184616117?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcm9kX2pvaG4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

	2.填写 GAV
![这里写图片描述](http://img.blog.csdn.net/20171227184738296?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcm9kX2pvaG4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast) 

	3.确认 Gradle 使用的版本和 JDK 版本 

![这里写图片描述](http://img.blog.csdn.net/20171227184752412?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcm9kX2pvaG4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

	4.填写项目名称和项目的位置
	 
![这里写图片描述](http://img.blog.csdn.net/20171227184906339?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcm9kX2pvaG4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

	5.文件结构
	
![这里写图片描述](http://img.blog.csdn.net/20171227185034102?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcm9kX2pvaG4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


文件分析

	.gradle，gradle的相关支持文件，不用管
	.idea，IntelliJ IDEA的相关文件，不用管
	build，构建生成物，存放项目构建中生成的class和jar包
	gradle，一个gradle的包装程序，貌似直接用gradle不太好，得再包一层，这个其实我们也不用管
	src，我们写代码的地方，不用说了吧
	build.gradle，gradle的构建配置，这是我们要关心的，相当于Maven的pom.xml
	GradleLearn.iml，IntelliJ IDEA的项目文件
	gradlew，一段gradle wrapper的运行脚本，For *nix
	gradlew.bat，一段gradle wrapper的运行脚本，For Windows



#