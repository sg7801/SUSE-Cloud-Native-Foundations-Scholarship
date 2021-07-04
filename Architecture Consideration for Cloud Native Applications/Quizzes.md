### Q: What application architecture a team is using if they manage multiple delivery pipelines, and binaries, but use only one programing language?
- [ ] Monolithic Architecture
- [x] Microservice Architecture

### Q:The first step in building a product is collecting requirements and listing the available resources. The requirements define the main functionalities of the projects and their users, while available resources provide the context of implementing these functionalities. Which listed options are valid requirements that need to be considered before developing an application?
- [ ] Available finances
- [x] Stakeholders
- [x] Handling of input data
- [ ] Project Timeframes

### Q: Imagine a mobile application that allows users to read the latest articles. Which application tier is suitable for each of the core functions?
Option 1 | Option 2
--- | --- 
UI | Mobile Application
Business Logic | Function to retrieve latest articles 
Data Layer | Function to store user preferences for articles

### Q: Which considerations does each trade-off cover?
Option 1 | Option 2
--- | --- 
Continuous project maintenance based on user feedback | Development complexity
Scale the application down when the number of the incoming request is low |  Scalability
Pipeline to ensure successful product release | Time to deploy
Adopt new functionalities and tooling | Flexibility 
Resources necessary throughout the project development and their cost | Operational Cost
Respond effectively to failure based on metrics and logs | Reliability 

### Q: Imagine a product that supports the handling of data with multiple databases. For example, a research team that benchmarks and evaluates a new database for their product. Which trade-off should the engineering team consider?
- [x] Flexibility
- [ ] Reliablity
- [ ] Scalability
- [ ] Time to deploy

### Q:Due to low customer satisfaction, an engineering team wants to optimize and refactor their product based on customer feedback. So far, the feedback highlights that the application errors when a transaction occurs or when a customer tries to access their account. What actions should the engineering team take to improve the reliability of the application?
- [x] Improve the log messages for each service, so it's easier to identify failures
- [ ] Check if the application scales under load
- [ ] Optimise the delivery pipeline
- [x] Check if the metrics are representative of the actual CPU and memory consumption for each service

### Q: What practice should be adopted to recreate the full journey of a request, including all the invoked functions?
- [ ] Health Checks
- [ ] Metrics
- [ ] Logs
- [x] Tracing

### Q: Match the API endpoint or expected output with a recommended development practice:

DEVELOPMENT PRACTICE | API ENDPOINT OR EXPECTED OUTPUT
--- | --- 
Logs | {"date" : "2021-01-01 02:00:01",<br>"severity" : "INFO",<br>"msg" : "foo logged in"}
Tracing | The full journey of a request and the function invoked
Health check | /status
Metrics | {"TotalRequests" : 5001,<br>"TotalRequestsFalied" : 35}
Resource consumption | CPU : 0.5 <br> Memory : 1028 MB

### Q: During the implementation stage, what practices should be adopted by a development team?
  - Building a metrics endpoint
  - Incorporating tracing at the application layer
  - Ensuring logs are captured when a failure occurs
  - Benchmarking the amount of CPU and memory the application requires

### Q: What practice is used to get the status of an application at a point in time?
- [ ] Tracing
- [ ] Logs
- [x] Health checks
- [ ] Resource Consumption









