

## Dependency Injection vs. Inversion of Control



## Complete Application Context Initialization Flow

Core flow defined in `AbstractApplicationContext#refresh`.

1. collects Bean definitions
   - explicitly registered through the ApplicationContext (e.g. `StandardEnvironment`)
   - declared through `BeanDefinitionRegistryPostProcessor`s (e.g. `ConfigurationClassPostProcessor`).
1. (if in a web app) loads the Servlet Context and Servlet Config's "init params"
   as `PropertySource`s.
1. checks that all properties marked as "required" are present.
1. prepares the `BeanFactory`
   - wires in all of the (many) collaborators that the `BeanFactory` uses
     to load classes, resolve string references of beans to actual beans,
     property editors, resource loader, app event publisher, and the
     application context itself.
1. `BeanFactoryPostProcessor`s are invoked over registered beans
   - Three groups: `PriorityOrdered`, `Ordered`, and unordered.


## Bare-Naked Application Context

- Minimum Viable AppCtx (`StaticApplicationContext`) has Six (6) Beans:
  - `environment` (a `StandardEnvironment`) with it's two sources:
    - `systemEnvironment`
    - `systemProperties`
  - `messageSource`
  - `applicationEventMulticaster`
  - `lifecycleProcessor`
  
- An Application Contexts (and friends) scan for special types of beans and
  registers them:
  - `ApplicationListener`s (by `AbstractApplicationContext`)
  - `Lifecycle`s (by `DefaultLifecycleProcessor`)
  - `BeanFactoryPostProcessor`s (by `PostProcessorRegistrationDelegate`)
  - `BeanPostProcessor`s (by `PostProcessorRegistrationDelegate`)
  - `LoadTimeWeaverAware` (by `AbstractApplicationContext`)
  
## Annotation Configured Application Context

Includes these additional beans (invoked in this order):
- `ConfigurationClassPostProcessor` — a `BeanDefinitionRegistryPostProcessor` 
   that registers beans from `@Configuration`-annotated classes.
- `AutowiredAnnotationBeanPostProcessor`
  - a `BeanPostProcessor` that injects `@Autowired` methods and fields with
   the corresponding Spring Bean.
- `o.s.c.annotation.internalRequiredAnnotationProcessor`
- `CommonAnnotationBeanPostProcessor`
  - a `BeanPostProcessor` that recognizes a number of JEE annotations:
    
- `o.s.c.event.internalEventListenerFactory`
- `o.s.c.event.internalEventListenerProcessor`


## Events

Don't confuse ApplicationContext Lifecycle Events with ApplicationEvents:
the former describe events on the container itself, especially during
start-up; the later describe...

### Application Context Lifecycle Events

1. ApplicationStartedEvent
2. ApplicationEnvironmentPreparedEvent
3. ApplicationPreparedEvent
4. ContextRefreshedEvent
5. EmbeddedServletContainerInitializedEvent
6. ApplicationReadyEvent

## Logging Use-Cases

### Registering Beans

- `org.springframework.beans`
- `org.springframework.context.annotation.ClassPathBeanDefinitionScanner`


## Lifecycles

Referring to the Spring feature wherein individual beans indicate they themselves
have a lifecycle that should be triggered.

Q: these were introduced circa Spring 3... are they useful to know?

## Configuration Sources in Spring Boot

Knowing the start-up flow of an Application Context (and how the test harnesses work) can greatly improve your ability to anticipate in what order property sources are searched:

1. ...
1. `BeanFactoryPostProcessor`s are executed, including that from the `ConfigFileApplicationListener`, which is run at near-highest precedence in the "Ordered" group of BFPPs.  This BFPP ensures that the `application.properties` and friends are _last_ in the property source search order.
  - For every Profile (in reverse order as named in `spring.profiles.active`, then `spring.profiles.include`, finally the so-called default profile), `application-{profile}.properties`, this component searches for that file at the following paths (in this order):
    1. `file:./config`
    1. `file:./`
    1. `classpath:./config`
    1. `classpath:./`
1. 

## Spring Factories

- Since Spring 3.2
- `SpringApplication`, on initialization, [loads](https://github.com/spring-projects/spring-boot/blob/v1.5.2.RELEASE/spring-boot/src/main/java/org/springframework/boot/SpringApplication.java#L255) via the Spring Factories feature (see also [spring.factories](https://github.com/spring-projects/spring-boot/blob/master/spring-boot/src/main/resources/META-INF/spring.factories)).
  - `ApplicationContextInitializer`s
  - `ApplicationListener`s
  

## Aspect-Oriented Programming

### With IntelliJ support

- Gutter icon treatment only works for `@Component`-registered beans.
- IntelliJ  `@EnableAspectJAutoProxy(proxyTargetClass = true)`.



## Uncategorized Bits of Knowledge

- `org.springframework.core.env.AbstractEnvironment#isProfileActive` implements the `@Profile` feature.
  - while `spring.profiles.active` is implemented here, `spring.profiles.include`
    is actually a Spring Boot feature ()
- When you are specifying a `basePackage` for bean scanning, that value
  can contain placeholder properties:
  ```java
    System.setProperty("rootPackage", "hello");
    AnnotationConfigApplicationContext appCtx = new AnnotationConfigApplicationContext();
    appCtx.scan("${rootPackage}.simple");
  ```
- When Spring loads property files, it actually delegates to the [`java.util.Properties`](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html) class to do so.
  - _(fun but likely-useless)_ this means that properties can be loaded in XML format (because `Properties` implements that).  Also fun is that the Spring's property loading utility specifically continues to support loading files with the `.xml` suffix.
  
 

