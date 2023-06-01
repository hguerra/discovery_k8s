run:
	kubectl apply -f pod-api-label.json
	kubectl describe pod api-pod
	kubectl apply -f pod-api-service.json
	kubectl describe service pod-api-svc
	kubectl get nodes -o wide
	# kubectl port-forward service/mongo 28015:27017

# filtrar usando labels
pod-get:
	kubectl get pod -l "app=simple-api,version=1.0.0"

create-ingress-cluster:
	kind create cluster --config ingress-cluster.yaml
	kubectl cluster-info --context kind-ingress-cluster
	kubectl config get-contexts
	kubectl config use-context kind-ingress-cluster
	kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
	kubectl wait --namespace ingress-nginx --for=condition=ready pod --selector=app.kubernetes.io/component=controller --timeout=90s

test-ingress-cluster:
	kubectl apply -f ingress-sample.yaml
	curl localhost/foo
	curl localhost/bar

