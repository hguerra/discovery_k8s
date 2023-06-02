Criar um serviço para distribuir as requisições para os deployments. Os tipos de serviço são:

* ClusterIP

* NodePort

* LoadBalancer

* ExternalName

https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types


Nos provedores cloud, quando o tipo é LoadBalancer, é criado um serviço gerenciado de LoadBalancer com IP Externo.
Por padrão, os serviços do Kubernetes são privados (internos do cluster).

```
kubectl apply -f courses/linkedin/learning-kubernetes-16086900/03/namespace.yaml

kubectl get ns

kubectl apply -f courses/linkedin/learning-kubernetes-16086900/04/deployment.yaml

kubectl get pods -n development

kubectl apply -f courses/linkedin/learning-kubernetes-16086900/04/service.yaml

kubectl get services -n development

kubectl get svc -n development

kubectl describe svc demo-service -n development

kubectl get svc/demo-service -n development
```


Expor o serviço via Ingress:

O Ingress é recurso utilizado para direcionar requisições externas para dentro do cluster. O Ingress serve como um único
ponto de entrada para o cluster.

While ingresses and load balancers have a lot of overlap in functionality, they behave differently. The main difference is ingresses are native objects inside the cluster that can route to multiple services, while load balancers are external to the cluster and only route to a single service.

The cluster must be running on a provider that supports external load balancers. Using an external load balancer will typically come with additional costs. This is because, unlike ingresses and their controllers, external load balancers exist outside of the Kubernetes cluster. Because of this, most cloud providers will charge for the additional resource usage beyond the cluster itself.

https://kubernetes.io/docs/concepts/services-networking/ingress/

https://www.baeldung.com/ops/kubernetes-ingress-vs-load-balancer

https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/

https://kind.sigs.k8s.io/docs/user/ingress/#ingress-nginx


```
kubectl get pods -n ingress-nginx

kubectl get svc -n ingress-nginx

kubectl apply -f courses/linkedin/learning-kubernetes-16086900/04/service.yaml

kubectl get svc -n development

kubectl get svc -n ingress-nginx

kubectl logs -f svc/demo-service -n development
kubectl logs -f svc/ingress-nginx-controller -n ingress-nginx
```


Validar se um Pod esta pronto para receber requisições:

https://komodor.com/learn/kubernetes-readiness-probes-a-practical-guide

https://spacelift.io/blog/kubernetes-liveness-probe

https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes



Como executar cron jobs no Kubernetes?

https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/

https://komodor.com/learn/kubernetes-cronjobs/

https://nieldw.medium.com/using-a-kubernetes-cronjob-the-team-city-api-to-trigger-a-regular-backup-17dfb076d83a

```
kubectl apply -f courses/linkedin/learning-kubernetes-16086900/04/cronjob.yaml

kubectl get pods -n development

kubectl get jobs -n development

kubectl logs -f jobs/cron-job-28094500 -n development

kubectl get jobs -n development --watch
```


Como expor os serviços no GKE:

https://cloud.google.com/kubernetes-engine/docs/how-to/exposing-apps?hl=pt-br

https://cloud.google.com/kubernetes-engine/docs/tutorials/http-balancer?hl=pt-br

https://cloud.google.com/blog/products/containers-kubernetes/exposing-services-on-gke

https://learnk8s.io/terraform-gke


Removendo os recursos criados:
```
kubectl delete -f courses/linkedin/learning-kubernetes-16086900/04/cronjob.yaml

kubectl delete -f courses/linkedin/learning-kubernetes-16086900/04/service.yaml

kubectl delete -f courses/linkedin/learning-kubernetes-16086900/04/deployment.yaml
```
