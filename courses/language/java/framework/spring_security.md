# Spring Security

## Secuity Terminilogy

- Eavesdopper: Gains access to data trsnmitted across network.
- Encryption: Encoding data to prevent unathorized access.
  - Symmetric Encryption: Same key is used by sender and reciever to encrypt/decrypt the data.
  - Asymmetric Encryption: Data is encryptes using a public key but can only be decrypted using a private key.
- Certificate: A digital document that contains public key and the name of issuing autority and others.
- Certificate Authority: A trusted org that issues and maintains certificates.
- Secure Socket Layer (SSL): A protocl for encrypting data for transmitting over the internet.
- Transport Layer Security (TLS): More secure version of SSL.
- Hypertext Transfer Protocl (HTTP): An open protocol for tranmitting data between a web client and server.
- HTTPS: A secure version of HTTP using SSL.
- Authentication: Verifies who you are.
  - Basic Authentication: The username and password are transmitted in the Authorization header of the HTTP request using Base64 encoding.
  - OAuth2: An authorization framework that allows users to sign into a website using credentials from another site.
  - JSON Web Token (JWT) Authentication: This is a specially formatted and digitally signed token that contains “claims,” which are standard or custom key-value pairs containing relevant information about the caller.
- Authorization: Verifies if an authenticates user has access to the resources.

## Spring Security

Spring Security uses filters (or more accurately “servlet filters”) to handle authentication and authorization. Filters are small programs that intercept and enrich incoming requests or outgoing responses in a predefined order. Each filter performs its processing and then passes the result to the next filter in a chain of filters, until the request finally reaches the desired endpoint implementation.

Spring Security by default uses session-based authentication. In that scheme, a session ID is preserved in a cookie and is sent with each request, allowing the server to retrieve the session and associated SecurityContext. In this way, the login remains valid until it times out or until the session ends, so there is no need to log in again for each request.

Applications can also choose to use token-based authentication. In that case a JWT token containing the user information is generated and passed in the request header for each request. Again, this allows the login to remain valid for the life of the token or until the session is terminated.

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

  @Bean
  public SecurityFilterChain securityFilterChain(HttpSecurity http) 
     throws Exception {
    http
       .csrf(csrf -> csrf
          .ignoringRequestMatchers(new AntPathRequestMatcher("/mtg/payment",
             HttpMethod.POST.name())) //ignore Cross-Site Request Forgery checking for this example
       )
       .authorizeHttpRequests((authorize) -> authorize //define the restrictions for each endpoint
          .requestMatchers(new AntPathRequestMatcher("/mtg/payment",
             HttpMethod.POST.name())).hasRole("USER")
          .requestMatchers(new AntPathRequestMatcher("/mtg/payment",
             HttpMethod.GET.name())).hasRole("USER")
          .requestMatchers(new AntPathRequestMatcher("/actuator/**",
             HttpMethod.GET.name())).hasRole("USER")
          .anyRequest().authenticated()
       )
       // use basic authentication
       .httpBasic(Customizer.withDefaults());
    return http.build();
  }

  @Bean
  public UserDetailsService userDetailsService() {
    PasswordEncoder encoder =
       PasswordEncoderFactories.createDelegatingPasswordEncoder();
    UserDetails user = User.builder()
       .username("user")
       .password(encoder.encode("password"))
       .roles("USER")
       .build();
    UserDetails admin = User.builder()
       .username("admin")
       .password(encoder.encode("admin"))
       .roles("ADMIN")
       .build();
    return new InMemoryUserDetailsManager(user);
  }
}

//usage
/* curl -X POST -H "Content-Type: application/json" -H "Authorization: Basic dXNlcjpwYXNzd29yZA==" -d @request.json http://localhost:8081/mtg/payment */
```