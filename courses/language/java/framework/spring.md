# Spring

Spring provides annotations where you configure beans, components, services, and repositories—all fancy names for “Spring managed instances.” Two design patterns are fundamental to spring.

Inversion of Control: It is a design pattern that the creation and assignment of new objects are managed by frameworks so that program can use the object with ease.

Dependency injection: It is a specific form of IOC where the depdendencies are defined in the configuration, injected by the framework and managed via annotations.

Beans are simply Java class instances that are managed by the Spring framework.

The Spring Boot framework greatly simplifies the development and deployment of Spring-based applications

Spring exposes an ApplicationContext class instance, which contains references to all your beans, as well as other important Spring information, such as the active profile

## Spring Bean Scopes

- Singleton: default. Returns the same instance for every access.
- Prototype: returns a new instance for every access.
- Request: returns the same instance during the processing of a single request, even with multiple threads.
- Session: returns the same instance during the same client HTTP session, even across multiple requests.

## Bean Configuration classes

The name of the bean is just the method name, and the bean type is the return type of the method. You annotate those methods with @Bean

```java
@Scope(scopeName = "prototype") //define number of instances
@Configuration //used to define beans
public class AppConfig {
  @Bean //creates instance
  MortgageCalculatorService mortgageCalculatorService() {
    return new MortgageCalculatorServiceImpl();
  }
  @Bean
  App app(MortgageCalculatorService mortgageCalculatorService) { //inject dependency instance as parameter
    return new App(mortgageCalculatorService);
  }
  //alternatively depdency can be injected via annnotation, then no need to inject as a parameter above
  @Autowired 
  private final MortgageCalculatorService calculatorService
}
```

## Component scanning

It is a process where Spring inspects the file system for Spring annotated classes and automatically loads them as managed beans.

Common annotations to let spring manage the class.

- @Configuration: Configuration class for defining Spring beans
- @Component: Marks this class as a general Spring bean.
- @Service: Indicates that this class performs some service.
- @Repository: Indicates that this is a data access class.
- @Controller: This is an MVC controller, for handling web requests.
- @RestController: This is a RESTful web services controller, for handling HTTP requests.

```java
@ComponentScan(basePackages = "com.wiley.realworldjava")
public class AppConfig {
    ApplicationContext context = new AnnotationConfigApplicationContext("com.wiley.realworldjava"); //create context to access the bean
}
```

## Injecting properties

```java
@Configuration
@PropertySource("classpath:application.properties")
@PropertySource("classpath:application-${spring.profiles.active}.properties") //load all environment specific properties (application-prod.properties), if same property, this overrides the default one
public class AppConfig {
    @Value("${default.interestRate}") //injected using annotation
    private double defaultInterestRate;
}
```

## Common Spring porjects

- Spring framewrok: The core of Spring including dependency injection, web applications, messaging, and more.
- Spring Batch: Used for batch processign applications.
- Spring Boot: Gets application running quickly.
- Spring Cloud: Supports cloud and microservices.
- Spring Data: Used for working with databases.
- Spring Integration: Supports popular enterprise integration patterns.
- Spring Security: Adds authenticationa and authorization support.
- Spring WebFlux: Provides reactive capabalities to web and REST endpoints.

