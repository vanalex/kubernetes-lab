# Creating Nginx Pod using Pod Manifest File

In our last workshop, we created a Pod directly using kubectl. Under this section, we will use Pod manifest file instead. We will see how to expose nginx pod to port 8080.

```
kubectl create -f nginx-pod.yaml
```

Check pods, services and deployments

```
kubectl get po,svc,deploy
```

Describe the pod

```
kubectl describe po nginx-pod
```

Get the pod list

```
kubectl get pods
```

Create a deployment
```
kubectl create -f nginx-deployment.yaml 
```

Verify that the pod came up

```
kubectl -n default port-forward $(kubectl -n default get pod -l name=nginx-pod -o jsonpath='{.items[0].metadata.name}') 8080:80 & open http://localhost:8080/
```