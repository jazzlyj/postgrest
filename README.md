# PV, Postgres, Postgrest API, Pgadmin, Swagger UI



### Start
```powershell
minikube start
```



# Setup
kubectl apply -f db-service.yaml
kubectl apply -f pgadmin-data-persistentvolumeclaim.yaml
kubectl apply -f pgadmin-deployment.yaml
kubectl apply -f pgadmin-service.yaml
kubectl apply -f server-deployment.yaml
kubectl apply -f server-service.yaml
kubectl apply -f swagger-deployment.yaml
kubectl apply -f swagger-service.yaml

* setup port forwarding 
kubectl port-forward service/pgadmin 5050:5050
kubectl port-forward service/server 3000:3000
kubectl port-forward service/swagger 8080:8080





### K8s Ingress
A reverse proxy that enables external access into other Kubernetes resources.

* Install ingress controller
```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.5.1/deploy/static/provider/do/deploy.yaml
```

* Confirm the pods have started:
```
kubectl get pods -n ingress-nginx -l app.kubernetes.io/name=ingress-nginx --watch
```

* Confirm that the Load Balancer was successfully created
```
kubectl get svc --namespace=ingress-nginx
```

* Deploy ingress
```bash
kubectl apply -f ingress.yaml
```

https://github.com/kubernetes/ingress-nginx








* Unless deploying to DNS use /etc/hosts
```bash
vim /etc/hosts
# add an entry for our domain name
127.0.0.1 localhost
```



# Once built - Run these on subsequent starts



```
minikube start
# port forwarding for pgadmin deployment/service/ http://localhost:5050/ to work 
kubectl port-forward service/pgadmin 5050:5050
# to start the minikube dashboard in browser
minikube dashboard
```

command history
```
kubectl get service --namespace kube-system

```



















## K8s clean up
```bash
kubectl delete all --all
```


