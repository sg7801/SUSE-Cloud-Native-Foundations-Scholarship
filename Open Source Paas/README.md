# Open Source Paas
In this lesson, we have explored the Platform as a Service (PaaS) mechanism as a way to deploy a service without underlying infrastructure knowledge.
- Open Source PaaS lesson outline 
- Open Source PaaS lesson outline

**Throughout this lesson we will explore:**
- PaaS Mechanisms
- Cloud Foundry
- Function as a Service

![image](https://user-images.githubusercontent.com/61888364/124624574-9f11b600-de9a-11eb-9c54-1bddc7354de6.png)

## PaaS Mechanisms:

- Kubernetes offers a wide range of functionalities that form the principles of any modern infrastructure. 
- These capabilities revolve around automation, portability, extensibility, flexibility, self-healing, and many more. However, managing Kubernetes at scale is challenging, especially when the clusters are self-hosted in datacenters or private clouds. 
- In this case, a team has to keep up-to-date with the latest Kubernetes releases, to ensure the platform is updated, upgraded, managed, and configured to meet the production-grade standards.
- Within any organization, a release process consists of releasing the application to multiple environments, such as sandbox, staging, and production. 
- In this case, each environment is represented by a separate Kubernetes cluster, with a total of 3 clusters. However, the number of clusters grows exponentially if the platform is replicated across different regions. 
- This is usually required to keep market proximity and deliver a service to consumers with minimal latency. 
- As a result, if the infrastructure is distributed across the US, Europe, and the Asia Pacific, a team ends up operating 9 clusters. Configuring, managing, upgrading, updating, and deploying to all of these clusters is a herculean task and often requires a dedicated team.
- In these circumstances, if an organization does not have sufficient engineering resources, delegating the platform management to a 3rd party provider is a more suitable solution. This is covered by a **PaaS or Platform as a Service solution**.

**Some of the widely used cloud-computing services are:**
- **On-premise** - where an engineering team has full control over the platform, including the physical servers
- **IaaS or Infrastructure as a Service** - where a team consumes compute, network, and storage resources from a vendor
- **PaaS or Platform as a Service** - where the infrastructure is fully managed by a provider, and the team is focused on application deployment

![image](https://user-images.githubusercontent.com/61888364/124625030-10e9ff80-de9b-11eb-9493-8435b894b1b7.png)

- **Networking** - establish communication between internal and external systems, such as internet connection, firewalls, routers, and cables
- **Storage** - collect and store digital data, such as files, blocks, or objects
- **Servers** - physical machines that provide compute services for a platform
- **Virtualization** - abstracts physical servers, storage, and networking. For example, we have learned that hypervisors are used to virtualize servers.
- **O/S** - operating systems that connect the software to physical resources (e.g. Linux, Ubuntu, Windows, etc)
- **Middleware** - help the developers to build an application by making it easy to consume platform capabilities (e.g. messaging, API, data management)
- **Runtime** - execution context for an application. For example, using JVM (or Java Virtual Machine) as a Java runtime
- **Data** - tools for collection and storage of data that is required by an application during execution(e.g. MySQL, MongoDB, or CockroachDB)
- **Applications** - the business logic for a product

- **On-premise**:
On-premise represents a cloud-computing offering where the engineering team has full control of the platform services (from networking to applications). This solution is suitable for organizations that have sufficient engineering power and regulations that demand full control of their technology stack and operations within it.

- **IaaS**:
IaaS solutions provide the abstraction of networking, storage, server, and virtualization layers. As a result, these services are consumed on-demand by the engineering teams. Additionally, IaaS provides a suitable abstraction for the management of self-hosted Kubernetes clusters, which depend on compute, network, and storage components for a successful bootstrap process.
The most common IaaS solutions are delivered by public cloud providers such as AWS, GCP, Microsoft Azure, and many more.

- **PaaS**:
  -PaaS is a cloud-computing offering that enables an engineering team to fully focus on application development. It abstracts all services except the application and the data associated with it. As a result, the team is required to manage the code base and any database service that the product needs to be fully operational.
Popular PaaS solutions are App Engine from GCP, Heroku, Cloud Foundry, Beanstalk from AWS, and many more.
  - **Advantages**: 
    - **Time-efficiency** - engineering focus is shifter toward development rather than infrastructure management
    - **Scalability and high availability** - on-demand resource consumption enables an application to easily scale and fail-over
    - **Rich application catalog** - integration of external service (e.g. databases) with minimal effor
  - **Diadvantages**:   
    - **Vendor lock-in** - it is challenging to interchange PaaS providers without service disruption
    - **Data security** - since data is managed by a 3rd party, an extra layer of complexity is added to ensure data confidentiality
    - **Operational limitations** - the service catalog is limited to the services offered by the integrated cloud provider

    ![image](https://user-images.githubusercontent.com/61888364/124626214-185dd880-de9c-11eb-9f75-a4ddd7bf78c6.png)
    
- The fewer components are delegated to external providers, the more control there is over available functionalities
- The more ownership there is across the stack, the more complexity is introduced in managing and delivering the product
- The fewer components are managed by an engineering team, the quicker is the usability of the stack. As such, with a PaaS offering the engineering team can deploy their application immediately.
- While if choosing an on-premise solution, the release of a product is possible only after the platform is built.

![image](https://user-images.githubusercontent.com/61888364/124626383-3deae200-de9c-11eb-9d73-11bcd46fa482.png)

 ## Cloud Foundry:
 -  Integrating PaaS solutions within an organization shifts the engineering effort from infrastructure management to product development. Additionally, it provides a powerful developer experience throughout the release process of an application, where the main functionalities are consumed through a UI or console. However, there is one major downside with this offering: vendor and application catalog lock-in. If an application is deployed using a PaaS offering from GCP, the application catalog of external services is narrowed down to GCP services mainly. Consequently, the open-source fundamentals were applied to PaaS offerings, resulting in an open-source PaaS such as Cloud Foundry.

  - **Routing** - handle the incoming external traffic and route it to applications
  - **Authentication** - identity management to user accounts
  - **Application lifecycle** - controls the application deployments, monitors their status, and reconciles any new changes to reach the desired state of the application.
  - **Application storage and execution** - handle the availability of artifacts to applications
  - **Service** - use service brokers to provisions on-demand the dependency services for an application, such as a database or third-party APIs
  - **Messaging** - ensure the communication between Cloud Foundry components
  - **Metrics and logging** - aggregates the system and application metrics and logs

## Edge Case: Function as a Service
- An organization will always explore the most efficient offering to deploy a product to consumers. PaaS solutions are lightweight on initial setup, as a team can release the code in production within days.
- However, there are use cases where customers interact with a service only once a day or for a couple of hours within a day. For example, a service to update a timetable with the new bus schedule once a day. In this case, using a PaaS offering has one major downside: it is not cost-efficient. For example, with Cloud Foundry there will always be an instance of the application up and running, even if the service is used once a day. However, the team is billed for a full day.
- For this scenario, a **FaaS or Function as a Service** is a more suitable offering. FaaS is an event-driven cloud-computing service that allows the execution of code without any management of the infrastructure and configuration files. As a result, the timetable update service is invoked only once a day, and for the rest of the time, there are no replicas of this service. A team will be billed only for the time the service is executed.
- **Popular FaaS solutions are AWS Lambda, Azure Functions, Cloud Functions from GCP, and many more.**
- Throughout the release process, a FaaS solution only requires the application code that is built and executed immediately. In comparison with a PaaS offering, this FaaS has a quicker usability rate, as no data management or configuration files are necessary.

![image](https://user-images.githubusercontent.com/61888364/124627069-dd0fd980-de9c-11eb-8c36-c9b9038aeb8b.png)

