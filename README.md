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
