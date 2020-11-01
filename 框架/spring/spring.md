

contextConfigLocation：
contextConfigLocation指的是Spring该去哪里读取配置文件，ContextLoaderListener用于启动的web容器（如tomcat）时，去读取配置文件并完成Spring容器的初始化（包括加载bean等）。
关于contextConfigLocation的配置方式也是可以非常丰富的，还可以使用通配符 * ，这里简单举几个例子说明：

1. classpath:resources/services.xml
表示到web工程的classes/resources文件夹中查找配置文件。
2. classpath*:resources/services.xml
这种方式除了会到classes/resources文件夹查找，还会到lib下面的jar包中查找，查找路径是jar包内/resources/services.xml。
3. classpath:resouces/**/*services.xml
这种方式表示到classpath的resources文件夹下所有文件夹（不限层级，可以在第N层子文件夹中）中查找文件名以services.xml结尾的文件。
4. 多个路径配置可以用空格分开


所以查看Spring框架的源码时，有两条清晰可见的脉络：

1）接口层描述了容器的重要组件及组件间的协作关系；

2）继承体系逐步实现组件的各项功能。


container
 A web container is responsible for managing the lifecycle of servlets, mapping a URL to a particular servlet and ensuring that the URL requester has the correct access-rights.

 The Web container creates servlet instances, loads and unloads servlets, creates and manages request and response objects, and performs other servlet-management tasks.

1. ApplicationContext represents Spring Ioc container
The interface org.springframework.context.ApplicationContext represents the Spring IoC container and is responsible for instantiating, configuring, and assembling the aforementioned beans
2. BeanDifinition
Within the container itself, these bean definitions are represented as BeanDefinition objects, which contain (among other information) the following metadata:
A package-qualified class name: typically the actual implementation class of the bean being defined.#类全名
Bean behavioral configuration elements, which state how the bean should behave in the container (scope, lifecycle callbacks, and so forth).#配置信息
References to other beans that are needed for the bean to do its work; these references are also called collaborators or dependencies.#依赖Bean的引用
Other configuration settings to set in the newly created object, for example, the number of connections to use in a bean that manages a connection pool, or the size limit of the pool.
