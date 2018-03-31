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

## Config Server (File System)
If you are going with Microservices architecture so you will face configuration overhead for all instances of application.
So config server need to configure to provide all configuration at one place. Each microservice when wakeup then it will raed all configuration from this Config Server

**Step 1:** Goto Window Menu -> Change Perspective ‘Spring’<br/>
**Step 2:** Goto File Menu -> New -> Spring Starter Project -> Type Project Name -> Next -> Select Config Server -> Click on Finish<br/>
**Step 3:** Annotate @EnableConfigServer (It will add capability for Config Server.) at Spring runner class to enable this microservice as Config Server to provide central configuration details (like db connection details, SMTP details) for other Client (Microservices) for consumtion.<br/>
**Step 4:** Goto application.properties/yml file and specify following:<br/>

> #Port to run Config Server
> **server.port=8888*

**Step 6:** Now your Config server is ready to provide configuration details from file system, Click on run button and type following URL to get configuration details like this.<br/>
http://localhost:8888/myapp1/production

## Config Client

Config Client features enable microservices instanc to read configuration details like DB credential SMTP credential for **Config Server**

**Step 1:** Goto Window Menu -> Change Perspective ‘Spring’<br>
**Step 2:** Goto File Menu -> New -> Spring Starter Project -> Type Project Name -> Next -> Select Config Client [You can select MVC and other required dependencies for your module] -> Click on Finish<br/>
**Step 3:** Goto application.properties/yml file and specify following:
> #Port to run Config Server<br/>
> **server.port=8080**

**Step 4:** Goto resources folder and create bootstrap.properties file.<br/>
Note: bootstrap.property file get loaded before all resources so that those configuration which required get loaded before application.property must be placed inside it.<br/>
> #application name play very important role it is basically property file name in your Config Server<br/>
> **spring.application.name=myapp1-production**<br/>
> **spring.profiles.active=default**<br/>
> #Fallback URI of Config Server<br/>
> **spring.cloud.config.uri=http://localhost:8888**<br/>
**Step 5:** Create ReST endpoint to check whether your config client is able to get configuration details from Config Server or Not<br/>

    @RestController
    public class CommonController {
	
	   @Value("${portal.jdbc.url:default url}")
	   String url;
	   @Value("${portal.jdbc.user:default user}")
	   String userName;
	   @Value("${portal.jdbc.password:default password}")
	   String password;
	
	   @RequestMapping(value="/getProperty", method=RequestMethod.GET)
	   public String displayProperty() {
		   Map<String,String> m=new HashMap<String,String>();
		   m.put("url", url);
		   m.put("userName", userName);
		   m.put("password", password);
		   return m.toString();
	   }
    }

## Config Server Security

**Step 1:** Add following dependency in Config Server POM
   <dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-security</artifactId>
   </dependency>
