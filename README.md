# tye-with-dotnet

Creating Microservices in a .NET Way
- runs all of the application services at once
- e.g <application-name> tye run //runs all the applciation in the solution at once
- picks unused ports whichever available at random , so no issue of conflicting ports
- provides a web interface to view and manage all the applications and logs as well,bindings,urls,restarts,logs
- tye utilizes service discovery, injects environment variables into the services before they start , so that the service that needs the url(destination) of another service(s) would know about it , that includes all the bindings and connectionstring required.
- Extension method is provided to get the binding/link e.g 
   var clientBaseAddress = Configuration.GetServiceUrl("backend"); //available due to tye injection process
- No need ot container services and docker services for auto discovery

Testing the applicaton in the kubernetes is difficult(lot of work upfront) :-
- create docker files
- build and push docker images with new versions
- write kubernetes manifests
- apply these manifests

Tye dockerises and deployes the services to kubernetes 
- uses the same conventions as development to keet the consistency(no code changes)
- microservice kubectl get deployments //check if already any deployments
- microservice kubectl get services   //check if any services running 
- microservice tye deploy -i 
  //it wil ask to the dockerhub container registry info , provide that
- tye will create :
  - a build output
  - a temp docker file 
  - executes the docket build to create a docker image 
  - pushes the image to the docker registry
  - kubernetes manifest will be generated and applied to kubernetes 
  - finally application will be available there in kubernetes environment 
So one single command does all the work without being manually do whole lot of steps manually or via scripts
- microservice kubectl port-forward svc/frontend 5000:80 //generated the service in port dignified 
- microservice kubectl describe deployment //will provide all the information and env variables that will be injected 

- 
