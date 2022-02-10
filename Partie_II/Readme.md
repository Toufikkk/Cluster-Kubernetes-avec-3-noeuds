# How to start the project

Create the cluster with  
`kind create cluster --config kind_config/config.yaml`

To check the created cluster  
`kind get clusters`

To check the nodes  
`kubectl get nodes` --> Show nodes informations (`-o wide` for more information)

To create volumes  
`kubectl apply -f volumes/dolibarr-conf-persistentvolumeclaim.yaml`  
`kubectl apply -f volumes/dolibarr-docs-persistentvolumeclaim.yaml`  
`kubectl apply -f volumes/mariadb-persistentvolumeclaim.yaml`

To create deployments  
`kubectl apply -f deployments/dolibarr-deployment.yaml`  
`kubectl apply -f deployments/mariadb-deployment.yaml`

To create services  
`kubectl apply -f services/dolibarr-service.yaml`  
`kubectl apply -f services/mariadb-service.yaml`

To check the deployments  
`kubectl get deployments`

To check the volumes  
`kubectl get pvc`

To check the services  
`kubectl get svc`

To check the pods  
`kubectl get pods` --> Show the pods informations (`-o` wide for more information)

To access the app  
`kubectl port-forward (pod_name) 1234:80`  

To destroy a pod  
`kubectl delete pod (pod_name)`

Check pod got renewed  
`kubectl get pods` --> Look at pod "AGE" and you will be able to see the new pod just go created
