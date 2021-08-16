# SalesOrderKubeProject

## command kubernate (minikube) - Pass to docker of Minikube (create an image into current terminal)
eval $(minikube docker-env)

## command kubernate (minikube) - Return to docker local machine
eval $(minikube docker-env -u)

kubectl delete svc salesapiuser -n salesorder
kubectl delete deploy salesapiuser -n salesorder
kubectl logs salesapiuser-769d9fd564-56pc6 -n salesorder

