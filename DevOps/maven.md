** maven 是如何去构建一个项目的 **

** maven有哪些更好用的插件 **
---
deploy 上传jar包
```
mvn deploy:deploy-file -Dmaven.test.skip=true -Dfile=D:\MvnProject\service-mvn-1.0.0.jar -DgroupId=pri.roy.mvn.test -DartifactId=mvn-api -Dversion=1.0.0-SNAPSHOT -Dpackaging=jar -DrepositoryId=roy_privrepository_snapshots -Durl=http://10.4.71.144:9090/repository/roy_privrepository_snapshots/
-Dmaven.test.skip=true                              //跳过编译、测试
-Dfile=D:\MvnProject\service-mvn-1.0.0.jar          //jar包文件地址,绝对路径
-DgroupId=pri.roy.mvn.test                          //gruopId--pom坐标，自定义
-DartifactId=mvn-api                                //artifactId--pom坐标，自定义
-Dversion                                           //版本号
-Dpackaging                                         //打包方式
-DrepositoryId                                      //远程库服务器ID
-Durl                                               //远程库服务器地址
```

<<<<<<< HEAD:componets/maven.md
management    <https://www.cnblogs.com/maxiaofang/p/5944362.html>

<https://www.cnblogs.com/mr-wuxiansheng/p/6189438.html>
=======
**build-helper-maven-plugin** 

[参考](https://blog.csdn.net/wangjunjun2008/article/details/17553503)

> Java程序开发，一般使用Eclipse、MyEclipse等工具，其源码目录为src，这与Maven默认的src/main/java不同。因此，在没有额外配置的情况下

**maven-jar-plugin**

生成可以直接运行的jar包：[参考](https://blog.csdn.net/xiao__gui/article/details/47341385)

**maven-compiler-plugin**

设置jdk编译相关参数：[参考](https://blog.csdn.net/liupeifeng3514/article/details/80236077)

**distributionManagement**

设置私服路径：[参考](https://blog.csdn.net/newbie_907486852/article/details/80928915)

**maven-antrun-plugin**

用于删除添加文件

**maven-assembly-plugin**

支持定制化打包方式:[参考](https://www.jianshu.com/p/14bcb17b99e0)

**maven-dependency-plugin**

[reference](https://liugang594.iteye.com/blog/2093082)

处理依赖相关的插件，用得最多的几个操作：copy, copy-dependencies和它们对应的unpack, unpack-dependencies

>>>>>>> 8f645797d0f2fe2b2f76c8c21629cd954a36064a:DevOps/maven.md
