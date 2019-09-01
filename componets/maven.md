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

management    <https://www.cnblogs.com/maxiaofang/p/5944362.html>

<https://www.cnblogs.com/mr-wuxiansheng/p/6189438.html>