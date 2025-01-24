# Logging

Logging is useful to get information about the application activity. There can be two sets of logs: troubleshooting logs and audit logs. Logging framewroks can make your aplication faster by storing messages for asynchronous logging.

## java.util.logging

It is built into java.

```java
import java.util.logging.Logger;

public class BasicLogging {
    private static final Logger LOGGER = Logger.getLogger(BasicLogging.class.getName());
    public static void main(String... args){
        LOGGER.severe("something bad happened");
        LOGGER.severe(String.format("%s: %.1f is %d/%d", "Division", 1.5, 3, 2));
    }
}

/* Feb 11, 2024 9:16:22 PM 
com.wiley.realworldjava.logging.jul.BasicLogging main
SEVERE: Something bad happened! */

```

logging.properties

```java
.level=WARNING
handlers=java.util.logging.ConsoleHandler, java.util.logging.FileHandler
java.util.logging.FileHandler.pattern = java-log-%u.log //%u is unique id
java.util.logging.FileHandler.limit = 10000 // limit files by bytes 1 MB
java.util.logging.FileHandler.count = 2 // max number of log file
```

## LOG4J

It is a direct logging framework.

```java
import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;

public class Logging {
    private static final Logger LOGGER = LogManager.getLogger();

    public static void main(String... args){
        LOGGER.fatal("{}: {} is {}/{}", "Division", 2, 6, 3);
    }
}
```

log4j.properties

```java
appenders = rolling
rootLogger.level = error
rootLogger.appenderRefs = RollingFile
rootLogger.appenderRef.rolling.ref = RollingFile
appender.rolling.type = RollingFilea
ppender.rolling.name = RollingFil
eappender.rolling.fileName = java-log.log
appender.rolling.filePattern = java-log-%d{yyyy-MM-dd}-%i.log.gz
appender.rolling.layout.type = PatternLayout
appender.rolling.layout.pattern = %d %p %c{1.} [%t] %m%n //date, log level, class name and package level, method, message and line
appender.rolling.policies.type = Policies
appender.rolling.policies.time.type = TimeBasedTriggeringPolicy
appender.rolling.policies.size.type = SizeBasedTriggeringPolicy
appender.rolling.policies.size.size = 1MB
appender.rolling.strategy.type = DefaultRolloverStrategy
appender.rolling.strategy.max = 3
```

Use a lambda expression for lazy logging

```java
public static void main(String[] args) { 
    LOGGER.error(() -> generateMessage());
}
private static String generateMessage() { 
    return "This is an expensive message";
}
```

## SLF4J

Simple logging facade for java is intended to be used as a wrapper so that the underlying framework can switched easily.

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class Logging {
    private static final Logger LOGGER = LoggerFactory.getLogger(Logging.class);

    public static void main(String... args){
        LOGGER.fatal("{}: {} is {}/{}", "Division", 2, 6, 3);
        //lazy logging
        LOGGER.atDebug()
            .setMessage(() -> "Message with expensive params {}")
            .addArgument(() -> generateParamToFillMessage())
            .log();
    }
}

```

## Consideration

- Logging involves input/output (I/O), so it is slower than computations and other operations. You want to make sure that logging does not slow down your application!
- You may want to log more in your test or QA environment than your production environment.
- Rotating the log file too often can produce a lot of files, making it harder to use them
- Log injection refers to hostile parties messing up your logs by including text you didn't expect
- Sensitive date should not be logged for security reasons.
- Filebeat, Fluentd, LogBeat, and Splunk is used to move local logs to central location
