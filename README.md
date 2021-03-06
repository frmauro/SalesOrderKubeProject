# SalesOrderKubeProject

## command kubernate (minikube) - Pass to docker of Minikube (create an image into current terminal)
eval $(minikube docker-env)

## command kubernate (minikube) - Return to docker local machine
eval $(minikube docker-env -u)

kubectl delete svc salesapiuser -n salesorder
kubectl delete deploy salesapiuser -n salesorder
kubectl logs salesapiuser-769d9fd564-56pc6 -n salesorder

kubectl create -f ingress/productapi-ingress.yaml -n salesorder

kubectl exec productdb-787d69f988-5swkt  -n salesorder -it -- /bin/bash
kubectl exec productdb-59f8665ffb-2rj85  -n salesorder -it -- /bin/bash

kubectl create secret generic mssql --from-literal=SA_PASSWORD="Mau123&&&"
kubectl create secret generic mssql --from-literal=SA_PASSWORD="Mau123&&&" -n salesorder
minikube dashboard

kubectl apply -f persistent/pvclaim.yaml
kubectl apply -f persistent/pvclaim.yaml -n salesorder
kubectl describe pvc pvclaim

kubectl apply -f secrets/mysql-secret.yaml -n salesorder
kubectl delete secrets mysql-login -n salesorder

kubectl create secret generic mysql-root-pass --from-literal=password=admin -n salesorder
kubectl create secret generic mysql-user-pass --from-literal=username=teste@localhost --from-literal=password=admin -n salesorder
kubectl create secret generic mysql-db-url --from-literal=database=polls --from-literal=url='jdbc:mysql://orderdb:3306/orderapi' -n salesorder

kubectl get secrets -n salesorder



kubectl apply -f services/salesproductfrontend.yaml -n salesorder
kubectl apply -f deployments/salesproductfrontend.yaml -n salesorder
kubectl delete deploy productfrontend  -n salesorder
kubectl delete svc productfrontend  -n salesorder
kubectl create -f ingress/salesorder-ingress.yaml -n salesorder
kubectl delete ingress salesorder-ingress -n salesorder



## By default, secrets have to be base64 encoded first. So, let’s generate those base64 strings first:
echo -n "dbuser" | base64
echo -n "admin" | base64
echo -n "orderapi" | base64

## command for iterate with mysql  
echo $MYSQL_ROOT_PASSWORD
admin
root@k8s-mysql:/# mysql --user=root --password=$MYSQL_ROOT_PASSWORD



## content reverse-proxy.conf file of NGINX (Ubunto Linux) in PATH: /etc/nginx/sites-availables
## the routes below are for the minikube ingress local cluster in Linux Ubunto

server {
        listen 80;
        listen [::]:80;

        access_log /var/log/nginx/reverse-access.log;
        error_log /var/log/nginx/reverse-error.log;

        location /getAllProduct {
                  proxy_pass http://salesorder.com/getAllProduct;
        }
        location /CreateProduct {
                  proxy_pass http://salesorder.com/CreateProduct;
        }
        location /UpdateProduct {
                  proxy_pass http://salesorder.com/UpdateProduct;
        }
        location /users {
                  proxy_pass http://salesorder.com/users;
        }
        location /UpdateUser {
                  proxy_pass http://salesorder.com/UpdateUser;
        }
        location /CreateUser {
                  proxy_pass http://salesorder.com/CreateUser;
        }
        location /GetAllOrders {
                  proxy_pass http://salesorder.com/GetAllOrders;
        }
        location /FindUserByEmailAndPassword {
                  proxy_pass http://salesorder.com/FindUserByEmailAndPassword;
        }
        location /getOrderByUserId {
                  proxy_pass http://salesorder.com/getOrderByUserId;
        }
        location /CreateOrder {
                  proxy_pass http://salesorder.com/CreateOrder;
        }
        location /UpdateOrder {
                  proxy_pass http://salesorder.com/UpdateOrder;
        }
        location /UpdateAmount {
                  proxy_pass http://salesorder.com/UpdateAmount;
        }


}


