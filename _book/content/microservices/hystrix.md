# Hystrix

Learn to leverage the one of the [Spring cloud Netflix]() stack component called `Hystrix` to implement **circuit breaker** while invoking underlying [microservice](). It is generally required to enable fault tolerance in the application where some underlying service is down/throwing error permanently, we need to fall back to different path of program execution automatically. This is related to distributed computing style of Eco system using lots of underlying Microservices. This is where circuit breaker pattern helps and `Hystrix` is an tool to build this circuit breaker.

```java
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-hystrix</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-hystrix-dashboard</artifactId>
</dependency>
```

```java
Add @EnableCircuitBreaker annotation
Add @EnableHystrixDashboard annotation
Add annotation @HystrixCommand(fallbackMethod = "myFallbackMethod")

```

