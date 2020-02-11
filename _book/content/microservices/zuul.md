# Zuul API Gateway

Zuul Server is an API Gateway application. It handles all the requests and performs the dynamic routing of microservice applications. It works as a front door for all the requests. It is also known as **Edge Server.**

Zuul is built to enable **dynamic routing, monitoring, resiliency,** and **security.** It can also route the requests to multiple **Amazon Auto Scaling Groups**.

For Example, **/api/products** are mapped to the **product** service and **/api/user** is mapped to the **user** service. The Zuul Server dynamically routes the requests to the respective backend application.



##### Zuul Components

Zuul has mainly four types of filters that enable us to intercept the traffic in different timeline of the request processing for any particular transaction. We can add any number of filters for a particular url pattern.

- **pre filters** – are invoked before the request is routed.
- **post filters** – are invoked after the request has been routed.
- **route filters** – are used to route the request.
- **error filters** – are invoked when an error occurs while handling the request.

##### Dependency



```java
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-actuator</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-netflix-zuul</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-devtools</artifactId>
		<scope>runtime</scope>
		<optional>true</optional>
	</dependency>
```
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.client.discovery.EnableDiscoveryClient;
import org.springframework.cloud.netflix.zuul.EnableZuulProxy;

@SpringBootApplication
@EnableZuulProxy
@EnableDiscoveryClient
public class ZuulServerApplication {

	public static void main(String[] args) {
		SpringApplication.run(ZuulServerApplication.class, args);
	}

}
```

```java
spring:
 application:
  name: zuul-server
    
server:
 port: 8765
   
eureka:
 client: 
  serviceUrl: 
   defaultZone: http://localhost:8761/eureka  
```

##### 

##### Implementing Logging Filter via Zuul

```java
import javax.servlet.http.HttpServletRequest;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Component;

import com.netflix.zuul.ZuulFilter;
import com.netflix.zuul.context.RequestContext;
import com.netflix.zuul.exception.ZuulException;

@Component
public class ZuulLoggingFilter extends ZuulFilter {

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Override
	public boolean shouldFilter() {
		return true;
	}

	@Override
	public Object run() throws ZuulException {
		HttpServletRequest request = RequestContext.getCurrentContext().getRequest();
		logger.info("request -> {} request uri-> {}", request, request.getRequestURI());  
		return null;
	}

	@Override
	public String filterType() {
		return "pre";
	}

	@Override
	public int filterOrder() {
		return 1;
	}

}
```



For more detail check [Zuul API](https://cloud.spring.io/spring-cloud-netflix/multi/multi__router_and_filter_zuul.html)

