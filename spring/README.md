

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
  
- An Application Context is supposed to detect special beans to include in 
  the Lifecycle:
  - `ApplicationListeners`
  - `BeanFactoryPostProcessor`
  - `BeanPostProcessor`
  
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



## Application Context Lifecycle Events

1. ApplicationStartedEvent
2. ApplicationEnvironmentPreparedEvent
3. ApplicationPreparedEvent
4. ContextRefreshedEvent
5. EmbeddedServletContainerInitializedEvent
6. ApplicationReadyEvent
