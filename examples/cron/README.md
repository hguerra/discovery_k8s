Como executar cron jobs no Kubernetes?

https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/

https://komodor.com/learn/kubernetes-cronjobs/

https://nieldw.medium.com/using-a-kubernetes-cronjob-the-team-city-api-to-trigger-a-regular-backup-17dfb076d83a

```
kubectl apply -f examples/cron/cronjob.yaml

kubectl get pods -n development

kubectl get jobs -n development

kubectl logs -f jobs/cron-job-28094500 -n development

kubectl get jobs -n development --watch
```


Removendo os recursos criados:
```
kubectl delete -f courses/linkedin/learning-kubernetes-16086900/04/cronjob.yaml
```
