# Java-Microservices
<img width="1596" height="929" alt="image" src="https://github.com/user-attachments/assets/91692370-62d4-470f-8d0e-e8af07ceafe4" />

<img width="1005" height="566" alt="image" src="https://github.com/user-attachments/assets/25eb104f-535a-42d4-94a5-8a68dcf35b0c" />



<img width="1482" height="561" alt="image" src="https://github.com/user-attachments/assets/b7dea797-5753-4f86-b39c-0a7fae73d0ff" />


Microservices are little bit more expensive becasue we are creating different instances and diffrent instances of database as well 

benfits :
1. dont get singe point of failure 
2.you can scal all of this seperately 


<img width="1532" height="776" alt="image" src="https://github.com/user-attachments/assets/a86634f0-ac66-4ca7-8404-92e9ab29b21c" />

<img width="1771" height="595" alt="image" src="https://github.com/user-attachments/assets/05cc27c0-c902-4402-b490-1e61cf7778f0" />
<img width="1675" height="777" alt="image" src="https://github.com/user-attachments/assets/3824122e-e804-4d23-bb06-c48777399d7c" />

# Project Micro services Arch 
<img width="1366" height="858" alt="image" src="https://github.com/user-attachments/assets/1a38d6a8-6f7b-4a21-8ab6-f79b53f1d6e0" />

# Service Registration with Eureka 

All of our microservices in a microservices environment are registered at a centralized location , Why ?

suppose , we have microservices A, B, C and when they want to communicate with each other then they have to have the address of other micro services 
(the Address or location of IP Address ) 
<img width="1783" height="497" alt="image" src="https://github.com/user-attachments/assets/25a13052-ff84-4b1f-b4be-2ec459a86a58" />

<img width="1763" height="545" alt="image" src="https://github.com/user-attachments/assets/509fa8f3-637b-4883-a4c9-bf603bd86b31" />
<img width="1732" height="668" alt="image" src="https://github.com/user-attachments/assets/d5feadbe-6c68-47ee-b347-fa3e5089193b" />

