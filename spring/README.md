

## Dependency Injection vs. Inversion of Control

## Bare-Naked Application Context

- Minimum Viable AppCtx (`StaticApplicationContext`) has Six (6) Beans:
  - `systemEnvironment`
  - `systemProperties`
  - `environment`
  - `messageSource`
  - `applicationEventMulticaster`
  - `lifecycleProcessor`
  
- An Application Context is supposed to detect special beans to include in 
  the Lifecycle:
  - `ApplicationListeners`
  - `BeanFactoryPostProcessor`
  - `BeanPostProcessor`
  
## Annotation Configured Application Context

Includes these additional beans:
- `o.s.c.annotation.internalRequiredAnnotationProcessor`
  - run at priority "Lowest"-1
- `o.s.c.annotation.internalAutowiredAnnotationProcessor`
  - a `BeanPostProcessor` that injects `@Autowired` methods and fields with
    the corresponding Spring Bean.
  - run at priority "Lowest"-2
- `o.s.c.annotation.internalCommonAnnotationProcessor`
- `o.s.c.annotation.internalConfigurationAnnotationProcessor`
- `o.s.c.event.internalEventListenerFactory`
- `o.s.c.event.internalEventListenerProcessor`
