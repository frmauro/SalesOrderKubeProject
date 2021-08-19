# SalesOrderKubeProject

## command kubernate (minikube) - Pass to docker of Minikube (create an image into current terminal)
eval $(minikube docker-env)

## command kubernate (minikube) - Return to docker local machine
eval $(minikube docker-env -u)

kubectl delete svc salesapiuser -n salesorder
kubectl delete deploy salesapiuser -n salesorder
kubectl logs salesapiuser-769d9fd564-56pc6 -n salesorder

kubectl exec productdb-787d69f988-5swkt  -n salesorder -it -- /bin/bash
kubectl exec productdb-59f8665ffb-2rj85  -n salesorder -it -- /bin/bash

kubectl create secret generic mssql --from-literal=SA_PASSWORD="Mau123&&&"
kubectl create secret generic mssql --from-literal=SA_PASSWORD="Mau123&&&" -n salesorder
minikube dashboard

kubectl apply -f persistent/pvclaim.yaml
kubectl apply -f persistent/pvclaim.yaml -n salesorder
kubectl describe pvc pvclaim
