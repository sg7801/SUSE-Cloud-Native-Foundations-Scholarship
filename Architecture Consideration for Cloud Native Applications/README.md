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

# For Quizzes check [here](https://github.com/sg7801/SUSE-Cloud-Native-Foundations-Scholarship/blob/main/Introduction%20to%20Cloud%20Native%20Fundamentals/Quizzes.md) 
