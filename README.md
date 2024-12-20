# anchal2610-MultiContainer-app-deployment


Multi-Container Application Deployment with Kubernetes
Overview
This document outlines the steps I took to deploy a multi-container application using Kubernetes, the solutions I implemented during the process, and the challenges I faced. The application consists of a backend, frontend, and a database service, deployed to a local Kubernetes cluster using Minikube.
________________________________________
Application Architecture
Components:
1.	Backend: Provides the core application logic.
2.	Frontend: User-facing interface interacting with the backend.
3.	Database: Stores application data.
Dependencies:
•	Docker Compose: For local deployment.
•	Kubernetes: For container orchestration.
•	Minikube: Local Kubernetes cluster.
________________________________________
Deployment Steps
1. Prerequisites
Below mentioned tools were installed:
•	Docker and Docker Compose
•	Kubernetes CLI (kubectl)
•	Minikube
•	Visual Studio Code (with Kubernetes extension)
2. Docker Compose Configuration
I created a docker-compose.yml file to define the application components:

 

3. Kubernetes Deployment Manifests
Namespace
I created a separate namespace for isolation: 
 

Backend Deployment and Service
          


Frontend Deployment and Service
               

Database Deployment and Service
         


4. Deployment
•	First, apply Namespace : 

   kubectl apply -f namespace.yaml

•	After that, we will deploy components:

kubectl apply -f backend-deployment.yaml
kubectl apply -f frontend-deployment.yaml
kubectl apply -f db-deployment.yaml

•	Lastly, we will verify if the resources are created or not:

kubectl get pods -n multi-container-app
kubectl get services -n multi-container-app
________________________________________
Challenges Faced and Solutions Implemented
1. TLS Handshake Timeout
•	Problem: kubectl returned Unable to connect to the server: net/http: TLS handshake timeout.
•	Solution: 
o	I restarted Minikube using minikube stop and minikube start.
o	I verified that system resources were sufficient.
2. Namespace Not Found
•	Problem: Services could not be created due to a missing namespace.
•	Solution: 
o	I explicitly created the namespace and added namespace to all resource files.
3. Application Buffering
•	Problem: The frontend application hosted on port 3000 was buffering.
•	Solution: 
o	I verified container logs using kubectl logs.
o	Resolved a network configuration issue in the frontend and backend services.
4. Docker Compose Errors
•	Problem: Obsolete version field and path errors in docker-compose.yml.
•	Solution: 
o	I removed the version field as it is no longer required.
o	Corrected the file paths and rebuilt the images.
________________________________________
Deployment Verification
1.	I verified running containers: 
2.	kubectl get pods -n multi-container-app
3.	I accessed the application endpoints: 
o	Frontend: http://localhost:3000
o	Backend: http://localhost:5000
o	Database: Exposed only within the cluster.

