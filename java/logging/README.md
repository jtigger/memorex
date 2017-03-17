

## Enabling JDK Logging

The default logger in Java is the JDK Logger.

To configure the logging system, the file `./src/main/reseources/logging.properties`

`logging.properties`
>   ```properties
>    handlers=java.util.logging.ConsoleHandler
>    java.util.logging.SimpleFormatter.format=%2$s %5$s%6$s%n
>    java.util.logging.ConsoleHandler.level=FINEST
>
>    org.springframework.level=FINEST
>    ```

In your Run Configuration, set the system property `java.util.logging.config.file`
```
-Djava.util.logging.config.file="build/resources/main/logging.properties"
```

