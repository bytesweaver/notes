### 扩展

BeanPostProcessor, bean后置处理器， bean创建对象初始化前后进行拦截工作的

BeanFactoryPostProcessor, BeanFactory的后置处理器， 在BeanFactory标准初始化， 所有的Bean定义已经保存加载到beanFactory, Bean还未初始化

invokeBeanFactoryPostProcessor

BeanDefinetionRegistryPostProcessor extends BeanFactoryPostProcessor 优先于 BeanFactoryPostProcessor执行



**事件 ApplicationEvent**

ApplicationContext.publishEvent;

1.  获取事件的多播器

2. multicastEvent派发事件
3. 遍历回调onApplicatioinEvent()（同步和异步支持）

事件多播器

1. initApplicationEventMulticaster() ；初始化

容器中有哪些监听器

​	1. registerListeners()，从容其中获取所有监听器就，病注册到多播器中

使用@EventListener注解

EventListenerLMethodProcessor