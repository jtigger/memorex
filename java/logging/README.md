

## Enabling JDK Logging

Point to a config file (filesystem path, not a classpath):
```
-Djava.util.logging.config.file="simple-hello-app/build/resources/main/logging.properties"
```

```properties
handlers=java.util.logging.ConsoleHandler
java.util.logging.ConsoleHandler.level=FINEST

org.springframework.level=FINEST
```