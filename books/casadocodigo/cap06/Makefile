run:
	kubectl create -f pod.json


delete:
	# kubectl delete pod mongodb-pod
	kubectl delete -f pod.json

get-pods:
	kubectl get pods

pod-logs:
	kubectl logs mongodb-pod

pod-exec:
	kubectl exec -it mongodb-pod mongo
	# db.collectionExemplo.insert({nome: 'K8S é demais!'});
	# db.collectionExemplo.find()
