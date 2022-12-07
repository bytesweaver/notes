1. spring-boot容器启动配置参数读取
2. spring-boot应用配置参数读取

## 起步依赖：

通过bom技术，引入所需依赖，对常用的依赖进行封装，使开发者无需关注包冲突。

1. 无需考虑不通框架不同版本的冲突问题
2. 简化了POM的配置

## 自动配置：

通过 @EnableAutoConfiguration 或者`@SpringBootApplication`注解 开启组件扫描和自动配置 

通过@SpringBootApplication(exclude = XAutoConfiguration.class)关闭自动配置，自动配置位于

org.springframework.boot.autoconfigure包路径。

有一个名为`getAutoConfigurationEntry`的方法，这个方法发挥的作用是扫描`ClassPath`下的所有`jar`包的`spring.factories`文件，将`spring.factories`文件`key`为`EnableAutoConfiguration`的所有值取出，然后这些值其实是类的全限定名，**也就是自动配置类的全限定名**，然后 Spring Boot 通过这些全限定名进行类加载(反射)，将这些自动配置类添加到 Spring 容器中

```java
/**
 * 加载AutoConfigurationImportSelector
 */
@AutoConfigurationPackage
@Import(AutoConfigurationImportSelector.class)
public @interface EnableAutoConfiguration {
...    
```

```java
/**
 *加载AutoConfigurationImportSelector
 *实现DeferredImportSelector，BeanClassLoaderAware，ResourceLoaderAware，BeanFactoryAware，Ordered
 */
public class AutoConfigurationImportSelector implements DeferredImportSelector, BeanClassLoaderAware,
		ResourceLoaderAware, BeanFactoryAware, EnvironmentAware, Ordered {
            ...
                
     /**
      * 实现DeferredImportSelector的selectImports方法
      */
 	@Override
	public String[] selectImports(AnnotationMetadata annotationMetadata) {
		if (!isEnabled(annotationMetadata)) {
			return NO_IMPORTS;
		}
		AutoConfigurationEntry autoConfigurationEntry = getAutoConfigurationEntry(annotationMetadata);
		return StringUtils.toStringArray(autoConfigurationEntry.getConfigurations());
	}
            
       /**
        *返回基于@Configuration的需要被自动加载的类
        *Return the AutoConfigurationImportSelector.AutoConfigurationEntry based on the    
        *AnnotationMetadata of the importing @Configuration class.
        *Params:
        *annotationMetadata – the annotation metadata of the configuration class
        *Returns:
        *the auto-configurations that should be imported
        */
      protected AutoConfigurationEntry getAutoConfigurationEntry(AnnotationMetadata annotationMetadata) {
		if (!isEnabled(annotationMetadata)) {
			return EMPTY_ENTRY;
		}
		AnnotationAttributes attributes = getAttributes(annotationMetadata);
		List<String> configurations = getCandidateConfigurations(annotationMetadata, attributes);
		configurations = removeDuplicates(configurations);
		Set<String> exclusions = getExclusions(annotationMetadata, attributes);
		checkExcludedClasses(configurations, exclusions);
		configurations.removeAll(exclusions);
		configurations = getConfigurationClassFilter().filter(configurations);
		fireAutoConfigurationImportEvents(configurations, exclusions);
		return new AutoConfigurationEntry(configurations, exclusions);
	}
      /**
       *返回META-INF/spring.factories里面配置的类
       *（org.springframework.boot.autoconfigure.EnableAutoConfiguration=后面的配置）
       *Return the auto-configuration class names that should be considered. By default this method          *will load candidates using SpringFactoriesLoader with getSpringFactoriesLoaderFactoryClass().
       *Params:
       *metadata – the source metadata
       *attributes – the annotation attributes
       *Returns:
       *a list of candidate configurations
       */
      protected List<String> getCandidateConfigurations(AnnotationMetadata metadata, AnnotationAttributes attributes) {
		List<String> configurations = SpringFactoriesLoader.loadFactoryNames(getSpringFactoriesLoaderFactoryClass(),
				getBeanClassLoader());
		Assert.notEmpty(configurations, "No auto configuration classes found in META-INF/spring.factories. If you "
				+ "are using a custom packaging, make sure that file is correct.");
		return configurations;
	}
       
     
```

1. DeferredImportSelector 继承ImportSelector

   > ImportSelector : ImportSelector implementations are usually processed in the same way as regular @Import annotations, however, it is also possible to defer(延迟) selection of imports until all @Configuration classes have been processed (see DeferredImportSelector for details).（所有的@Configuration已经被process）
   >
   > DeferredImportSelector :A variation of ImportSelector that runs after all @Configuration beans have been processed. This type of selector can be particularly useful when the selected imports are @Conditional.(配合@Conditional)

2. BeanClassLoaderAware

3. ResourceLoaderAware 可以被ResourceLoader通知，也可以通过实现ApplicationContextAware，获得ApplicationContext对象，ApplicationContext继承了ResourceLoader接口

   ```
   Interface to be implemented by any object that wishes to be notified of the ResourceLoader (typically the ApplicationContext) that it runs in. This is an alternative to a full ApplicationContext dependency via the ApplicationContextAware interface.
   ```

   

4. BeanFactoryAware

5. Ordered 指定顺序

   >Ordered is an interface that can be implemented by objects that should be orderable, for example in a Collection.
   >The actual order can be interpreted as prioritization, with the first object (with the lowest order value) having the highest priority.

```java
	/**
	  * SpringFactoriesLoader.loadSpringFactories
	  * 该类位于spring-core包，加载FACTORIES_RESOURCE_LOCATION也就是META-INF/spring.factories文件的配置
	  */
     private static Map<String, List<String>> loadSpringFactories(ClassLoader classLoader) {
		Map<String, List<String>> result = cache.get(classLoader);
		if (result != null) {
			return result;
		}

		result = new HashMap<>();
		try {
			Enumeration<URL> urls = classLoader.getResources(FACTORIES_RESOURCE_LOCATION);
			while (urls.hasMoreElements()) {
				URL url = urls.nextElement();
				UrlResource resource = new UrlResource(url);
				Properties properties = PropertiesLoaderUtils.loadProperties(resource);
				for (Map.Entry<?, ?> entry : properties.entrySet()) {
					String factoryTypeName = ((String) entry.getKey()).trim();
					String[] factoryImplementationNames =
							StringUtils.commaDelimitedListToStringArray((String) entry.getValue());
					for (String factoryImplementationName : factoryImplementationNames) {
						result.computeIfAbsent(factoryTypeName, key -> new ArrayList<>())
								.add(factoryImplementationName.trim());
					}
				}
			}

			// Replace all lists with unmodifiable lists containing unique elements
			result.replaceAll((factoryType, implementations) -> implementations.stream().distinct()
					.collect(Collectors.collectingAndThen(Collectors.toList(), Collections::unmodifiableList)));
			cache.put(classLoader, result);
		}
		catch (IOException ex) {
			throw new IllegalArgumentException("Unable to load factories from location [" +
					FACTORIES_RESOURCE_LOCATION + "]", ex);
		}
		return result;
	}
```

