# Progressive Weather App

### About

This repository is using vue framework to create frontend files.
<br>These frontend files are served using nginx. The minimal nginx configuration is in deployment-configurations directory.

### Image creation

This repository is using Dockerfile to build the npm package and create the image.
<br>Command used to create image execute is -
<br>`docker build -t frontend-server .`

### Kubernetes Deployment File

Kubernetes deployment file is present in deployment-configurations directory. The deployment comprises of

- 2 replicas (To prevent single point of failure)
- resource limts (To protect node from crashing and for hpa)
- startup, readiness and liveness probes (To restart the pod or accept the requests when required)
- affinity and tolerations (To deploy on specific node)

### Kubernetes Service File

Kubernetes service file is present in deployment-configurations directory. The service is having a annotation of aws loadbalancer. By default it will create a Classic Loadbalancer.
This service file is using label selector as `app: frontend-server` which is same for deployment.yaml

### Kubernetes Horizontal Pod Autoscalar

Kubernetes HPA file is also present in deployment-configurations directory. The purpose of this configuration is to increase the number of pods when avaerage CPU utilization reaches to 75%.

### Jenkinsfile

Jenkinsfile is present in root directory illustrating the deployment pipeline using Jenkins.

### TektonCd

In tektoncd-deployment folder, tektoncd configurations are present. Tekton is cloudnative solution and with these configurations, weather-app can be deployed using tektoncd also.
