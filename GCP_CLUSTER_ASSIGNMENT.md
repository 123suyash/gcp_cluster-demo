# 1. Register a GCP account
First things first: go ahead and register for a GCP account if you haven’t already.

# 2. Create the GCP project
Once you’ve registered, Create project in GCP named as Kyndryl-demo. This is where you create all of your GCP resources.
https://console.cloud.google.com/home/dashboard?project=kyndryl-demo&_ga=2.10889468.990794453.1650984853-830809271.1650984853

# 3. Create the GCP cluster using API command
# Prereuisite to install on your local windows machine
1) Install gcloud CLI
2) gcloud components install kubectl

# Command to create GCP cluster-
gcloud container clusters create --zone us-central1-a kyndryl-cluster-demo

# Connect to the above cluster-
gcloud container clusters get-credentials kyndryl-cluster-demo --zone us-central1-a --project kyndryl-demo

# To set the environment variable-
$Env:KUBECONFIG="C:\Users\SUYASH\.kube\config"

# Command to check cluster
kubectl get pods
kubectl get ns

# 4. Deploying Steps
### Step 1 : Creating namespace 
```
kubectl create namespace easyclaim

```
## Easyclaim backend
Backend code for easycliam application. The backend code is written in java springboot (Java 8)

Github Repository- https://github.com/123suyash/easyclaim-backend

## Deployment
### Deploy mysql database as deployment in Kubernetes
```
kubectl apply -f deployment/mysql/deployment/configmap.yaml -n easyclaim
kubectl apply -f deployment/mysql/deployment/secret.yaml -n easyclaim
kubectl apply -f deployment/mysql/deployment/deployment.yaml -n easyclaim
kubectl apply -f deployment/mysql/deployment/service.yaml -n easyclaim
```

### Deploy easyclaim backend java application as deployment in kubernetes
```
kubectl apply -f deployment/configmap.yaml -n easyclaim
kubectl apply -f deployment/deployment.yaml -n easyclaim
kubectl apply -f deployment/service.yaml -n easyclaim
```

### Deploying frontend container as deployment
```
Github Repository- https://github.com/123suyash/easyclaim-frontend

kubectl apply -f deployment.yml -n easyclaim
kubectl apply -f configmap.yml -n easyclaim
kubectl apply -f service.yml -n easyclaim

```
# 5. Few imporatant commands

kubectl get pods -n easyclaim  -- Shows pods under easyclaim namespace

kubectl get pods -o wide -- Gives IP address information for Pods 

kubectl get pods -o wide -n easyclaim -- Shows IP address for Pods under easyclaim namespace

kubectl logs easyclaim-backend-768bb946fc-9552l -n easyclaim -- To check the logs of running container pod

# 6. Web URL of deployed container application on cluster
http://35.226.138.218:32011/
