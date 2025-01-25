# Spring Boot

It is a framework that elminates scaffolding and setup required by Spring applications. It brings bill-of-material(BOM) dependecies required to start an applciation.

Spring initializer: https://start.spring.io/

application.properties

```java
server.port = 8081
management.endpoints.web.exposure.include=info,metrics
```

## Rest application

```java
@RestController
@RequestMapping("/mtg") //context path for organizing
public class MortgageController {
    //@PutMapping //replace a resourse
    //@PatchMappanig //updates field of a resource
    //@DeleteMapping //delete the resource
    @GetMapping("/payment") //query for resource, for querying a complex payload, such as an arbitrarily large list of data, enterprises will often use a POST request even for read-only queries.
    public ResponseEntity<String> calculateMonthlyPayment( // ResponseEntity is a class to embed response metadata
        @RequestParam("amount") double principal, //mapping amount to principal
        @RequestParam int years,
        @RequestParam double interest) { 
            double payment = mortgageCalculator.payment(principal, interest, years); 
            String rval = String.format("Principal:%,.2f<br>Interest: %.2f<br>" + "Years: %d<br>Monthly Payment:%.2f", principal, interest, years, payment); 
            HttpHeaders headers = new HttpHeaders();
            headers.add("Request time", "Call for payment at " + LocalDateTime.now()); 
            return new ResponseEntity<>(rval, headers, HttpStatus.OK); 
    }
}

@PostMapping("/payment") //create a resource/record
public ResponseEntity<Response> calculateMonthlyPayment(
    @RequestBody List<Mortgage> mortgages) { //spring converts JSON list to Java List
    logger.info("Called payment POST endpoint " + mortgages);
    for(Mortgage mortgage:mortgages) {
      double principal = mortgage.getPrincipal();
      double rate = mortgage.getInterest();
      int years = mortgage.getYears();
      double payment = mortgageCalculator.payment(principal, rate, years);
      mortgage.setPayment(payment);
    }
    HttpHeaders headers = new HttpHeaders();
    headers.add("Request time", "Call for payment at " + LocalDateTime.now());
    return new ResponseEntity<>(new Response(mortgages, LocalDateTime.now()), headers, HttpStatus.OK); //wrapping response in an object
  }
}
```

## Handling Errors

The best way to handle exception is to create a custom exception class that extends RuntimeException and throw this exception in the code.

```java
public class MortgageException extends RuntimeException{

  public MortgageException(String message) {
    super(message);
  }

  public MortgageException(String message, Throwable cause) {
    super(message, cause);
  }
}

//and then use this to handle any exception in the application
@ControllerAdvice
public class GlobalExceptionHandler {
  @ExceptionHandler
  public ResponseEntity<ErrorResponse> handleException(MortgageException exception) {
    ErrorResponse errorResponse = ErrorResponse.builder(exception, HttpStatusCode.valueOf(400), exception.getMessage()).build();
    return new ResponseEntity<>(errorResponse, HttpStatus.BAD_REQUEST);
  }
}
```

## Inspecting application

Actuator can be used to get the status and health of the application.

Common endpoints:

- /actuator: This displays a list of all actuator endpoints.
- /actuator/health: This useful endpoint provides health information about the application, in the form of a JSON response with the single property{"status":"ok"}. You can call this endpoint directly, but its main value is that it is used by monitoring tools to check on the health of your application.
- /actuator/info: This displays standard and bespoke (custom) application information.
- /actuator/metrics: This displays a list of names of metrics for the current application.
- /actuator/metrics/<metric name>: This displays the current value of the named metric. For example, http://localhost:8081/actuator/metrics/disk.free returns the usable disk space.
- /actuator/loggers: This displays the configuration of all loggers in the application.
- /actuator/env: This exposes properties from the Spring environment.
- /actuator/beans: This displays a list of every Spring bean in your application.
- http://localhost:8081/actuator/metrics/jvm.info returns all you want to know about the current JVM