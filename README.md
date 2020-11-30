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

    #### Mac
    - https://www.rabbitmq.com/install-homebrew.html
- Zipkin
    #### Windows
    ```
    SET RABBIT_URI=amqp://localhost 
    java -jar zipkin-server-2.5.2-exec.jar
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
