Listar namespaces padrões do Kubernetes:
```
kubectl get namespaces

kubectl get ns
```


Criar um novo namespace:
```
kubectl apply -f namespace.yaml
```


Remover os namespaces criados:
```
kubectl delete -f namespace.yaml
```


Criar um deployment:
```
kubectl apply -f deployment.yaml
```


Listar todos os deployments de um namespace:
```
kubectl get deployments -n development
```


Listar todos os os pods criados:
```
kubectl get pods -n development
```


Deletar um pod pelo nome:
```
kubectl delete pod pod-info-deployment-869667679b-5gqg6 -n development
```


Exibir informações de um pod pelo nome:
```
kubectl describe pod pod-info-deployment-869667679b-bxj2w -n development
```

Fazer uma requisição dentro da rede interna do Kubernetes:
```
kubectl apply -f busybox.yaml

kubectl get pods

# listar os pods com ip
kubectl get pods -n development -o wide

# executar um comando para acesso o shell do container
kubectl exec -it busybox-55fdb79844-bjljt -- /bin/sh

# dentro do container busybox, realizar a request:
wget 10.244.0.17:3000
cat index.html
exit
```


Exibir logs de um pod:
```
kubectl get pods -n development

kubectl logs pod-info-deployment-869667679b-bxj2w -n development

kubectl logs -f pod-info-deployment-869667679b-bxj2w -n development
```


Desafio:
```
kubectl apply -f quote.yaml

kubectl get pods -n development -o wide

kubectl exec -it busybox-55fdb79844-bjljt -- /bin/sh

wget 10.244.0.22:8080
cat index.html
exit

kubectl delete -f quote.yaml

kubectl delete -f busybox.yaml
```


Remover o deployment:
```
kubectl delete -f deployment.yaml
```
