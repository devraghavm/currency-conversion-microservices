# Spring Cloud Microservices Complete Example
A complete spring cloud example using Centralized Configuration, Naming Server, API Gateway, Service Registry, Service Discovery, Ribbon Client Side Load Balancing, Distributed Tracing Using Zipkin and RabbitMQ.

Run the below command to clone all the code to your local:
```
git clone --recurse-submodules -j8 https://github.com/devraghavm/currency-conversion-microservices.git
```

## Prerequisites
- Java 1.8+
- Java based IDE (IntelliJ IDEA or Eclipse)
- RabbitMQ
    #### Windows
    - https://www.rabbitmq.com/install-windows.html
    - https://www.rabbitmq.com/which-erlang.html
    - http://www.erlang.org/downloads
    - Video - https://www.youtube.com/watch?v=gKzKUmtOwR4
    
    (Note: For window, the RabbitMQ should be running as daemon process if you followed the above steps in links properly)

    #### Mac
    - https://www.rabbitmq.com/install-homebrew.html
    
    After installing rabbitmq using homebrew, issue the below command.
    ```
    /usr/local/sbin/rabbitmq-server
    ```
   
    
- Zipkin
    
    Quick Start Page
    - https://zipkin.io/pages/quickstart

    Downloading Zipkin Jar
    - https://search.maven.org/remote_content?g=io.zipkin.java&a=zipkin-server&v=LATEST&c=exec

    Command to run
    #### Windows
    ```
    SET RABBIT_URI=amqp://localhost 
    java -jar <zipkin-jar-name>.jar
    ```
    #### Mac
    ```
    RABBIT_URI=amqp://localhost java -jar <zipkin-jar-name>.jar 
    ```
## Setup Process:
Open the project in any of your favorite IDE. (I prefer IntelliJ IDEA).

- Once the project is opened, navigate to each subfolder and right click on each pom.xml file and import as maven projects. (In IntelliJ IDEA, we import them right clicking on each pom.xml and selecting Add Maven Project)
- Each subproject inside the folder is a Spring Boot project except for *git-localconfig-repo*. (*git-localconfig-repo* is a central repository where we store all our centralized configuration.)
- Do the following in whichever IDE you are using to setup local repository for centralized configuration management.
  - In Eclipse:
    - Right click on *spring-cloud-config-server*, Build -> Build Path -> Add *git-localconfig-repo* to the sources folder.
  - In IntelliJ IDEA:
    - Use shortcut, ```⌘; (For Mac)``` or ```Ctrl+Alt+Shift+S (For Windows)``` to open **Project Structure**. In the window, Add Content Root using the following:
    ```
    Project Settings -> Modules -> spring-cloud-config-server -> + Add Content Root -> Navigate to git-localconfig-repo folder and add it.
    ```
- Once all projects are built and the centralized configuration is initialized, Start the projects in the below order either by issuing ```mvn spring-boot:run``` or directly running the spring boot main application:
```
1. spring-cloud-config-server
2. netflix-eureka-naming-server
3. limits-service
4. currency-exchange-service
5. currency-conversion-service
6. netflix-zuul-api-gateway-server
```

## Testing Functionality

Make sure all appplications are started in the order specified and all applications are up and running. 
(Note: All services are deployed with profile selected as 'qa'. All the configuration is loaded up with that profile.)
1. Check if all centralized configuraion is applied by navigating to url.
    - http://localhost:8888/**{service-name}**/**{environment}** (Example: http://localhost:8888/limits-service/dev)
2. Check if all services are registered with the Eureka Naming Server.
    - http://localhost:8761/
3. Check if *limits-service* is working as expected.
    - http://localhost:8080/limits
    - http://localhost:8080/fault-tolerance-example (Hystrix Fault Tolerance Example)
4. Check if *currency-exchange-service* is working as expected.
    - http://localhost:7000/currency-exchange/from/EUR/to/INR
5. Check if *currency-conversion-service* is working as expected.
    - http://localhost:7100/currency-converter-feign/from/EUR/to/INR/quantity/10000
6. Finally, check if requests through *zuul-api-proxy/gateway* are working as expected.
    - http://localhost:8765/currency-exchange-service/currency-exchange/from/EUR/to/INR
    - http://localhost:8765/currency-conversion-service/currency-converter-feign/from/EUR/to/INR/quantity/10000
7. If you made it this far and were successfully able to test everything specified so far and get the appropriate responses, You can test distributed tracing by searching for each service in zipkin UI using the below URL.
    - http://localhost:9411/zipkin (Note: Make sure RabbitMQ and Zipkin are started in the background)
    
This is a complete production like setup for all spring cloud applications.

Hope this helps.

Happy Learning!

## References
    - https://github.com/in28minutes/spring-microservices
