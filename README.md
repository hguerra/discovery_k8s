# Discovery K8S

## Install

https://kind.sigs.k8s.io/docs/user/quick-start/#installing-from-release-binaries

```
go install github.com/go-task/task/v3/cmd/task@v3.25.0

[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.19.0/kind-linux-amd64

chmod +x ./kind

sudo mv ./kind /usr/local/bin/kind
```


## Creating a Cluster

https://kind.sigs.k8s.io/docs/user/quick-start/#configuring-your-kind-cluster

https://kind.sigs.k8s.io/docs/user/ingress/#using-ingress

```
task create_cluster
```


### Example

```
kubectl apply -f ./kind/usage.yaml

kubectl get pods

# should output "foo-app"
curl localhost/foo/hostname

# should output "bar-app"
curl localhost/bar/hostname

kubectl delete -f ./kind/usage.yaml
```


## Deleting a Cluster

https://kind.sigs.k8s.io/docs/user/quick-start/#deleting-a-cluster

```
task delete_cluster
```
