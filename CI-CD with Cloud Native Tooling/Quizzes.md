## Q:What stages are covered by Continuous Integration?
- [x] Build
- [ ] Deploy
- [x] Test
- [x] Package

## Q: What are the main advantages of using a CI/CD pipeline?
- [x] Frequent releases
- [x] Developer productivity
- [ ] Higher revenue
- [x] Less risk

## Q: What stages are covered by Continuous Delivery?
- [ ] Test
- [ ] Package
- [x] Deploy
- [ ] Build

## Q: You are provided with a Python front-end application. Match each Continuous Integration stage with the commands used to implement the expected operations.
|Stages|Commands|
|---|---|
|Run tests using Python testing frameworks|pytest|
|Install application dependencies|RUN pip install -r requirements.txt|
|Build the image of the application|docker build -t python-frontend|
|Store the Docker image in a registry|docker push pixelpotato/python-frontend:v4.3.8|

## Q: What are the characteristics of a typical Continuous Integration implementation?
- [x] Triggered at each commit
- [ ] The output is always a Docker image
- [ ] It is only used to test the code
- [x] The output can be an OCI compliant image

## Q: What is the most suitable characteristic for GitHub Actions?
- [ ] Can execute only 1 task
- [x] Event-driven workflows
- [ ] Is limited to run for Python applications

## Q: What are the characteristics of a typical Continuous Delivery implementation?
- [ ] Deploys only to sandbox
- [ ] Always requires a trigger to push to production
- [x] Release to multiple environments
- [x] Should be automatic and replicable

## Q: You are provided with a Python front-end application and need to implement the Continuous Delivery stage. Match each command to a deployment approach in a Kubernetes cluster?
|Development approach|Command|
|---|---|
|Declarative|kubectl apply -f frontend-deploy.yaml|
|Imperative|kubectl create deploy python-frontend\ <br> --image-pixelpotato/python-frontend:6.3.8|

## Q: Which statements are true based on the ArgoCD Application CRD snippet below?
```
source:
  path: go-backend
  repoURL: https://github.com/kgamanji/argocd-demo
  targetRevision: HEAD
```
- [ ] It will deploys the c592293 commit
- [x] It will deploy plain YAML manifests
- [x] The manifests are stored under argocd-demo/go-backend folder
- [ ] The manifests are stored under go-backend/argocd-demo folder

## Q: Match each configuration management technique with its main characteristic:
|Configuration management tool | characteristics|
|---|---|
|Jsonnet|A programming language used to template manifests as JSON files|
|Kustomize|A template-free mechanism that uses a base and multiple overlays|
|Helm|A package manager that template manifests using Go Template|

## Q: Which components construct a valid Helm chart?
- [x] values.yaml
- [ ] manifests/ folder
- [x] templates/folder.
- [x] Chart.yaml

## Q: What is the output of the following templated resource and input values file:
```
service.yaml

[...]
spec:
  ports:
  - port: {{ .Values.service.port }} 
    protocol:  {{ .Values.service.protocol }} 
  type: {{ .Values.service.type }} 
values.yaml

service:
  port: 4112
  protocol: UDP
  type: ClusterIP
```
- [ ] port: 6755; protocol: UDP; type: Cluster IP
- [ ] port: 4112; protocol: TCP; type: Cluster IP
- [ ] port: 4112; protocol: UDP; type: LoadBalancer
- [x] port: 4112; protocol: UDP; type: ClusterIP 
