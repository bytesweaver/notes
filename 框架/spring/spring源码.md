## @Value

1.基本数值

2. #{} SPEL语法
3. ${}读取配置文件中的值



使用@propertySource 读取外部配置文件

ApplicationContext-> getEnvironment->getProperties

## 自动装配

1. 默认优先级按照类型去容器找对应的组件：applicationContext.getBean(BookDao.class);

2. 如果找到多个相同类型的组件，再将属性的名称作为组件的id去容器中查找

3. @Qualifier(""):指定要装配的Id

4. @Primary:指定首选装配

5. @Resource:java规范，可以实现自动装配，默认按照组件名称进行组件装配

6. 自定义组件想要使用Spring容器底层的一些组件， ApplicationContext, BeanFactory, xxx, 自定义组件实现xxxAware，在创建对象的时候，把Spring底层的一些组件注入到自定义的bean中， xxxAware:公式使用xxxProcessor;ApplicationContextAware ==> ApplicatioinContextProcessor

7. Profile:

   Spring 为我们提供的可以根据当前环境， 动态的激活和切换一系列组件的功能，