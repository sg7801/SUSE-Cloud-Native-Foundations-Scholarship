## Q: Match the following Docker components with their main functionality
|Docker Components | Functionality|
|---|---|
|Dockerfile|Set of instructions to create a docker image|
|Docker image| A read only template that is used to spin up the container|
|Docker container|A runnable instance of docker image|
|Docker registry|a tool used to store and distribute docker images|

## Q: By default, Docker will create OCI (Open Container Initiative) compliant images. What is the reason for using OCI guidelines?
- [ ] To ensure everyone uses docker
- [x] To standardise the image formats
- [x] To ensure that images can execute on OCI compliant runtimes
- [ ] To ensure docker files are used as standard component

## Q: What is the Docker command used to get the following output?
|Command|Output|
|---|---|
|Build a Docker image using Dockerfile.staging file in the app/backend folder|docker build \ <br> -f Dockerfile.staging app/backend|
|Create an interactive shell to a busybox container|docker run-it busybox|
|Tag the new image ID as the front-end application in versionv4.5.2|docker tag f10fea406345 \ <br> pixelpotato/frontend: v4.5.2|
|Push the new front-end application to DockerHub|docker push\ <br> pixelpotato/frontend:v4.5.2|
|Login into the DockerHub using valid credentials|docker login|

## Q: The control plane makes the global decisions on the actions within a cluster. Which components are installed on a node to mark it as part of the control plane, but at the same time to ensure that this node is part of the Kubernetes cluster?
- [x] api-server
- [x] etcd
- [x] kubelet
- [x] kube-proxy
- [x] controller-manager
- [x] scheduler

## Q: The data plane is used to host workloads onto the cluster. Which components are installed on a node to mark it as part of the data plane in a Kubernetes cluster?
- [ ] api-server
- [x] kube-proxy
- [ ] controller-manager
- [ ] etcd
- [x] kubelet
- [ ] scheduler

## Q: What bootstrap tools can be used to provision a production-grade Kubernetes cluster?
- [ ] Minikube
- [x] Kops
- [x] Kubeadm
- [ ] Kind
- [x] Kubespray
- [x] K3s

## Q:What are the 3 main sections of a kubeconfig file?
- [x] Contexts
- [x] Users
- [ ] Tokens
- [x] Clusters

## Q: What Kubernetes resources are used to ensure the following functionalities?

|FUNCTIONALITY|KUBERNETES RESOURCES|
|---|---|
|Application management|Deployments, ReplicaSets, and Pods|
|Application reachability|Services and Ingress|
|Application configuration|Secrets and ConfigMaps|
|Application context|Namespaces|

## Q:What Kubernetes resources should be used to direct the external traffic to services within the cluster?
- [ ] Pods
- [ ] Services
- [x] Ingress
- [ ] Load balancers

## Q: What kubecti commands should be used to achieve the following output?
|Output|Kubectl Commands|
|---|---|
|Expose the backend deployment using a service on port 7653|kubectl expose deploy backend port-7633|
|Create a busybos deployment with 10 replicas, exposed on part 90se|kubectl create deploy busybox \ <br> --image=busybox -r-10 --port=9090|
|Label a configmap with the tier-networking key-value pair|kubectl label configmap app-cm tier-networking|
|Delete the sandbox namespace|kubectl delete ns sandbox|
|Describe the secret with the name team-token|kubect describe secret team-token|

## Q: What resource would be created with the following declarative manifest?
```
apiVersion: v1
data:
  token: YWJjZA==
kind: Secret
metadata:
  creation Timestamp: null
  name: team-token
```
- [ ] ConfigMap
- [ ] Deployment
- [ ] Pod
- [x] Secret

## Q: What properties are set in the following manifest for a pod?
```
[...]
spec:
  containers:
  - image: alpine
    name: test-pod
    ports:
    - containerPort: 5777
    resources:
      requests:
        cpu: 100m
        memory: 256Mi
    livenessProbe:
     httpGet:
       path: /
       port: 5777
```
- [x] CPU request of 100 millicpus
- [ ] Exposed on port 7555
- [x] A liveness probe to check the application on port 5777
- [x] Running the alpine image
- [ ] Memory limit of 256 Mebibytes
