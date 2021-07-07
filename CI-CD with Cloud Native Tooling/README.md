# CI/CD with Cloud Native Tooling

- Once a team has built a product and has structured a release process onto the platform, the next phase is to bring automation. A release process should enable a team to deliver new features to consumers, and it should be highly automated to eliminate misconfiguration scenarios. These functionalities are encapsulated by a CI/CD pipeline, for continuous integration and delivery of the new code changes.

- In this lesson, we have explored how to use cloud-native tooling to construct a CI/CD pipeline. As well, we will explore template configuration managers, such as Helm to enable the easy deployment of an application to multiple clusters.
  - Cloud Native CI/CD lesson outline 
  - Cloud Native CI/CD lesson outline

- Overall, in this lesson we will explore:
  - Continuous Application Deployment
  - The CI Fundamentals
  - The CD Fundamentals
  - Configuration Managers

![image](https://user-images.githubusercontent.com/61888364/124707036-e38e6780-df15-11eb-9f46-50021ffb8fab.png)

- We have practiced the packaging of an application using Docker and its deployment to a Kubernetes cluster using kubectl commands. As well, we have explored the simplified developer experience of application release with Cloud Foundry. However, in both cases, a user has to manually trigger and complete all the operations. This is not sustainable if tens and hundreds of releases are performed within a day. Automation of the release process is fundamental!

- In the case of a PaaS offering, the release of a new feature is managed by the provider. For example, Cloud Foundry monitors the repository with the source code, and when a new commit is identified, the user can easily deploy the latest changes with a click of a button. On the other side, releasing an application to a Kubernetes cluster consists of a series of manually typed docker and kubectl commands. At this stage, this approach has no automation integrated.

- In this lesson, we will not cover how a PaaS automates the release process, since this is already solutionized by the 3rd party providers. Instead, we will focus on building a delivery pipeline to automate the deployment to Kubernetes using cloud-native tooling.

A delivery pipeline is triggered when a new commit is available. The new changes should traverse the following stages:
- **Build** - compile the application source code and its dependencies. If this stage fails the developer should address it immediately as there might be missing dependencies or errors in the code.
- **Test** - run a suite of tests, such as unit testing, integration, UI, smoke, or security tests. These tests aim to validate the behavior of the code. If this stage fails, then developers must correct it to prevent dysfunctional code from reaching the end-users.
- **Package** - create an executable that contains the latest code and its dependencies. This is a runnable instance of the application that can be deployed to end-users.
- **Deploy** - push the packaged application to one or more environments, such as sandbox, staging, and production. Usually, the sandbox and staging deployments are automatic, and the production deployment requires engineering validation and triggering.

It is common practice to push an application through multiple environments before it reaches the end-users. Usually, these are categorized as follows:
- **Sandbox** - development environment, where new changes can be tested with minimal risk.
- **Staging** - an environment identical to production, and where a release can be simulated without affecting the end-user experience.
- **Production** - customer-facing environment and any changes in this environment will affect the customer experience.

![image](https://user-images.githubusercontent.com/61888364/124707508-8ba43080-df16-11eb-8bd5-08fc487dccb1.png)

Overall, a delivery pipeline consists of two phases:
- Continuous Integration (or CI) includes the build, test, and package stages.
- Continuous Delivery (or CD) handles the deploy stage.
-  Advantages of a CI/CD pipeline
  - Frequent releases - automation enables engineers to ship new code as soon as it's available and improves responsiveness to customer feedback.
  - Less risk - automation of releases eliminates the need for manual intervention and configuration.
  - Developer productivity - a structured release process allows every product to be released independently of other components

- Continuous Integration (CI) is a mechanism that produces the package of an application that can be deployed to consumers. As such, every commit to the main branch is built, tested, and packaged, if it meets the expected behavior. Within the cloud-native, the result of Continuous Integration represents a Docker image or an artifact that is OCI compliant.
![image](https://user-images.githubusercontent.com/61888364/124707671-c60dcd80-df16-11eb-8c0f-a33cb82f9adb.png)

## Build
- The build stage compiles the application source code and associated dependencies. We have explored this stage as part of the Dockerfile. For example, the Dockerfile for the Python hello-world application instructed the installation of dependencies from requirements.txt file and execution of the app.py at the container start.
### Test
- The technology landscape provides an abundance of frameworks, libraries, and tools to test and validate the behavior of an application. For Python application, some of the well-known frameworks are:
- pytest - for functional testing of the application
- pylint - for static code analysts of the application codebase

## Package
- The result of the package stage is an executable that contains the latest features and their dependencies. With Docker, this stage is implemented using docker build and docker push commands. These create a Docker image using a Dockerfile, and stores the image to a registry, such as DockerHub.
- GitHub Actions are event-driven workflows that can be executed when a new commit is available, on external or scheduled events. These can be easily integrated within any repository and provide immediate feedback if a new commit passes the quality check. Additionally, GitHub Actions are supported for multiple programming languages and can offer tailored notifications (e.g. in Slack) and status badges for a project.
- A GitHub Action consists of one or more jobs. A job contains a sequence of steps that execute standalone commands, known as actions. When an event occurs, the GitHub Action is triggered and executes the sequence of commands to perform an operation, such as code build or test.
![image](https://user-images.githubusercontent.com/61888364/124707950-2997fb00-df17-11eb-92c3-1cdda97a1009.png)
- GitHub Actions are configured using YAML syntax, hence uses the .yaml or .yml file extensions. These files are stored in .github/workflows directory within the code repository. 

## The CD Fundamentals
- Once an engineering team has automated the packaging of an application, the next phase is to release it to customers. Before the application is pushed to a production environment, it is important to check the functionality of an application when deployed and integrated with platform components. Only when the application meets the excepted behavior, it is deployed to a customer-facing environment. The process of propagating an application through multiple environments, until it reached the end-users, is known as the Continuous Delivery (or CD) stage.
- It is common practice to push the code through at least 3 environments: sandbox, staging, and production. A reminder of each environment's purpose :
  - **Sandbox** - development environment, where new changes can be tested with minimal risk.
  - **Staging** - an environment identical to production, and where a release can be simulated without affecting the end-user experience.
  - **Production** - customer-facing environment and any changes in this environment will affect the customer experience.

![image](https://user-images.githubusercontent.com/61888364/124708169-8398c080-df17-11eb-90d0-57037315946f.png)

## Argo CD
- ArgoCD is a declarative Continuous Delivery tool for Kubernetes, which follows the GitOps patterns. As such, ArgoCD operates on configuration stored in manifests (declarative) and uses Git repositories as the source of truth for the desired state of an application (GitOps pattern). 
- As such, ArgoCD monitors the new commits to Git repositories and applies the latest changes reconciled automatically or on a manual trigger. Additionally, ArgoCD offers deployment to target environments and multiple clusters, and support for multiple config management tools (such as plain YAML, Helm, Kustomize).
- For application deployment through multiple environments, ArgoCD provides CRDs (Custom Resource Definitions) to configure and manage the application release.

## Project resource
- The Project resource is a CRD that provides a logical grouping of applications, including access to source and destination repositories, and permissions to resources within the cluster. This resource is handy to segregate and control the deployment to multiple clusters.

## Application resource
- The Application resource that stores the configuration of how an application should be deployed and managed.
Let's explore how a Python hello-world application is deployed using an ArgoCD Application resource: Note: It is assumed that the declarative manifests for Python hello-world are available ((e.g. deploy.yaml, service.yaml, etc).

![image](https://user-images.githubusercontent.com/61888364/124708322-be9af400-df17-11eb-80b9-ded07f385ad4.png)

- ArgoCD provides an “app-of-apps” technique that enables a group of applications to be deployed and configured together. 
- This technique is useful if a product is developed using a microservice-based architecture, and a single point of orchestration is necessary to deploy all microservices. 
- For example, a Web-store Application CRD can be used to manage the Application CRDs for the UI, Login, and Payment units. In this case, one point of control is provisioned to release and manage multiple microservices.

## Configuration Managers
- A CI/CD pipeline is essential to automate and standardize the application release process. New changes are propagated through multiple environments, including the production cluster, and ensure that the consumers can use the latest features. In an ideal situation, all clusters are similarly configured, such that the engineering team can inspect a realistic simulation of a production deployment. 
- This implies that a set of nearly similar manifests are required for each cluster, sandbox, staging, and production. To reduce the management overhead of overseeing a similar suite configuration for each cluster, templating is necessary.
- For example, to deploy the nginx-alpine application 4 resource manifests were necessary: Namespace, Deployment, Service, and Configmap. However, this suite of manifests represents the deployment to a single environment, e.g sandbox. 
- The application should be propagated through staging and production environment, which reference a separate set of manifests. 
- It is essential to ensure that the application configuration is tailored for each environment, for example, allocate more CPU and memory to the application in production since it handles more traffic, or have a different number of replicas for each cluster. In this case, an engineering team ends up managing 3 sets of manifests, 1 for each cluster.

![image](https://user-images.githubusercontent.com/61888364/124708641-2b15f300-df18-11eb-81d0-982aceb25bb1.png)

![image](https://user-images.githubusercontent.com/61888364/124708666-3537f180-df18-11eb-9612-8fa17a4108a8.png)

- **Helm** - package manager that templates exiting manifests, and uses input files to tailor configuration for each environment
- **Kustomize** - a template-free mechanism that uses a base and multiple overlays, to manage the configuration for each environment
- **Jsonnet** - a programming language, that enables the templating of manifests as JSON files, that can be easily consumed by Kubernetes

- Helm is a package manager, that manages Kubernetes manifests through charts. A Helm chart is a collection of YAML files that describe the state of multiple Kubernetes resources. These files can be parametrized using Go template.
- A Helm chart is composed of the following files:
  - **Chart.yaml** : expose chart details, such as description, version, and dependencies
  - **templates/ folder** - contains templates YAML manifests for Kubernetes resources
  - **values.yaml** - default input configuration file for the chart. If no other values file is supplied, the parameters in this file will be used.

![image](https://user-images.githubusercontent.com/61888364/124708901-82b45e80-df18-11eb-9048-2d4bb4244faf.png)

- Templates folder
The templates/ folder is a directory containing templated YAML manifests, that require an input file to generate valid Kubernetes resources. For example, the templates/ folder contains the manifests for Deployment and Namespace resources, used to deploy the Python hello-world application:
```
templates/
├── deployment.yaml
└── namespace.yaml
```
## Push-based CI/CD
- In a push-based model, as shown in the image below:
  - (1)the developer commits new code to the Git repository:
  - (2) which triggers the Continuous Integration stages 
  - (3) The code is packaged and distributed using an image registry, such as DockerHub 
  - (4) The Continuous Delivery stage is triggered once the YAML manifests are updated to reference the new image tag 
  - (5) A Continuous Delivery tool then pushed the updated manifests to multiple clusters 

![image](https://user-images.githubusercontent.com/61888364/124709291-efc7f400-df18-11eb-82f7-de096bb58cbd.png)

## Pull-based CI/CD
In a pull-based CI/CD approach:
  - the release process is still be triggered by a developer that pushed new features to the source code 
  - The package of the application is similar, resulting in a new image stored in DockerHub 
  - However, once the YAML manifests are updated with the new image tag, a pull-based Continuous Delivery tool identifies new changes and applies them to a Kubernetes cluster
  - As a result, this simplifies the process of application release, as new features can be applied automatically as soon as they are available. Tools that offer this CI/CD model are ArgoCD and Flux.

![image](https://user-images.githubusercontent.com/61888364/124709451-2271ec80-df19-11eb-9a64-d2f43b104d0c.png)

- It is paramount to build a deployment pipeline that fits the business requirements closely and automates the release process. There is no "golden path" that would cover all engineering requirements. However, the pull and push-based CI/CD tools contribute to the ultimate goal to ships code securely, automatically, and reliably.



