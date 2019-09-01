1. spring-boot容器启动配置参数读取
2. spring-boot应用配置参数读取

起步依赖：

通过bom技术，引入所需依赖

自动配置：

通过 @EnableAutoConfiguration 或者`@SpringBootApplication`注解 开启组件扫描和自动配置 

通过@SpringBootApplication(exclude = XAutoConfiguration.class)关闭自动配置，自动配置位于

org.springframework.boot.autoconfigure包路径。