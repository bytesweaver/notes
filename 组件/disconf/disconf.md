# 强兼容性
当开启Disconf时，
如果Disconf正常运行，则正常使用分布式配置。
如果Disconf非正常运行，则使用本地配置。(Disconf可以保证在Disconf失败时，原有程序能够按原有逻辑正确运行)
当不开启Disconf时， 则使用本地配置

两者调用disconfmgr
first scan  -> DisconfMgrBean  在Spring内部的Bean定义初始化后执行，这样是最高优先级的
导入系统配置
导入用户配置（disconf.properties）
静态扫描，扫描包内配置
second scan  -> DisconfMgrBeanSecond 第二次扫描, 动态扫描, for annotation config
动态扫描
Problem
1. spring-boot容器启动参数和配置中心配置文件（除discof.properties）加载顺序
2. spring-boot启动过程
3. disconf什么时候扫描并加载配置文件
