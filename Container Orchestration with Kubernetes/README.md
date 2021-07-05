# Container Orchestration With Kubernetes 
- In this lesson, we discussed how an application can be packaged using Docker and released to a Kubernetes cluster. Image showcasing the Container Orchestration lesson outline container Orchestration lesson outline

- Overall, in this lesson we will explore:
  - Docker for Application Packaging
  - Container Orchestration with Kubernetes
  - Kubernetes Resources
  - Declarative Kubernetes Manifests

![image](https://user-images.githubusercontent.com/61888364/124453719-47dde980-dda5-11eb-8fd7-14540962d148.png)

## VMs:
- VMs (Virtual Machines) were the main mechanism to host an application. VMs encapsulate the code, configuration files, and dependencies necessary to execute the application.
- VM is composed of an operating system (OS) with a set of pre-installed libraries and packages. During execution, an application utilizes an OS filesystem, resources, and packages.

![image](https://user-images.githubusercontent.com/61888364/124453900-76f45b00-dda5-11eb-8cb2-f4405b56cc30.png)

- A set of VMs is managed through a hypervisor. A hypervisor provides the virtualization of the infrastructure which is composed of physical servers.
- Hypervisor is capable of creating, configuring, and managing multiple VMs on the available servers. For example, we are able to running applications A, B, and C on 3 separate VMs.
- The utilization of VMs introduced standardization in infrastructure provisioning, in association with efficient use of available infrastructure. Instead of running an application per server, a hypervisor enables multiple VMs to run at the same time to host multiple applications. 
- However, there is one downside to this mechanism: **it is not efficient enough**. For example, applications A, B, and C uses the same Operating System. Replicating an OS consumes a lot of resources, and the more applications we run the more space we allocate to the replication of the operating systems alone.
- There was a clear need to optimize the usage of the available infrastructure. As a result, the virtualization of the Operating System was introduced. 
- This prompted the appearance of containers, which represent the bare minimum an application requires for a successful execution e.g. code, config files, and dependencies. By default, there is a better usage of available infrastructure.
- The appearance of containers is unlocked by OS-level virtualization and as a result, multiple applications can run on the same OS. By nature, containers are lightweight, as these encapsulate only the application code and essential dependencies. Consequently, there is a better usage of available infrastructure and a more efficient pathway to release a product to consumers.
- The appearance of containers enabled organizations to ship products using a lightweight mechanism, that would make the most of available infrastructure. There are plenty of tools used to containerize services, however, Docker has set the industry standards for many years.
- To containerize an application using Docker, 3 main components are distinguished: Dockerfiles, Docker images, and Docker registries. Let's explore each component in a bit more detail!

![image](https://user-images.githubusercontent.com/61888364/124454270-ea966800-dda5-11eb-98f9-cb256fcf5906.png)

## Dockerfile
- A Dockerfile is a set of instructions used to create a Docker image. Each instruction is an operation used to package the application, such as installing dependencies, compile the code, or impersonate a specific user. 
- A Docker image is composed of multiple layers, and each layer is represented by an instruction in the Dockerfile. All layers are cached and if an instruction is modified, then during the build process only the changed layer will be rebuild. As a result, building a Docker image using a Dockerfile is a lightweight and quick process.
- To construct a Dockerfile, it is necessary to use the pre-defined instructions, such as:
```
FROM -  to set the base image
RUN - to execute a command
COPY & ADD  - to copy files from host to the container
CMD - to set the default command to execute when the container starts
EXPOSE - to expose an application port 
```
## Dockerimage
- Once a Dockerfile is constructed, these instructions are used to build a Docker image. 
- A Docker image is a read-only template that enables the creation of a runnable instance of an application. 
- In a nutshell, a Docker image provides the execution environment for an application, including any essential code, config files, and dependencies.
- A Docker image can be built from an existing Dockerfile using the docker build command. Below is the syntax for this command:
```
# build an image
# OPTIONS - optional;  define extra configuration
# PATH - required;  sets the location of the Dockefile and  any referenced files 
docker build [OPTIONS] PATH

# Where OPTIONS can be:
-t, --tag - set the name and tag of the image
-f, --file - set the name of the Dockerfile
--build-arg - set build-time variables

# Find all valid options for this command 
docker build --help
```
- To build the image of the Python hello-world application from the Dockerfile, the following command can be used:
```
# build an image using the Dockerfile from the current directory
docker build -t python-helloworld .

# build an image using the Dockerfile from the `lesson1/python-app` directory
docker build -t python-helloworld lesson1/python-app
```
## Docker Registry
- The last step in packaging an application using Docker is to store and distribute it. So far, we have built and tested an image on the local machine, which does not ensure that other engineers have access to it. As a result, the image needs to be pushed to a public Docker image registry, such as DockerHub, Harbor, Google Container Registry, and many more. 
- To tag an existing image on the local machine, the docker tag command is available. Below is the syntax for this command:
```
# tag an image
# SOURCE_IMAGE[:TAG]  - required and the tag is optional; define the name of an image on the current machine 
# TARGET_IMAGE[:TAG] -  required and the tag is optional; define the repository, name, and version of an image
docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
```
- Once the image is tagged, the final step is to push the image to a registry. For this purpose, the docker push command can be used. Below is the syntax for this command:
```
# push an image to a registry 
# NAME[:TAG] - required and the tag is optional; name, set the image name to be pushed to the registry
docker push NAME[:TAG]
```
- OPTIONS - define extra configuration through flags
- IMAGE - sets the name of the image 
- NAME- set the name of the image
- COMMAND and ARG - instruct the container to run specific commands associated with a set of arguments

## Kubernetes - The Container Orchestrator Framework
- Running an application in production implies that thousands and millions of customers might consume the product at the same time. For this reason, it is paramount to build for scale. 
- It is impossible to manually manage thousands of containers, keeping these are up to date with the latest code changes, in a healthy state, and accessible. As a result, a container orchestrator framework is necessary.
- Kubernetes took the lead in defining the principles of how to run containerized workloads on a distributed amount of machines.
- Kubernetes is widely adopted in the industry today, with most organizations using it in production. Kubernetes currently is a graduated CNCF project, which highlights its maturity and reported success from end-user companies.


|Feature|Advantage|
|-------|---------|
|Portability|Kubernetes is a highly portable tool. This is due to its open-source nature and vendor agnosticism. As such, Kubernetes can be hosted on any available infrastructure, including public, private, and hybrid cloud.|
|Scalability|Building for scale is a cornerstone of any modern infrastructure, enabling an application to scale based on the amount of incoming traffic. Kubernetes has in-build resources, such as HPA (Horizontal Pod Autoscaler), to determine the required amount of replicas for a service. Elasticity is a core feature that is highly automated within Kubernetes.|
|Resilience|Failure is expected on any platform. However, it is more important to be able to recover from failure fast and build a set of playbooks that minimizes the downtime of an application. Kubernetes uses functionalities like ReplicaSet, readiness, and liveness probes to handle most of the container failures, which enables powerful self-healing capability.|
|Service Discover | Service discovery encapsulates the ability to automatically identify and reach new services once these are available. Kubernetes provide cluster level DNS (or Domain Name System), which simplifies the accessibility of workloads within the cluster. Additionally, Kubernetes provides routing and load balancing of incoming traffic, ensuring that all requests are served without application overload.|
|Extensibility|Kubernetes is a highly extensible mechanism that uses the building-block principle. It has a set of basic resources that can be easily adjusted. Additionally, it provides a rich API interface, that can be extended to accommodate new resources or CRDs (Custom Resource Definitions).|
|Operational Cost|Operational cost refers to the efficiency of resource consumption within a Kubernetes cluster, such as CPU and memory. Kubernetes has a powerful scheduling mechanism that places an application on the node with sufficient resources to ensure the successful execution of the service. As a result, most of the available infrastructure resources are allocated on-demand. Additionally, it is possible to automatically scale the size of the cluster based on the current incoming traffic. This capability is provisioned by the cluster-autoscaler, which guarantees that the cluster size is directly proportional to the traffic that it needs to handle.|

## Kubernetes AArchitecture
![image](https://user-images.githubusercontent.com/61888364/124473171-9ea2ed80-ddbc-11eb-8be6-300ab55b581c.png)
- A Kubernetes cluster is composed of a collection of distributed physical or virtual servers. These are called nodes. Nodes are categorized into 2 main types: master and worker nodes. The components installed on a node, determine the functionality of a node, and identifies it as a master or worker node.
- The suite of master nodes, represents the control plane, while the collection of worker nodes constructs the data plane.

## Control Plane
![image](https://user-images.githubusercontent.com/61888364/124473336-d1e57c80-ddbc-11eb-9e83-53b77acc0181.png)
- The control plane consists of components that make global decisions about the cluster. These components are the:
  - kube-apiserver - the nucleus of the cluster that exposes the Kubernetes API, and handles and triggers any operations within the cluster
  - kube-scheduler - the mechanism that places the new workloads on a node with sufficient satisfactory resource requirements
  - kube-controller-manager - the component that handles controller processes. It ensures that the desired configuration is propagated to resources
  - etcd - the key-value store, used for backs-up and keeping manifests for the entire cluster
## Data plane 
- The data plane consists of the compute used to host workloads. The components installed on a worker node are the:
  - kubelet - the agent that runs on every node and notifies the kube- apiserver that this node is part of the cluster
  - kube-proxy - a network proxy that ensures the reachability and accessibility of workloads places on this specific node

## Kubectl Commands:
```
# Inspect available vagrant boxes 
vagrant status 

# create a vagrant box using the Vagrantfile in the current directory
vagrant up

# SSH into the vagrant box
# Note: this command uses the .vagrant folder to identify the details of the vagrant box
vagrant ssh
```

|Name |Command |
|---|---|
|Create Resources|kubectl create RESOURCE NAME FLAGS|
|Describe Resources|kubectl describe RESOURCE NAME |
|Get Resources|Here -o yaml instructs that the result should be YAML formated. <br>kubectl get RESOURCE NAME -o yaml|
|Edit Resources|Here -o yaml instructs that the edit should be YAML formated.<br>kubectl edit RESOURCE NAME -o yaml|
|Label Resources|kubectl label RESOURCE NAME PARAMS|
|Port-forward to Resources|kubectl port-forward RESOURCE/NAME PARAMS|
|Logs from Resources|kubectl logs RESOURCE/NAME FLAGS|
|Delete Resources|kubectl delete RESOURCE NAME|

- Imperative configuration 
  - resource management technique, that operates and interacts directly with the live objects within the cluster.
- Declarative configuration 
  - resource management technique, that operates and manages resources using YAML manifests stored locally.

## Failing Control Plane for Kubernetes
- Failure is expected in any technology stack. However, it is more important to have efficient remediations steps rather than plan for no-failure scenarios. Kubernetes provides methods to handle some of the low-level failures and ensure the application is healthy and accessible. Some of these resources are:
- ReplicaSets - to ensure that the desired amount of replicas is up and running at all times
- Liveness probes - to check if the pod is running, and restart it if it is in an errored state
- Readiness probes - ensure that traffic is routed to that pods that are ready to handle requests
- Services - to provide one entry point to all the available pods of an application
- These services, prompt the automatic recovery of an application if an error is encountered. However, failure can happen at the cluster-level, for example, a control plane failure.
- In this case, a subset or all control plane components are compromised. While the situation is disastrous, the applications are still running and handling traffic. The downside of the control plane failure is that no new workloads can be deployed and no changes can be applied to the existing workloads.

The engineering team needs to recover the control plane components as a critical priority. However, they should not worry about recovering applications, as these will be intact and still handling requests.