# SetUp Eureka Server 
1. Create a Spring boot Project with Dependencies : Eureka Server ( Project Name: discovery-service)
2. enable the Eureka Server on this Project Name: discovery-service ( go to main method of this Project , and enable eureka server using this annotation @EnableEurekaServer)
3. we need to tell this project that dont have to register yourself as eureka client ( go to application.properties ,
              eureka.client.register-with-eureka=false
              eureka.client.fetch-register=false

# SetUp Eureka client Microservices A 
1. go to POM.XML of Micro service A Project and add the Eureka Discovery client dependencies and this Eureka client needs to
   Spring cloud starter dependency and alos Spring cloud depenency management needs the spring cloud version so we need to specify the spring cloud version inside the property
2. eureka server configuration -->  then go to Application.properties
            eureka.client.service-url.defaultZone=http://localhost:8761/eureka  ( this is location of eureka server, this is defualt server url  )
   # configure the eureka client
   <img width="1532" height="463" alt="image" src="https://github.com/user-attachments/assets/7e868f3c-392c-448d-80fd-dd6c05c24f3f" />


4. Then Start the Discovery-service Application  and check it discovery service: localhost:8761
   Then Start the Microservice A then automatically registering themselves to the eureka server
   and if they both want to communicate to each other since they don't know about the address of both of these services what thye can do is they can come to the eureka server and get the discovery for another service and from there they can make REST API Call
   <img width="1809" height="591" alt="image" src="https://github.com/user-attachments/assets/c006bef6-35cf-4611-8c93-a0189746d9fc" />

<img width="989" height="318" alt="image" src="https://github.com/user-attachments/assets/bf70258d-010e-4984-90e5-be5182bb13a4" />




## Spring Cloud API Gateway 
<img width="1203" height="681" alt="image" src="https://github.com/user-attachments/assets/7a37136f-31f0-4f79-8416-67e17418743b" />

<img width="1775" height="594" alt="image" src="https://github.com/user-attachments/assets/d97de4b7-876c-4b19-9376-324db9638ef7" />
<img width="1452" height="177" alt="image" src="https://github.com/user-attachments/assets/e04729da-8002-440c-8a9d-646055e88280" />

<img width="1597" height="369" alt="image" src="https://github.com/user-attachments/assets/74d981ba-2035-4033-bdc4-2fb1e7722686" />
<img width="831" height="450" alt="image" src="https://github.com/user-attachments/assets/09dfc07d-faaf-4b92-bc2d-589c958f8b1e" />

1. Create Spring boot Project for API Gateway with eureka discovery client dependency
2. Add the one more dependency : Gateway (Spring cloud routng) and POM.xml , Please keep this artifactID: spring-cloud-starter-gateway
3. Spring Cloud Gateway Building Blocks
          Spring CLoud gateway consists of 3 main building block
   
                 1) Route

                     Think of this as destination that we want a particuler request to route . it comprises of destination                         URL  
   
                 2) Predicate   : Condition match , if condition , if requests has something  -e.g path=blah
                      Predicates with path : - Path=/api/v1/orders/**
                      Predicate with Methods : - Method=GET , POST
                      Predicate With Header :  - Header=User-Agent
   
                 3) Filters
                     by using filter we can add certain behaviour modify the request or the response
                     for examples we can add a request header to our request
                        filters :
                                      - AddRequestheader=X-Request-Id,1234
                                      - RedirectTo=302, https://youtube.com
                                      - RemoveRequestHeader=Cookie
                                      - AddResponseHeader=X-Response-Id, abcd 
5. SetUp API Gateway  -Microservices A
    <img width="469" height="360" alt="image" src="https://github.com/user-attachments/assets/b9c977c8-0ba4-4923-8d9e-30af97acd732" />

   # Note : our API gateway alos uses the eureka server to find where where every service lies

6. Add the eureka clinet to API Gateway prejct to register it to eureka server
                 eureka.client.service-url.defaultZone= http://localhost:8761/eureka 
   



# Open Feign MicroServices Communication 

  ## What is OpenFeign?

OpenFeign is a tool that helps one microservice call another microservice without writing a lot of HTTP request code.
Spring Cloud OpenFeign is a declarative REST client that allows one microservice to call another by simply defining a Java interface, eliminating the need to write manual HTTP request code
 With OpenFeign

 you simply create an interface.
 ```java 
@FeignClient(name = "product-service")
public interface ProductClient {

    @GetMapping("/products/{id}")
    Product getProduct(@PathVariable Long id);

}
```
Now whenever you write:
```java
Product product = productClient.getProduct(101L);
```
Why is it called Declarative?
Because you only declare what API you want.

## Main Advantages :
✅ Less boilerplate code
✅ Easy to read
✅ Easy to maintain
✅ Automatically converts Java method calls into REST API calls
✅ Integrates well with Spring Boot and Spring Cloud


Step1 :  go to Microservices A (inventory-service)and Add the following dependency to your `pom.xml` file.
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```
## Create the Feign Client Interface
Create a new interface named `OrdersFeignClient` inside the `clients` package.
```java
@FeignClient(name = "order-service", path = "/orders")
public interface OrdersFeignClient {

    @GetMapping("/core/helloOrders")
    String helloOrders();
}
```
### Explanation

- `@FeignClient(name = "order-service")`
  - Specifies the name of the target microservice registered with Eureka.
   - `path = "/orders"`
  - Sets the base URL path for all API calls made through this client.

- `@GetMapping("/core/helloOrders")`
  - Maps the `helloOrders()` method to the `GET /orders/core/helloOrders` endpoint.

- `String helloOrders();`
  - Declares the method that calls the remote API. OpenFeign automatically generates the implementation at runtime.
### Request Flow

```
Inventory Service
       |
       | helloOrders()
       |
       ▼
GET /orders/core/helloOrders
       |
       ▼
Order Service
       |
       ▼
Returns String Response
feign client talk to eureka server and from eureka server discovery client it will find the urifor the microservice A so you dont have to define the URI here , just define the path here 


### Enable Feign Client on Microservice A((inventory-service)
``java
@SpringBootApplication
@EnableFeignClients
public class InventoryServiceApplication {

    public static void main(String[] args) {
        SpringApplication.run(InventoryServiceApplication.class, args);
    }
}
```
#### What happens internally?

When the application starts:

1. Spring scans for all interfaces annotated with `@FeignClient`.
2. It generates proxy implementations for those interfaces.
3. Registers them as Spring Beans.
4. These beans can then be injected using `@Autowired` or constructor injection.

### Startup Flow

```text
Application Starts
        │
        ▼
@EnableFeignClients
        │
        ▼
Scan for @FeignClient Interfaces
        │
        ▼
Create Proxy Implementations
        │
        ▼
Register as Spring Beans
        │
        ▼
Ready to Call Other Microservices
```
## Use the Feign Client in the Controller
Once the Feign client is created and enabled, inject it into your controller and use it to communicate with the `order-service`.
```java
@RestController
@RequiredArgsConstructor
public class ProductController {

    private final OrdersFeignClient ordersFeignClient;

    @GetMapping("/fetchOrders")
    public String fetchFromOrdersService(HttpServletRequest httpServletRequest) {

        log.info(httpServletRequest.getHeader("x-custom-header"));

        return ordersFeignClient.helloOrders();
    }
}
```
## Why Use Feign Instead of RestTemplate?
### Without Feign

```java
ServiceInstance orderService =
        discoveryClient.getInstances("order-service").getFirst();

return restClient.get()
        .uri(orderService.getUri() + "/orders/core/helloOrders")
        .retrieve()
        .body(String.class);
```

You need to:
- Discover the service.
- Build the URL.
- Send the HTTP request.
- Retrieve the response.
- Convert the response.

### With Feign

```java
return ordersFeignClient.helloOrders();
```

OpenFeign handles all of the above automatically, resulting in cleaner, more maintainable code.

---

## Summary

- Inject the Feign client into your controller.
- Call the remote service using a simple Java method.
- No manual HTTP request code is required.
- OpenFeign manages service discovery, request execution, and response conversion behind the scenes.


  # MicroServices Resilience4J
  Resilience4J is a lightweight and standalone library for implementing resilience patterns in java application 
it provides mechanisms to handle failures gracefully and ensure that service remain responsive under failer condition 
that facilitates all these patterns  so that we don't have to write these patterns from scratch 
            - Retry  [ response is an expection right then we can retry again ]
            - Rate Limiter   [ particuler time frame only these many requests should be allowed ]
            - Circuit Breaker 
            - Integration with Spring boot 

Order-Service Microservices : Add the Resilience4J dependency 
``` xml
<dependency>
      <groupId>org.springframeworks.cloud</groupId>
	  <artifactId>spring-cloud-starter-circuitbreaker-resilience4j</artifactId>
</dependency>
```
application.yml
```yaml 
resilience4j:
  retry:
    instances:
	  inventoryRetry:
	    maxRetryAttempts: 3
		waitDuration: 10s
```
```java
@Retry(name = "inventoryRetry", fallbackMethod = "createOrderFallback")
public OrderRequestDto createOrder(OrderRequestDto orderRequestDto) {

    log.info("Calling the createOrder method");

    Double totalPrice = inventoryOpenFeignClient.reduceStocks(orderRequestDto);

    Orders orders = modelMapper.map(orderRequestDto, Orders.class);

    for (OrderItem orderItem : orders.getItems()) {
        orderItem.setOrder(orders);
    }

    orders.setTotalPrice(totalPrice);
    orders.setOrderStatus(OrderStatus.CONFIRMED);

    Orders savedOrder = orderRepository.save(orders);

    return modelMapper.map(savedOrder, OrderRequestDto.class);
}
public OrderRequestDto createOrderFallback(OrderRequestDto orderRequestDto,
                                           Throwable throwable) {

    log.error("Fallback occurred due to : {}", throwable.getMessage());

    return new OrderRequestDto();
}
```
### Benefits

- Prevents application crashes.
- Provides graceful degradation when dependent services are unavailable.
- Improves system reliability.
- Logs errors for easier debugging and monitoring.
- Works seamlessly with Resilience4j's `@Retry` annotation.

### Rate Limiter   [ particuler time frame only these many requests should be allowed ]

Rate Limiting controls how many requests are allowed within a specific period of time 

### Why Do we need  Rate Limiting ?
        - traffic spike 
		- DDos like requesr floods 
		- Expensive APIs 
 
Rate limiting can protect incoming traffic or outgoing calls 
``` java 
@RateLimiter(name= "inventoryRateLimiter",fallbackMethod = "fallBackMethodReduceOrder")
```
application.yml
```yaml 
resilience4j:
  ratelimiter:
    configs:
	  default:
	    limitForPeriod: 3        # Max 10 calls in a refresh period 
		limitRefreshPeriod: 5s  # Refresh the limit every second 
		timeoutDuration : 1s  # Time to wait for permission before a request fails  
```


### Circuit Breaker  [ opposite of Retry logic ]

if something is failing , do not let other call it again 
how the circuit breaker work 

if the circuit is closed then our applicaiton is working  
if the circuit is open then our application is not working 
so by default our circuit is closed 

# Circuit Breaker & Rate Limiter using Resilience4j

The Order Service uses **Resilience4j Circuit Breaker** and **Rate Limiter** to improve fault tolerance and protect downstream services (Inventory Service).

---

## Implementation

```java
@CircuitBreaker(
    name = "inventoryCircuitBreaker",
    fallbackMethod = "createOrderFallback"
)
@RateLimiter(
    name = "inventoryRateLimiter",
    fallbackMethod = "createOrderFallback"
)
public OrderRequestDto createOrder(OrderRequestDto orderRequestDto) {

    log.info("Calling the createOrder method");

    Double totalPrice = inventoryOpenFeignClient.reduceStocks(orderRequestDto);

    Orders orders = modelMapper.map(orderRequestDto, Orders.class);

    for (OrderItem orderItem : orders.getItems()) {
        orderItem.setOrder(orders);
    }

    orders.setTotalPrice(totalPrice);
    orders.setOrderStatus(OrderStatus.CONFIRMED);

    Orders savedOrder = orderRepository.save(orders);

    return modelMapper.map(savedOrder, OrderRequestDto.class);
}
```

---

# Fallback Method

If the Inventory Service is unavailable or the rate limit is exceeded, the fallback method is automatically executed.

```java
public OrderRequestDto createOrderFallback(
        OrderRequestDto orderRequestDto,
        Throwable throwable) {

    log.error("Fallback occurred due to : {}", throwable.getMessage());

    return new OrderRequestDto();
}
```

---

# Circuit Breaker Configuration


## application.yml

```yaml
resilience4j:
  circuitbreaker:
    instances:
      inventoryCircuitBreaker:
        registerHealthIndicator: true
        slidingWindowSize: 10
        slidingWindowType: COUNT_BASED
        minimumNumberOfCalls: 10
        failureRateThreshold: 50
        waitDurationInOpenState: 20s
        permittedNumberOfCallsInHalfOpenState: 3
        eventConsumerBufferSize: 10
```

---

## Configuration Properties

| Property | Value | Description |
|----------|------:|-------------|
| `registerHealthIndicator` | `true` | Registers the Circuit Breaker as a Spring Boot Actuator health indicator. |
| `slidingWindowSize` | `10` | Evaluates the last 10 requests. |
| `slidingWindowType` | `COUNT_BASED` | Uses a fixed number of requests instead of a time window. |
| `minimumNumberOfCalls` | `10` | Requires at least 10 requests before calculating the failure rate. |
| `failureRateThreshold` | `50%` | Opens the circuit when 50% or more of the requests fail. |
| `waitDurationInOpenState` | `20s` | Keeps the circuit OPEN for 20 seconds before moving to HALF_OPEN. |
| `permittedNumberOfCallsInHalfOpenState` | `3` | Allows 3 test requests while in HALF_OPEN state. |
| `eventConsumerBufferSize` | `10` | Stores the last 10 Circuit Breaker events for monitoring. |

---
# Spring Boot Actuator Configuration

Spring Boot Actuator is enabled to monitor the health and state of the Circuit Breaker.

## application.yml

```yaml
management:
  health:
    circuitbreakers:
      enabled: true

  endpoints:
    web:
      exposure:
        include: "*"

  endpoint:
    health:
      show-details: always
```

---

## Actuator Configuration

| Property | Description |
|----------|-------------|
| `management.health.circuitbreakers.enabled=true` | Includes Circuit Breaker status in the Health endpoint. |
| `management.endpoints.web.exposure.include="*"` | Exposes all Actuator endpoints over HTTP. |
| `management.endpoint.health.show-details=always` | Always displays detailed health information. |

---


# Circuit Breaker States

### 🟢 CLOSED

- Normal operating state.
- All requests are sent to the Inventory Service.
- Successes and failures are monitored.

```
Client
   │
   ▼
Order Service
   │
   ▼
Inventory Service
```

---

### 🔴 OPEN

- Triggered when the failure rate exceeds the configured threshold.
- Requests are blocked immediately.
- The fallback method is executed without calling the Inventory Service.

```
Client
   │
   ▼
Order Service
   │
   ├───────────────X
   │
Fallback Method
```

---

### 🟡 HALF_OPEN

- Activated after the configured wait duration.
- A limited number of requests are allowed.
- If they succeed, the circuit closes.
- If they fail, the circuit returns to OPEN.

```
Client
   │
   ▼
Order Service
   │
   ▼
Few Test Requests
   │
   ▼
Inventory Service
```

---

# Rate Limiter

The Rate Limiter restricts the number of requests reaching the Inventory Service within a specified time period.

### Benefits

- Prevents API abuse.
- Protects downstream services.
- Avoids traffic spikes.
- Improves application stability.

---

# Request Flow

```text
                Client
                   │
                   ▼
            Order Service
                   │
       ┌───────────┴────────────┐
       │                        │
       ▼                        ▼
 Rate Limiter          Circuit Breaker
       │                        │
       └───────────┬────────────┘
                   ▼
         Inventory Service
                   │
         Success / Failure
                   │
         ┌─────────┴─────────┐
         │                   │
         ▼                   ▼
   Save Order         Fallback Method
```

---

# Advantages

- ✅ Prevents cascading failures.
- ✅ Improves system resilience.
- ✅ Handles downstream service outages gracefully.
- ✅ Protects services from excessive traffic.
- ✅ Provides automatic recovery after failures.
- ✅ Integrates seamlessly with Spring Boot and OpenFeign.
- ✅ Supports Spring Boot Actuator monitoring.

# Resilience4j TimeLimiter

      A TimeLimiter is stops waiting for a response once a configured timeout is reached and then fall back machinism will be called 
### Why do we need it ?
   - Blocked Threads 
   - Poor User Experience 
   - Resoruce Exhaustion 
   - Slow APIs 

### Time Limiter Flow 
<img width="533" height="161" alt="image" src="https://github.com/user-attachments/assets/9f450126-fadd-4e3c-81de-b7c786ed1488" />


### TimeOut vs Time Limiter 
    
	- Now Lets say Order service is talking to inventory services and let's say inventory service is taking a lot of time 
	Then eventually after some amount of time you may have seen the read timeout error or connection timeout error or socket timeout error 
	so those errors will come over here 
	<img width="826" height="310" alt="image" src="https://github.com/user-attachments/assets/9adb77e1-3059-49ca-821c-79890a1d8c98" />

	HTTP Client responsible for establishing this connection and Providing the response to Order Service 
	and this connection timeouts, read timeouts everything we can configure inside our spring boot applicaiton 
	Socket Timeout 
	Connection Timeout 
	
	all things going on inside your network layer 
	
	I want to stop this request the moment a time threshhold value reaches
   I want to handle this use case in application level  so that is when we move away from network layer and go to application layer and bring in our utility 
   which is time limiter inside order service 
	
# Centralized Configuration Server Using GitHub 
<img width="1400" height="849" alt="image" src="https://github.com/user-attachments/assets/8cec8eed-f244-4a87-99bd-e7d68de18cb5" />

### Why do you need config server ?
we will have to modify those property files on each micro services then we will have to restart the microservices 
wherever they are deployed and that's how it will work  but this is inefficient 

we have a spring cloud config server somewhere and this store all the configurations that are required by all microservices 
that we have so suppose all the property file are being managed by this particuler config server and
if you want to modify any of the behavior inside the any of the micro services we just go there and we just modify the behavior there 
and these microservices just simply refresh without even needing to restart the whole micro services right and that makes our microservies 
systems available all the time and we can make the changes on the fly as well 

Spring cloud config server which will be taking all the configuration form either a file store somewhere or may be a git repository 


### Create the SPring boot Project: config-server with dependencies : Config Server , Eureka Discovery Client , Config Cllient
    Config Cllient dependencies use for micro services to pull this configuration from the github configuration server 
      
	    Application.yml in config-server proejct 
           ``` xml 
               spring:
                  cloud:
                     config: 
                       server: 
                          git:
                            uri: uri of repository 
                            username:  github_username 
                            password: access token 
                            default-lable: master 

                server:
                    port: 8888
				
				-- config eureka server location 
				eureka:
				  client:
				    service-url:
					  defaultZone=http://localhost:8761/eureka
             ``` 					
			 
### Create a Private Repository : `ecommerce-config-server` in Github then create a application.yml file in the root repositry 

        - Our application will not pull the information from github so we will need to authorize our application to get the information 
		   from our github server so that i am going to create a password API Tokens inside github 
		    got to settings --> Developer Setting ---> Personal Access Token --> Fine_grainedt tokens -- generate new token 
            Repository Permisions --> Administration READ ONLY , Content  READ ONLY 
            Then take token and save it 
      
 
        - Create the application.property inside github proejct: `ecommerce-config-server`
		      for eaxmple you have inventory-service microservices 
			  create property file like inventory-service.properties inside `ecommerce-config-server`
			  Then copy all the details from application.yml from inventory-service and move into 
			  inventory-service.properties inside `ecommerce-config-server`
			  
 
        -  The inventory-service to pull this configuration from the github configuration server , it will have to know 
           like from where i have to pull this infomration right for that we have to make this inventory-service as configuration client 
		     Add the config clinet dependencies for all micor services 
			  ```xml 
			         <dependency>
					      <groupId> org.springframework.cloud</groupId>
						  <artifactId>spring-cloud-starter-config</artifactId>
              ```
			  
			        application.properties of inventory-service , by default config server name is configserver 
				``` xml 
				       spring.config.import=configserver:http://localhost:8888
				```
				
				I will keep the application.properties of `discovery-service` because inter dependency b/w `discovery-service`
				and `config-server ` 
		
		-  we are dealing default profile inside our microservices architecture but if we want to define the configuration 
		   for `Dev` environment or `Dev` Profile 
		       create a file in github  like order-service-dev.properties
			   
			   Now we have defualt profile and dev profile , micro services picks up based which profile you mention inside the applicatio 
			   first priority default profile over the dev profiles 
			   
			    for example default profile , we define a property [my.variable=narendra-default , my.variable1=ponugoti-default]
				            Dev profile  , we define same property [my.variable=narendra-dev]
							when you launch micro services with Dev profile ,it will puck the application followig properties 
							
							 my.variable=narendra-dev
                             my.variable1=ponugoti-default
		
		-   Sometimes in all our  microservices , we have some propery soruce that are similar in all the microservices
		    what we can do is we can define a global file which is the application.yml , all the global properties can put inside this global file 
			and then we dont have to repeat those property sources across all the microservices  configuration file 
			
			

 
 # Refresh Configuration without Restart 

 Issue : we have change something inside github , lets go to order-service-dev.properties  
 let change the my.variable=orders-github-dev to orders-github-dev222
 after doing this then check it config server , localhost:8888/order-service/dev 
 the value changed to orders-github-dev222 that would happen becuase every time you run this is going to pull all the latest 
 information from the GitHub uri that's why its happen 
 but we not getting latest value when we hit the endpoint : http://localhost:9020/orders/core/helloOrders 
 we still getting the old value orders-github-dev , If you want to see the latest value , we want to restart the micro services 
 
 so what we want to refresh our property soruce as soon as we can change something so for we have something called 
 @RefreshScope 
 <img width="1663" height="726" alt="image" src="https://github.com/user-attachments/assets/8e89e8ca-4d6e-4587-a685-f2cca5dff258" />

 it needs actuator support so basically whats going to happen is that as soon as you change something in your configuration 
 and your configuration server actually picks thats changes up automatically you are going to call an API that API would be provided by the actuator if you call that API for your microservices by that actuator then basically you are telling your 
 application context to restart all the beans to basically refresh all the benas that are defined as @RefreshScope 
 <img width="1675" height="817" alt="image" src="https://github.com/user-attachments/assets/c66cda0c-22d5-4ff6-bcd7-2109edea3306" />

### Complete Flow
    Developer

Changes Git Configuration
        │
        ▼
Git Repository
        │
        ▼
Config Server
        │
        ▼
Microservice
        │
        ▼
POST /actuator/refresh
        │
        ▼
Application Context
        │
        ▼
Find @RefreshScope Beans
        │
        ▼
Destroy Old Beans
        │
        ▼
Create New Beans
        │
        ▼
Latest Configuration Loaded

Interview Question

### Interviewer: What happens internally when /actuator/refresh is called?

Answer:

The Actuator refresh endpoint receives the request.
Spring Cloud contacts the Config Server and retrieves the latest configuration.
The Application Context identifies beans annotated with @RefreshScope.
Those beans are destroyed and recreated.
During recreation, the beans are injected with the latest configuration values.
Beans without @RefreshScope are not recreated and continue using their existing configuration.


One Important Clarification

The statement:

"your configuration server actually picks those changes up automatically"

is only partially correct.

A more accurate explanation is:

The Config Server can serve the latest configuration from Git when requested.
The microservice does not automatically refresh its beans just because Git changed.
A refresh must be triggered, either:
manually by calling POST /actuator/refresh, or
automatically using Spring Cloud Bus (or another event mechanism) to broadcast refresh events to all services. Without one of these mechanisms, the running application continues using its previously loaded configuration.


refresh endpoint 
POST http://localhost:9020/orders/actuator/refresh 
this will update the application context just the bean that are defined as refreshscpe 

