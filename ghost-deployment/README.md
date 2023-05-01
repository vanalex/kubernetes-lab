## Deploy an app with 2 commands

$ kubectl run ghost --image=ghost:0.9
$ kubectl expose deployments ghost --port=2368 --type=NodePort
$ minikube dashboard