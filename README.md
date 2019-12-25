# Docker in 5 Steps

Let's learn Docker in 5 Easy Steps. 

Watch the Video Now - https://www.youtube.com/watch?v=Rt5G5Gj7RP0

- Step 00 - Installing Docker
- Step 01 - A simple Docker use case - Run an existing application
- Step 02 - Playing with Docker - Containers and Images
- Step 03 - How does Docker work?
- Step 04 - Manually creating a docker image
- Step 05 - Dockerizing a Spring Boot Application using Dockerfile and Spotify Maven Plugin

### Step 00 - Installing Docker

- https://docs.docker.com/install/

### Step 01 - A Simple Docker User Case - Run an existing application

- https://hub.docker.com/u/sdannarapu

```
### troubleshooting mvn package issue
no matching manifest for windows/amd64 in the manifest list entries
I had issue on Windows 10. Just run the docker daemon in experimental mode and it should work. Follow the below steps:

Right click Docker user interface
Go to Settings
Daemon
Advanced
Set the "experimental": true
Restart Docker
```

```
docker run -d -p 5000:5000 sdannarapu/docker-todo-rest-api-h2:1.0.0.RELEASE
```

```
docker run -d -p 8761:8761 springcloud/eureka
```

```
docker run -d -e MYSQL_ROOT_PASSWORD=dummypassword -e MYSQL_USER=todos-user -e MYSQL_PASSWORD=dummytodos -e MYSQL_DATABASE=todos --p 3306:3306 mysql:5.7
```

#### Traditional Deployment

![Traditional Deployment](images/docker-traditional-deployment.png)

#### Deployment with Docker

![Docker Deployment](images/docker-zz-deployment.png)


### Step 02 - Playing with Docker - Containers and Images

- Image is static
- Container is dynamic

```
  649  docker run sdannarapu/docker-todo-rest-api-h2:1.0.0.RELEASE
  650  docker run -p 5000:5000 sdannarapu/docker-todo-rest-api-h2:1.0.0.RELEASE
  651  clear
  652  docker run -p 8761:8761 springcloud/eureka
  653  clear
  654  docker run -d -p 5000:5000 sdannarapu/docker-todo-rest-api-h2:1.0.0.RELEASE
  655  docker run -d -p 8761:8761 springcloud/eureka
  656  docker images
  657  docker containers 
  658  docker containers ls
  659  docker container
  660  docker container ls
  661  docker container ls -l
  662  docker container ls -l
  663  docker container ls
  664  docker container ls -a
  665  clear
  666  docker container ls -a
  667  docker container start fed549e69e9d
  668  docker container ls
  669  docker container stop tender_ardinghelli
  670  docker container ls
  671  docker container ls -a
  672  clear
  673  docker container ls -a
  674  docker container start c165f459e7d7
  675  docker container stop 151a77679241
  676  docker container start c165f459e7d7
  677  docker container logs c165f459e7d7
  678  docker container logs c165f459e7d7
  679  docker container logs c165f459e7d7
  680  docker container logs c165f459e7d7
  681  docker container ls
  682  docker container ls -a
  683  docker container rm fed549e69e9d
  684  docker container ls -a
  685  docker container prune
  686  docker container ls -a
  687  docker container inspect 0967ba7aa180
  688  docker images
  689  docker image history f8049a029560
  690  clear
  691  docker images
  692  docker image history sdannarapu/docker-todo-rest-api-h2
  693  docker image history sdannarapu/docker-todo-rest-api-h2:1.0.0.RELEASE
  694  docker images
  695  docker image remove f8049a029560
  696  docker image remove 3094afcbdf12
  697  docker container stop c165f459e7d7
  698  docker image remove 3094afcbdf12
  699  docker container rm c165f459e7d7
  700  docker image remove 3094afcbdf12
  701  docker images
  702  docker containers ls
  703  docker container ls
  704  docker container ls -a
```

### Step 03 - How does Docker work?

#### Docker Architecture

![Docker Architecture](images/docker-architecture.png)

### Step 04 - Manually creating a new docker image

