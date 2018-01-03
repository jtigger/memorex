# Understanding Spring Security

Spring Security is a general-purpose framework that applies in many different contexts.  Much of the complexity experienced arises intrinsically from the significant scope the framework addresses.  Here are some of the dimensions:

-

These are addressed in the following structures:

- the framework is configured through a DSL that wires in Configurers into a Builder


# The Configuration Flow

1. Spring Application starts.
1. During bean-registration time, a registered `@Configuration` includes a `@EnableWebSecurity`.
1.






# Gotchas

- if you fail to include the CSRF token in a form, you will get the cryptic message:

    ```
    org.apache.jasper.JasperException: /index.jsp (line: 3, column: 5) Invalid standard action
        org.apache.jasper.compiler.DefaultErrorHandler.jspError(DefaultErrorHandler.java:41)
    ```

    - this is not a problem with Thymeleaf because that token gets inserted automatically.  It is not when using JSPs.
