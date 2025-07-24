### install minikube

`brew update`

`brew install minikube`

`kubectl`

`minikube`

### create minikube cluster

`minikube start --driver=docker`

`kubectl get nodes`

`minikube status`

`kubectl version`

### delete cluster and restart in debug mode

`minikube delete`

`minikube start --driver=docker --v=7 --alsologtostderr`

`minikube status`

### kubectl commands

`kubectl get all` --> Gets all the components that are inside the cluster

`kubectl get nodes`

`kubectl get pod --watch` --> watch flag optional

`kubectl get pod -o wide` --> with more information

`kubectl get services` --> or kubectl get svc

`kubectl get secret`

`kubectl create deployment nginx-depl --image=nginx`

`kubectl get deployment`

`kubectl get deployment nginx-deployment -o yaml`
Gets the configuration of the deployment which resides in the etcd. This is to check the status of the deployment

`kubectl get replicaset`

`kubectl edit deployment nginx-depl`

### debugging

`kubectl logs {pod-name}`

`kubectl describe pod {pod-name}`

`kubectl exec -it {pod-name} -- bin/bash`
It allows you to run commands inside the pod's container (indirective terminal access).

### create mongo deployment

`kubectl create deployment mongo-depl --image=mongo`

Get logs to console inside the pod
`kubectl logs mongo-depl-{pod-name}`

Get info about the pod
`kubectl describe pod mongo-depl-{pod-name}`

Get interactive terminal inside the pod
`kubectl exec -it {pod-name} -- bin/bash`

### delete deployment

`kubectl delete pod {pod-name}`
If i delete a pod, it will be recreated if it's managed by a deployment

`kubectl delete deployment mongo-depl`

`kubectl delete deployment nginx-depl`

### create or edit config file

`vim nginx-deployment.yaml`

`kubectl apply -f nginx-deployment.yaml`
It creates or updates a component. It can create/update services/volumes

`kubectl get pod`

`kubectl get deployment`

### delete with config

`kubectl delete -f nginx-deployment.yaml`

#Metrics

`kubectl top` The kubectl top command returns current CPU and memory usage for a cluster’s pods or nodes, or for a particular pod or node if specified.

### describe a service

`kubectl describe service nginx-service`
It says where this service is connected to (in what deployment)

### creating secrets

They need to be in base64 format

`echo -n 'username' | base64`

### assigning public IP to external service

`minikube service mongo-express-service`

### namespaces

`kubectl get namespaces`

`kubectl create namespace my-namespace`
Or i can create it with a namespace configuration file