```
  716  docker run -dit openjdk:8-jdk-alpine
  720  docker container cp target/docker-in-5-steps-todo-rest-api-h2-1.0.0.RELEASE.jar 28d5e5d893fdb1530e9920ff66fee252adc834a8b572b77b3fdf7d316730127c:/tmp
  725  docker container exec romantic_aryabhata ls /tmp
    734  docker container commit romantic_aryabhata sdannarapu/manual-todo-rest-api:v1
  735  docker container commit --change='CMD ["java","-jar","/tmp/docker-in-5-steps-todo-rest-api-h2-1.0.0.RELEASE.jar"]' romantic_aryabhata sdannarapu/manual-todo-rest-api:v2
  743  docker run -d -p 5000:5000 sdannarapu/manual-todo-rest-api:v2
```

### Step 05 : Containerizing Spring Boot Application using Dockerfile and Spotify Maven Plugin

Run com.rest.webservices.restfulwebservices.RestfulWebServicesApplication as a Java Application.

- mvn package
- docker run -d -p 5000:5000 sdannarapu/docker-todo-rest-api-h2:1.0.0.RELEASE
- docker login
- docker push sdannarapu/docker-todo-rest-api-h2:1.0.0.RELEASE

#### Troubleshooting

- Problem - Caused by: com.spotify.docker.client.shaded.javax.ws.rs.ProcessingException: java.io.IOException: No such file or directory
- Solution - Check if docker is up and running!
- Problem - Error creating the Docker image on MacOS - java.io.IOException: Cannot run program “docker-credential-osxkeychain”: error=2, No such file or directory
- Solution - https://medium.com/@dakshika/error-creating-the-docker-image-on-macos-wso2-enterprise-integrator-tooling-dfb5b537b44e


#### Creating Containers

To test execute API at http://localhost:5000/users/Srikanth/todos.

```
docker login
```

#### Hello World URLS

- http://localhost:5000/hello-world

```txt
Hello World
```

- http://localhost:5000/hello-world-bean

```json
{"message":"Hello World - Changed"}
```

- http://localhost:5000/hello-world/path-variable/sdannarapu

```json
{"message":"Hello World, Srikanth"}
```


#### Todo JPA Resource URLs

- GET - http://localhost:5000/jpa/users/Srikanth/todos

```
[
  {
    "id": 10001,
    "username": "Srikanth",
    "description": "Learn JPA",
    "targetDate": "2019-06-27T06:30:30.696+0000",
    "done": false
  },
  {
    "id": 10002,
    "username": "Srikanth",
    "description": "Learn Data JPA",
    "targetDate": "2019-06-27T06:30:30.700+0000",
    "done": false
  },
  {
    "id": 10003,
    "username": "Srikanth",
    "description": "Learn Microservices",
    "targetDate": "2019-06-27T06:30:30.701+0000",
    "done": false
  }
]
```

##### Retrieve a specific todo

- GET - http://localhost:5000/jpa/users/Srikanth/todos/10001

```
{
  "id": 10001,
  "username": "Srikanth",
  "description": "Learn JPA",
  "targetDate": "2019-06-27T06:30:30.696+0000",
  "done": false
}
```

##### Creating a new todo

- POST to http://localhost:5000/jpa/users/Srikanth/todos with BODY of Request given below

```
{
  "username": "Srikanth",
  "description": "Learn to Drive a Car",
  "targetDate": "2030-11-09T10:49:23.566+0000",
  "done": false
}
```

##### Updating a new todo

- http://localhost:5000/jpa/users/sdannarapu/todos/10001 with BODY of Request given below

```
{
  "id": 10001,
  "username": "Srikanth",
  "description": "Learn to Drive a Car",
  "targetDate": "2045-11-09T10:49:23.566+0000",
  "done": false
}
```

##### Delete todo

- DELETE to http://localhost:5000/jpa/users/Srikanth/todos/10001


#### H2 Console

- http://localhost:5000/h2-console
- Use `jdbc:h2:mem:testdb` as JDBC URL 

### Important kubectl Commands 

