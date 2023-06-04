Como configurar Horizontal Pod Autoscaling (HPA)?

Horizontal scaling means that the response to increased load is to deploy more Pods. This is different from vertical scaling, which for Kubernetes would mean assigning more resources (for example: memory or CPU) to the Pods that are already running for the workload.

If the load decreases, and the number of Pods is above the configured minimum, the HorizontalPodAutoscaler instructs the workload resource (the Deployment, StatefulSet, or other similar resource) to scale back down.

https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/

https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/

https://cloud.google.com/kubernetes-engine/docs/how-to/horizontal-pod-autoscaling?hl=pt-br

https://www.kubecost.com/kubernetes-autoscaling/kubernetes-hpa/

https://aptakube.com/blog/how-to-fix-failedgeteesourcemetric-hpa

https://kubernetes-sigs.github.io/metrics-server/

https://gist.github.com/sanketsudake/a089e691286bf2189bfedf295222bd43

https://www.dbi-services.com/blog/kubernetes-deployment-autoscaling-using-memory-cpu/


Como mapear serviços externos?

https://www.googblogs.com/kubernetes-best-practices-mapping-external-services/

https://www.sobyte.net/post/2022-04/kubernetes-ext-service/

https://faun.pub/kubernetes-mapping-external-services-b8f49c35be7e

https://faun.pub/route-to-external-domains-using-kubernetes-services-df58472fb246


Exemplo:

```
kubectl apply -f examples/hpa/namespace.yaml

kubectl apply -f examples/hpa/external-service.yaml

kubectl apply -f examples/hpa/service.yaml

kubectl apply -f examples/hpa/ingress.yaml

kubectl get events -n development

kubectl get svc -n development

kubectl get pods -n development

kubectl top pods -n development --containers

kubectl logs -f pod-info-deployment-587f5b7d8d-w2x7p -n development

kubectl logs -f svc/ingress-nginx-controller -n ingress-nginx

kubectl get hpa -n development -w

kubectl get pods -n development -w

curl --connect-timeout 5 --max-time 60 --no-keepalive -i -X GET 'http://localhost'

curl --connect-timeout 5 --max-time 60 --no-keepalive -i -X GET 'http://servicos.cptec.inpe.br/XML/cidade/4963/previsao.xml'

curl --connect-timeout 5 --max-time 60 --no-keepalive -i -X GET 'http://localhost/XML/cidade/4963/previsao.xml'
```


Testar aumento de carga:

<service-name>.<namespace>.svc.cluster.local:<service-port>

```
kubectl run -i --tty load-generator --rm --image=busybox --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://pod-info-service.development.svc.cluster.local:80; done"
```


Remover recursos criados:

```
kubectl delete pod/load-generator

kubectl delete -f examples/hpa/ingress.yaml

kubectl delete -f examples/hpa/external-service.yaml

kubectl delete -f examples/hpa/service.yaml

kubectl delete -f examples/hpa/namespace.yaml
```
