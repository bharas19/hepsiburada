# hepsiburada
Hepsiburada Case

In this case, I plan to use Docker for containerization, Minikube and kubectl for orchestration and Jenkins for automation. So I start with installing the tools. I’ll skip the installment steps of the given tools and I’ll explain the configuration later parts.


a. Docker:  To start a docker,  I installed repository and docker engine. Figure 2 shows the details of the Docker Engine that installed on the server.
		

b. Minikube and Kubectl: 

I installed minikube and kubectl, details below:


c. Jenkins: 
I installed and set-up the Jenkins to work on port 8080.

http://34.77.185.189:8080/
	
 

2. Wrapping-up the Web-App

I’ve found a basic javaScript script and progressed with it. First I created a Dockerfile to wrap it up and build a docker image. I’ll share the Dockerfile script at the end.

docker build -t bharas19/hbjavasc:latest .

 
To test if the app is working or not, I run the image locally by exposing it to the port 11130 and saw that web-app is running.

docker run -p 11130:11130 -d bharas19/hbjavasc

 
After seeing that the container works fine, I pushed it to the docker.hub to pull it directly from the hub when working with kubernetes.

docker push bharas19/hbjavasc:latest

3. Kubernetes

To set up kubernetes clusters, I first created a basic deployment yaml (hbtest.yml)
I declared the specifications and route it to the container port of 11130. Then I run;

./kubectl create -f hbtest.yml

Then checked the pods and the status of the deployment. I saw the status is running. 


Later, I expose the port 11130 with NodePort by;

./kubectl expose deployment hbjavasc --type=NodePort --name=hbjavasc03

 
Since 11130 port binded containers 31205 port; we can reach the application we run as shown below:

 
4. Automation

At the end, with Jenkins, I created a simple pipeline which pulls a git repository, build docker and deploy it to the kubernetes cluster.

 