```

docker run -p 8080:8080 sdannarapu/hello-world-rest-api:0.0.1.RELEASE

kubectl create deployment hello-world-rest-api --image=sdannarapu/hello-world-rest-api:0.0.1.RELEASE
kubectl expose deployment hello-world-rest-api --type=LoadBalancer --port=8080
kubectl scale deployment hello-world-rest-api --replicas=3
kubectl delete pod hello-world-rest-api-58ff5dd898-62l9d
kubectl autoscale deployment hello-world-rest-api --max=10 --cpu-percent=70
kubectl edit deployment hello-world-rest-api #minReadySeconds: 15
kubectl set image deployment hello-world-rest-api hello-world-rest-api=sdannarapu/hello-world-rest-api:0.0.2.RELEASE

gcloud container clusters get-credentials srikanth-cluster --zone us-central1-a --project solid-course-258105
kubectl create deployment hello-world-rest-api --image=sdannarapu/hello-world-rest-api:0.0.1.RELEASE
kubectl expose deployment hello-world-rest-api --type=LoadBalancer --port=8080
kubectl set image deployment hello-world-rest-api hello-world-rest-api=DUMMY_IMAGE:TEST
kubectl get events --sort-by=.metadata.creationTimestamp
kubectl set image deployment hello-world-rest-api hello-world-rest-api=sdannarapu/hello-world-rest-api:0.0.2.RELEASE
kubectl get events --sort-by=.metadata.creationTimestamp
kubectl get componentstatuses
kubectl get pods --all-namespaces

kubectl get events
kubectl get pods
kubectl get replicaset
kubectl get deployment
kubectl get service

kubectl get pods -o wide

kubectl explain pods
kubectl get pods -o wide

kubectl describe pod hello-world-rest-api-58ff5dd898-9trh2

kubectl get replicasets
kubectl get replicaset

kubectl scale deployment hello-world-rest-api --replicas=3
kubectl get pods
kubectl get replicaset
kubectl get events
kubectl get events --sort.by=.metadata.creationTimestamp

kubectl get rs
kubectl get rs -o wide
kubectl set image deployment hello-world-rest-api hello-world-rest-api=DUMMY_IMAGE:TEST
kubectl get rs -o wide
kubectl get pods
kubectl describe pod hello-world-rest-api-85995ddd5c-msjsm
kubectl get events --sort-by=.metadata.creationTimestamp

kubectl set image deployment hello-world-rest-api hello-world-rest-api=sdannarapu/hello-world-rest-api:0.0.2.RELEASE
kubectl get events --sort-by=.metadata.creationTimestamp
kubectl get pods -o wide
kubectl delete pod hello-world-rest-api-67c79fd44f-n6c7l
kubectl get pods -o wide
kubectl delete pod hello-world-rest-api-67c79fd44f-8bhdt

kubectl get componentstatuses
kubectl get pods --all-namespaces

gcloud auth login
kubectl version
gcloud container clusters get-credentials srikanth-cluster --zone us-central1-a --project solid-course-258105

kubectl set image deployment hello-world-rest-api hello-world-rest-api=sdannarapu/hello-world-rest-api:0.0.4-SNAPSHOT

kubectl rollout history deployment hello-world-rest-api
kubectl set image deployment hello-world-rest-api hello-world-rest-api=sdannarapu/hello-world-rest-api:0.0.4-SNAPSHOT --record

kubectl rollout history deployment hello-world-rest-api
kubectl rollout status deployment hello-world-rest-api
kubectl rollout undo deployment hello-world-rest-api --to-revision=3
kubectl rollout status deployment hello-world-rest-api
kubectl rollout undo deployment hello-world-rest-api --to-revision=3
kubectl rollout status deployment hello-world-rest-api
kubectl rollout history deployment hello-world-rest-api
kubectl get pods
kubectl logs hello-world-rest-api-67c79fd44f-d6q9z
kubectl logs hello-world-rest-api-67c79fd44f-d6q9z -f

kubectl get deployment hello-world-rest-api
kubectl get deployment hello-world-rest-api -o wide
kubectl get deployment hello-world-rest-api -o yaml
kubectl get deployment hello-world-rest-api -o yaml > deployment.yaml
kubectl get service hello-world-rest-api -o yaml
kubectl get service hello-world-rest-api -o yaml > service.yaml

kubectl delete all -l app=hello-world-rest-api
kubectl get all
kubectl apply -f deployment.yaml
kubectl get all

kubectl diff -f deployment.yaml 
kubectl apply -f deployment.yaml 
kubectl delete all -l app=hello-world-rest-api
kubectl get all -o wide

mvn clean install
docker push sdannarapu/todo-web-application-h2:0.0.1-SNAPSHOT
kubectl delete all -l app=hello-world-rest-api

kubectl get pods
kubectl get pods --all-namespaces
kubectl get pods -l app=todo-web-application-h2
kubectl get pods -l app=todo-web-application-h2 --all-namespaces
kubectl get services --all-namespaces
kubectl get services --all-namespaces --sort-by=.spec.type
kubectl get services --all-namespaces --sort-by=.metadata.name
kubectl cluster-info
kubectl top node
kubectl top pod

kubectl get services
kubectl get svc
kubectl get ev
kubectl get rs

kubectl get ns
kubectl get nodes
kubectl get no
kubectl get po

docker run --detach --env MYSQL_ROOT_PASSWORD=dummypassword --env MYSQL_USER=todos-user --env MYSQL_PASSWORD=dummytodos --env MYSQL_DATABASE=todos --name mysql --publish 3306:3306 mysql:5.7
docker run -p 8080:8080 sdannarapu/todo-web-application-mysql:0.0.1-SNAPSHOT
docker run -p 8080:8080 --link=mysql --env RDS_HOSTNAME=mysql sdannarapu/todo-web-application-mysql:0.0.1-SNAPSHOT

docker-compose --version
docker-compose up

brew install kompose
kompose convert

kubectl delete all -l app=todo-web-application-h2

kubectl apply -f mysql-database-data-volume-persistentvolumeclaim.yaml,mysql-deployment.yaml,mysql-service.yaml
kubectl get svc
kubectl apply -f todo-web-application-deployment.yaml,todo-web-application-service.yaml
docker push sdannarapu/todo-web-application-mysql:0.0.1-SNAPSHOT
kubectl logs todo-web-application-b65cc44d9-7h9pr -f

kubectl apply -f mysql-service.yaml
kubectl get pv
kubectl get pvc
kubectl describe pod/mysql-5ccbbbdcd8-5zjqg 

kubectl create configmap todo-web-application-config --from-literal=RDS_DB_NAME=todos
kubectl get configmap todo-web-application-config
kubectl describe configmap/todo-web-application-config

kubectl edit configmap/todo-web-application-config
kubectl scale deployment todo-web-application --replicas=0
kubectl scale deployment todo-web-application --replicas=1

kubectl edit configmap/todo-web-application-config
kubectl apply -f todo-web-application-deployment.yaml 
kubectl edit configmap todo-web-application-config
kubectl scale deployment todo-web-application --replicas=0
kubectl scale deployment todo-web-application --replicas=1

kubectl create secret generic todo-web-application-secrets --from-literal=RDS_PASSWORD=dummytodos
kubectl get secret/todo-web-application-secrets
kubectl describe secret/todo-web-application-secrets
kubectl apply -f todo-web-application-deployment.yaml 

kubectl delete -f mysql-database-data-volume-persistentvolumeclaim.yaml,mysql-deployment.yaml,mysql-service.yaml,todo-web-application-deployment.yaml,todo-web-application-service.yaml

apiVersion: v1
data:
  RDS_DB_NAME: todos
  RDS_HOSTNAME: mysql
  RDS_PORT: "3306"
  RDS_USERNAME: todos-user
kind: ConfigMap
metadata:
  name: todo-web-application-config
  namespace: default

cd /kubernetes-workspcae/currency-exchange-microservice-basic 
mvn clean install
docker push sdannarapu/currency-exchange:0.0.1-RELEASE
kubectl apply -f deployment.yaml
curl 34.67.103.178:8000/currency-exchange/from/USD/to/INR

kubectl create configmap currency-conversion --from-literal=YOUR_PROPERTY=value --from-literal=YOUR_PROPERTY_2=value2

kubectl autoscale deployment currency-exchange --min=1 --max=3 --cpu-percent=10 
kubectl get events
kubectl get hpa
kubectl get hpa -o yaml
kubectl get hpa -o yaml > 01-hpa.yaml
kubectl get hpa currency-exchange -o yaml > 01-hpa.yaml

kubectl set image deployment hello-world-rest-api --image=sdannarapu/hello-world-rest-api:0.0.4-SNAPSHOT
kubectl apply -f ingress.yaml
kubectl get ingress
kubectl describe gateway-ingress
kubectl describe gateway gateway-ingress
kubectl describe ingress gateway-ingress
kubectl apply -f rbac.yml
 
docker push sdannarapu/currency-conversion:0.0.5-RELEASE

kubectl create configmap currency-conversion --from-literal=YOUR_PROPERTY=value --from-literal=YOUR_PROPERTY_2=value2

kubectl describe configmap/currency-conversion


kubectl label namespace default istio-injection=enabled

kubectl get svc --namespace istio-system
kubectl apply -f 01-helloworld-deployment.yaml 
kubectl apply -f 02-creating-http-gateway.yaml 
kubectl apply -f 03-creating-virtualservice-external.yaml 
kubectl get svc --namespace istio-system
kubectl get svc istio-ingressgateway --namespace istio-system
kubectl scale deployment hello-world-rest-api --replicas=4
kubectl delete all -l app=hello-world-rest-api
kubectl apply -f 04-helloworld-multiple-deployments.yaml 
kubectl apply -f 05-helloworld-mirroring.yaml 
kubectl apply -f 06-helloworld-canary.yaml 
watch -n 0.1 curl 35.223.25.220/hello-world

gcloud container clusters get-credentials srikanth-cluster-istio --zone us-central1-a --project solid-course-258105
kubectl create namespace istio-system
curl -L https://git.io/getLatestIstio | ISTIO_VERSION=1.2.2 sh -
ls istio-1.2.2
ls istio-1.2.2/install/kubernetes/helm/istio-init/files/crd*yaml
cd istio-1.2.2
for i in install/kubernetes/helm/istio-init/files/crd*yaml; do kubectl apply -f $i; done
helm template install/kubernetes/helm/istio --name istio --set global.mtls.enabled=false --set tracing.enabled=true --set kiali.enabled=true --set grafana.enabled=true --namespace istio-system > istio.yaml
kubectl apply -f istio.yaml
kubectl get pods --namespace istio-system
kubectl get services --namespace istio-system


docker push sdannarapu/currency-exchange:3.0.0-RELEASE
kubectl apply -f deployment.yaml 
kubectl apply -f 11-istio-scripts-and-configuration/07-hw-virtualservice-all-services.yaml 
kubectl get secret -n istio-system kiali
kubectl create secret generic kiali -n istio-system --from-literal=username=admin --from-literal=passphrase=admin
kubectl get svc --namespace istio-system


gcloud container clusters get-credentials helm-cluster --zone us-central1-a --project solid-course-258105
helm init
kubectl get deploy,svc tiller-deploy -n kube-system
clear
unzip 12-helm.zip
ls helm-tiller.sh
chmod +x helm-tiller.sh

gcloud container clusters get-credentials helm-cluster --zone us-central1-a --project solid-course-258105
./helm-tiller.sh
cat helm-tiller.sh 
kubectl get deploy,svc tiller-deploy -n kube-system
helm install ./currency-exchange/ --name=currency-services
helm install ./currency-conversion/ --name=currency-services-1
helm install ./currency-conversion/ --name=currency-services-3 --debug --dry-run
helm history currency-services-1
helm upgrade currency-services-1 ./currency-conversion/
helm rollback currency-services-1 1
helm upgrade currency-services-1 ./currency-conversion/ --debug --dry-run
helm upgrade currency-services-1 ./currency-conversion/
helm history currency-services-1

```
## Notes

- Assume replicas = 200 maxUnavailable = 20% maxSurge = 20%. Max pods that can be unavailable during release = 20%(maxUnavailable) * 200 = 40. Max pods used during release = 200 + 20%(maxSurge) * 200 = 240
- updateMode: "Auto"
- Step 1 : Install all the Istio Custom Resource Definitions (CRD)
- Step 2 : Install Istio with Components for graphana, prometheus, tracing(jaeger), kiali as subcharts using Helm Charts.
- Fun Fact : istio.yaml has 18,000 lines of configuration!
- Step 3 : Verify Intallation of Istio
- Step 4 : Enable Adding Istio Side Cars in each Pod

## Diagrams

- Courtesy http://viz-js.com/

```
graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = TB
node[shape=record, width=2]
Level1[shape=record, width=7.0, style=filled,color="#D14D28", fontcolor=white]
edge [width=0]
graph [pad=".75", ranksep="0.05", nodesep="0.25"];
Block1,Block2,Block3[height=2]

Block1 -- Level1 [style=invis]
Block2 -- Level1 [style=invis]
Block3 -- Level1 [style=invis]

Level1[label=<Kubernetes>]
Block1[label=<Container Orchestration <BR/><BR/><BR/><BR/> <FONT POINT-SIZE="10">Manage 1000's of instances<BR/>1000's of microservices<BR/>Declaratively</FONT>>]
Block2[label=<Features <BR/><BR/> <FONT POINT-SIZE="10">Auto Scaling<BR/> Service Discovery <BR/> Load Balancing <BR/> Self Healing <BR/> Zero Downtime Deployments </FONT> 
>]
Block3[label=<Cloud Neutral <BR/><BR/><BR/><BR/><FONT POINT-SIZE="10">Standardized Platform <BR/> on any infrastructure</FONT>>]

}

graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = TB
node[shape=record, width=2]
Level1[shape=record, width=7.0, style=filled,color="#D14D28", fontcolor=white]
edge [width=0]
graph [pad=".75", ranksep="0.05", nodesep="0.25"];
Block1,Block2,Block3[height=2]

Block1 -- Level1 [style=invis]
Block2 -- Level1 [style=invis]
Block3 -- Level1 [style=invis]

Level1[label=<Docker>]
Block1[label=<Standaridized <BR/> Application Packaging <BR/><BR/><BR/> <FONT POINT-SIZE="10">Same packaging for <BR/>all types of applications</FONT>>]
Block2[label=<Features <BR/> <FONT POINT-SIZE="10">Language Neutral<BR/>  Cloud Neutral <BR/> Enables Standardization </FONT> 
>]
Block3[label=<Challenges <BR/><BR/><FONT POINT-SIZE="10"> 1000 Microservices<BR/> 1000 Instances</FONT>>]

}


graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = TB
node[shape=record, width=2, height=2]
Block11, Block12[width=1,height=1]
Block21, Block22[width=1,height=1]
Level1[shape=record, width=10, style=filled,color="#D14D28", fontcolor=white]
edge [width=0]
graph [pad=".75", ranksep="0.05", nodesep="0.25"];
Block1,Block2[ width=4.8]

Block1 -- Level1 [style=invis]
Block2 -- Level1 [style=invis]

Block11 -- Block1 [style=invis]
Block12 -- Block1 [style=invis]

Block21 -- Block2 [style=invis]
Block22 -- Block2 [style=invis]


Level1[label=<Deployment>]
Block1[label=<Replica Set 1 >]
Block2[label=<Replica Set 2 >]
Block11[label=<Pod Instance 1>]
Block12[label=<Pod Instance 2>]
Block21[label=<Pod Instance 1>]
Block22[label=<Pod Instance 2>]

}

graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = TB
node[shape=record, width=2]
Level1[shape=record, width=4.5, style=filled,color="#D14D28", fontcolor=white]
edge [width=0]
graph [pad=".75", ranksep="0.05", nodesep="0.25"];
Block1,Block2[height=2]

Block1 -- Level1 [style=invis]
Block2 -- Level1 [style=invis]

Level1[label=<Cluster>]
Block1[label=<Master Node(s) <BR/> <FONT POINT-SIZE="10">Manages Cluster</FONT>>]
Block2[label=<Worker Node(s) <BR/> <FONT POINT-SIZE="10">Run Your Applications</FONT>>]

}

graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = TB
node[shape=record, width=2, height=2]
Block11, Block12[width=1,height=1]
Block21, Block22[width=1,height=1]
Level1[shape=record, width=10, style=filled,color="#D14D28", fontcolor=white]
edge [width=0]
graph [pad=".75", ranksep="0.05", nodesep="0.25"];
Block1,Block2[ width=4.8]

Block1 -- Level1 [style=invis]
Block2 -- Level1 [style=invis]

Block11 -- Block1 [style=invis]
Block12 -- Block1 [style=invis]

Block21 -- Block2 [style=invis]
Block22 -- Block2 [style=invis]


Level1[label=<Node>]
Block1[label=<Pod 1 >]
Block2[label=<Pod 2 >]
Block11[label=<Container 1>]
Block12[label=<Container 2>]
Block21[label=<Container 3>]
Block22[label=<Container 4>]

}

graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = TB
node[shape=record, width=2]
Level1[shape=record, width=9.0, style=filled,color="#D14D28", fontcolor=white]
edge [width=0]
graph [pad=".75", ranksep="0.05", nodesep="0.25"];
Block1,Block2,Block3,Block4[height=2]

Block1 -- Level1 [style=invis]
Block2 -- Level1 [style=invis]
Block3 -- Level1 [style=invis]
Block4 -- Level1 [style=invis]

Level1[label=<Master Node>]
Block1[label=<API Server <BR/> <FONT POINT-SIZE="10">(kube-apiserver)</FONT>>]
Block2[label=<Distribute Database <BR/> <FONT POINT-SIZE="10">(etcd)</FONT>>]
Block3[label=<Scheduler  <BR/> <FONT POINT-SIZE="10">(kube-scheduler)</FONT>>]
Block4[label=<Controller Manager  <BR/> <FONT POINT-SIZE="10">(kube-controller-manager)</FONT>>]

}

graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = TB
node[shape=record, width=2]
Level1[shape=record, width=9.0, style=filled,color="#D14D28", fontcolor=white]
edge [width=0]
graph [pad=".75", ranksep="0.05", nodesep="0.25"];
Block1,Block2,Block3,Block4[height=2]

Block1 -- Level1 [style=invis]
Block2 -- Level1 [style=invis]
Block3 -- Level1 [style=invis]
Block4 -- Level1 [style=invis]

Level1[label=<Worker Node (or) Node>]
Block1[label=<Node Agent <BR/> <FONT POINT-SIZE="10">(kubelet)</FONT>>]
Block2[label=<Networking Component <BR/> <FONT POINT-SIZE="10">(kube-proxy)</FONT>>]
Block3[label=<Container Runtime  <BR/> <FONT POINT-SIZE="10">(CRI - docker, rkt etc)</FONT>>]
Block4[label=<PODS  <BR/> <FONT POINT-SIZE="10">(Multiple pods running <BR/> containers)</FONT>>]

}



graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = LR
node[shape=record, width=3]


ParentNode -- ChildNode1
ParentNode -- ChildNode2
ParentNode -- ChildNode3
ParentNode -- ChildNode4

ParentNode[label=<Master Node>]
ChildNode1[label=<API Server>];
ChildNode2[label=<Distributed Database - etcd>];
ChildNode3[label=<Scheduler>];
ChildNode4[label=<Controller Manager>];

}

graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = LR
node[shape=record, width=3]


ParentNode -- ChildNode1
ParentNode -- ChildNode2
ParentNode -- ChildNode3
ParentNode -- ChildNode4

ParentNode[label=<Worker Node (or) Node>]
ChildNode1[label=<Kubelet>];
ChildNode2[label=<Kube Proxy>];
ChildNode3[label=<Container Runtime>];
ChildNode4[label=<Pods>];

}


graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = LR
node[shape=record, width=1.6]


ParentNode1 -- ChildNode1
ParentNode2 -- ChildNode1
ChildNode1 -- ChildNode2

ParentNode1[label=<User>]
ParentNode2[label=<Service Consumer>]
ChildNode1[label=<Service>];
ChildNode2[label=<Pod>];

}

graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = TB
node[shape=record, width=2]


ParentNode1 -- ChildNode1
ChildNode1 -- Level2Child1
ChildNode1 -- Level2Child2
ParentNode1 -- ChildNode2
ChildNode2 -- Level2Child3
ChildNode2 -- Level2Child4

ParentNode1[label=<Node>]
ChildNode1[label=<Pod 1>]
Level2Child1[label=<Container 1>]
Level2Child2[label=<Container 2>]

ChildNode2[label=<Pod 2>]
Level2Child3[label=<Container 3>]
Level2Child4[label=<Container 4>]
}

graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = LR
node[shape=record, width=2]


Node1 -- Node2
Node2 -- Node3

Node1[label=<Project Code>]
Node2[label=<Docker Image>]
Node3[label=<Docker Repository>]
}

graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = LR
node[shape=record, width=2]


Node1 -- Node2
Node2 -- Node3
Node2 -- Node4

Node1[label=<Istio Gateway>]
Node2[label=<Istio Virtual Service <BR/> <FONT POINT-SIZE="10">Configure Routes</FONT>>]
Node3[label=<K8S Service A>]
Node4[label=<K8S Service B>]
}

graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = LR
node[shape=record, width=2]


Node1 -- Node3
Node3 -- Node2
Node2 -- Node4
Node2 -- Node5

Node1[label=<Istio Gateway>]
Node3[label=<Istio Virtual Service <BR/> <FONT POINT-SIZE="10">Configure routes to Services<BR/>Configure weights for Subsets</FONT>>]
Node2[label=<Destination Rule<BR/> <FONT POINT-SIZE="10">Map to different <BR/> Service Versions</FONT>>]
Node4[label=<K8S Service A V1>]
Node5[label=<K8S Service A V2>]
}

graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = LR
node[shape=record, width=2]


Node1 -- Node2
Node2 -- Node3

Node1[label=<Create Cluster>]
Node2[label=<Create Deployment>]
Node3[label=<Docker Repository>]
}

graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = TB
node[shape=record, width=3]

Clusters, LocalImages [height=1]

KubernetesClient -- Daemon
Daemon -- Clusters 
Daemon -- LocalImages
Daemon -- ImageRegistry

KubernetesClient[label=<Kubernetes Client>]
ImageRegistry[label=<Image Registry <BR /><FONT POINT-SIZE="10">nginx<BR />mysql<BR />eureka<BR />your-app<BR /><BR /></FONT>>];
Daemon[label=<Kubernetes Daemon>]


}


graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = TB
node[shape=record, width=2]
Hypervisor,HostOS, Hardware[shape=record, width=6.5, style=filled,color="#D14D28", fontcolor=white]
edge [width=0]
graph [pad=".75", ranksep="0.05", nodesep="0.25"];

Application1 -- Software1 [style=invis]
Application2 -- Software2 [style=invis]
Application3 -- Software3 [style=invis]

Software1 -- GuestOS1 [style=invis]
Software2 -- GuestOS2 [style=invis]
Software3 -- GuestOS3 [style=invis]
GuestOS1 -- Hypervisor [style=invis]
GuestOS2 -- Hypervisor [style=invis]
GuestOS3 -- Hypervisor [style=invis]
Hypervisor -- HostOS [style=invis]
HostOS -- Hardware [style=invis]

}


graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = TB
node[shape=record, width=2]
HostOS, CloudInfrastructure, KubernetesEngine[shape=record, width=6.5, style=filled,color="#D14D28", fontcolor=white]
edge [width=0]
graph [pad=".75", ranksep="0.05", nodesep="0.25"];
Container1,Container2,Container3[height=2]

Container1 -- KubernetesEngine [style=invis]
Container2 -- KubernetesEngine [style=invis]
Container3 -- KubernetesEngine [style=invis]
KubernetesEngine -- HostOS [style=invis]
HostOS -- CloudInfrastructure [style=invis]

}
```