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
                 2) Predicate   : Condition match , if condition , if requests has something  -e.g path=blah
                      Predicates with path : - Path=/api/v1/orders/**
                      Predicate with Methods : - Method=Get
                      Predicate With Header :  - Header=User-Agent
   
                 3) Filters
5. SetUp API Gateway 

