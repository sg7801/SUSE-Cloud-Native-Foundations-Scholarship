# Lesson 2 : Architecture Consideration for Cloud Native Applications
- In this lesson, we will cover:
  - Monoliths and Microservices
  - Trade-offs for Monoliths and Microservices
  - Practices for Application Development

![image](https://user-images.githubusercontent.com/61888364/124396771-3bb44680-dd29-11eb-8172-b54615cf2b47.png)

- The two main approaches that are usually referenced are monoliths and microservices.
- We have explore each architectural model and the implied trade-offs. As well, we will cover good development practices to be considered if an application is targeted for containerization. These practices are valid for both monolith and microservice architectures.
- When building an application it is important to allocate time for context discovery. This includes listing all necessary functionalities of the application and enumerating any resources that can enable its buildout. This phase sets the fundamentals of the project. If properly implemented, it can enable the creation of services that are scalable, resilient, and extensible.
- The first step in the context discovery process is to list the functional requirements, or what application capabilities should deliver to the end-users:  
  - Stakeholders
  - Functionalities
  - End users
  - Input and output process
  - Engineering teams 
- The second step is to enumerate the available resources that facilitates the implementation of the project. For example, a good starting point is to list available:
  - Engineering resources
  - Financial resources
  - Timeframes
  - Internal knowledge

## Architecture: 
- The main goal is to design an application that delivers value to customers and can be easily adjusted to accommodate new functionalities.
- Also, each architecture encapsulates the 3 main tires of an application:
  - UI (User Interface) - handles HTTP requests from the users and returns a response
  - Business logic - contained the code that provides a service to the users
  - Data layer - implements access and storage of data objects
## Monoliths:
- In a monolithic architecture, application tiers can be described as:
  - part of the same unit
  - managed in a single repository
  - sharing existing resources (e.g. CPU and memory)
  - developed in one programming language
  - released using a single binary

![image](https://user-images.githubusercontent.com/61888364/124396918-1b38bc00-dd2a-11eb-82df-7e809b46cea2.png)
 
## Microservices:
- In a microservice architecture, application tiers are managed independently, as different units. Each unit has the following characteristics:
  - managed in a separate repository
  - own allocated resources (e.g. CPU and memory)
  - well-defined API (Application Programming Interface) for connection to other units
  - implemented using the programming language of choice
  - released using its own binary
![image](https://user-images.githubusercontent.com/61888364/124396992-a914a700-dd2a-11eb-913d-09dada7b2ec7.png)

Trade-Off | Monolith | Microservices
--- | --- | ---
Development Complexity | one programming language, one repository, enables sequential development| multiple programming languages, multiple repositories, enables concurrent development
Scalability | replication of the entire stack; hence it's heavy on resource consumption | replication of a single unit, providing on-demand consumption of resources 
Time to Deploy | one delivery pipeline that deploys the entire stack; more risk with each deployment leading to a lower velocity rate | multiple delivery pipelines that deploy separate units; less risk with each deployment leading to a higher feature development rate
Flexibility | low rate, since the entire application stack might need restructuring to incorporate new functionalities | high rate, since changing an independent unit is straightforward 
Operational Cost | low initial cost, since one code base and one pipeline should be managed. However, the cost increases exponentially when the application needs to operate at scale | high initial cost, since multiple repositories and pipelines require management. However, at scale, the cost remains proportional to the consumed resources at that point in time.
Reliability | in a failure scenario, the entire stack needs to be recovered. Also, the visibility into each functionality is low, since all the logs and metrics are aggregated together. | in a failure scenario, only the failed unit needs to be recovered. Also, there is high visibility into the logs and metrics for each unit. 

## Best Practices For Application Deployment:
### Health Checks
  - Health checks are implemented to showcase the status of an application. These checks report if an application is running and meets the expected behavior to serve incoming traffic. 
  - Usually, health checks are represented by an HTTP endpoint such as /healthz or /status. These endpoints return an HTTP response showcasing if the application is healthy or in an error state.
  - /status health check that showcases that the application is healthy

### Metrics
  - Metrics are necessary to quantify the performance of the application. To fully understand how a service handles requests, it is mandatory to collect statistics on how the service operates. 
  - For example, the number of active users, handled requests, or the number of logins. Additionally, it is paramount to gather statistics on resources that the application requires to be fully operational. For example, the amount of CPU, memory, and network throughput. 
  - Usually, the collection of metrics are returned via an HTTP endpoint such as /metrics, which contains the internal metrics such as the number of active users, consumed CPU, network throughput, etc.
  - /metrics endpoint that list of metrics counting the amount requests by the HTTP code returned

### Logs
  - Log aggregation provides valuable insights into what operations a service is performing at a point in time. It is the nucleus of any troubleshooting and debugging process. For example, it is essential to record if a user logged in successfully into a service, or encountered an error while performing a payment.
  - Usually, the logs are collected from STDOUT (standard out) and STDERR (standard error) through a passive logging mechanism. This means that any output or errors from the application are sent to the shell. Subsequently, these are collected by a logging tool, such as Fluentd or Splunk, and stored in backend storage. 
  - However, the application can send the logs directly to the backend storage. In this case, an active logging technique is used, as the log transmission is handled directly by the application, without a logging tool required.
  - There are multiple logging levels that can be attributed to an operation. Some of the most widely used are:
    - DEBUG - record fine-grained events of application processes
    - INFO - provide coarse-grained information about an operation
    - WARN - records a potential issue with the service
    - ERROR - notifies an error has been encountered, however, the application is still running
    - FATAL - represents a critical situation, when the application is not operational
  - As well, it is common practice to associate each log line with a timestamp, that will exactly record when an operation was invoked.

### Tracing
  - Tracing is capable of creating a full picture of how different services are invoked to fulfill a single request. 
  - Usually, tracing is integrated through a library at the application layer, where the developer can record when a particular service is invoked. 
  - These records for individual services are defined as spans. A collection of spans define a trace that recreates the entire lifecycle of a request.

### Resource Consumption
  - Resource consumption encapsulates the resources an application requires to be fully operational. 
  - This usually refers to the amount of CPU and memory that is consumed by an application during its execution. 
  - Additionally, it is beneficial to benchmark the network throughput, or how many requests can an application handle concurrently. 
  - Having awareness of resource boundaries is essential to ensure that the application is up and running 24/7.

### 

## For Quizzes check [here](https://github.com/sg7801/SUSE-Cloud-Native-Foundations-Scholarship/blob/main/Architecture%20Consideration%20for%20Cloud%20Native%20Applications/Quizzes.md) 
