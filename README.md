# Microservices-Docs
## Eureka Server
Eureka Server Provides service for registration and discovery it can register other client (Microservices) and client applications (Microservices) can discover other client through this server.

- Step 1: Goto Window Menu -> Change Perspective ‘Spring’
- Step 2: Goto File Menu -> New -> Spring Starter Project -> Type Project Name -> Next -> Select EurekaDiscovery (Service discovery using spring-cloud-netflix and Eureka)  and Ureka Server (spring-cloud-netflix Eureka Server) -> Click on Finish
- Step 3: Annotate @EnableEurekaServer at Spring runner class to enable this microservice as Eureka server to discover and register other client (Microservices).
- Step 4: Goto application properties/yml file and specify following:
