# Microservices-Docs
## Eureka Server
Eureka Server Provides service for registration and discovery it can register other client (Microservices) and client applications (Microservices) can discover other client through this server.

**Step 1:** Goto Window Menu -> Change Perspective ‘Spring’<br/>
**Step 2:** Goto File Menu -> New -> Spring Starter Project -> Type Project Name -> Next -> Select EurekaDiscovery (Service discovery using spring-cloud-netflix and Eureka)  and Ureka Server (spring-cloud-netflix Eureka Server) -> Click on Finish<br/>
**Step 3:** Annotate @EnableEurekaServer at Spring runner class to enable this microservice as Eureka server to discover and register other client (Microservices).<br/>
**Step 4:** Goto application properties/yml file and specify following:<br/>

> #Default port is 8761 for Eureka Server<br/>
> **server.port=8761**<br/>
> #To specify hostname<br/>
> **eureka.instance.hostname=localhost**<br/>
> #these two properties disable this server to resister himself as client set this property false because it will act as server. It will look for other client to register<br/>
> **eureka.client.register-with-eureka=false**<br/>
> **eureka.client.fetch-registry=false**<br/>

## Eureka Client
Eureka Client feature must be enabled each and every microdervices (Real module). This feature enables each module to automatically get register himself on Eureka Registory Server.

**Step 1:** Goto Window Menu -> Change Perspective ‘Spring’</br>
**Step 2:** Goto File Menu -> New -> Spring Starter Project -> Type Project Name -> Next -> Select EurekaDiscovery (Service discovery using spring-cloud-netflix and Eureka)  and Ureka Server (spring-cloud-netflix Eureka Server) -> Click on Finish</br>
**Step 3:** Annotate @EnableEurekaClient/@EnableDiscoveryClient (It will provide metadata information and every time it will send heartbeat to Eureka Server.) at Spring runner class to enable this microservice as Eureka Client to register itself with Eureka Server so that other client (Microservices) can discover it.</br>
**Step 4:** Goto application properties/yml file and specify following:</br>

> **server.port=8080**<br/>
> #Service name for lockup for other client<br/>
> **spring.application.name=student-service**<br/>
> #Eureka Server fallback URL where this client will register itself. Note: if you are running multiple Eureka Server Instance then you can give multiple Instance URL of Eureka Server.<br/>
> **eureka.client.service-url.defaultZone=http://localhost:8761/eureka**<br/>
> #Eureka Client instance ID. Note: Default Instance Id will be as ‘SERVICE-NAME/PHISICAL-MACHIME-NAME:PORT’<br/>
> **eureka.instance.instance-id=${spring.application.name}:${random.port}**<br/>
