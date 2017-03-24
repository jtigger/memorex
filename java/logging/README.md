

## Enabling JDK Logging

The default logger in Java is the JDK Logger.

There is a default configuration.  To take control,

1. create a `logging.properties` file.
2. when starting up your Java application, set the system property
   `java.util.logging.config.file` to the path to that file, relative
   to the current working directory.

`logging.properties`
>   ```properties
>    handlers=java.util.logging.ConsoleHandler
>    java.util.logging.SimpleFormatter.format=%2$s %5$s%6$s%n
>    java.util.logging.ConsoleHandler.level=FINEST
>
>    org.springframework.level=FINER
>    ```

In IntelliJ, in the Run Configuration include this line the the **VM Options**
field, include something like:
```
-Djava.util.logging.config.file=path-relative-to-project-root/logging.properties
```

