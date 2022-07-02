### spring boot with kubernetes

Containerize the Application

```bash
./mvnw spring-boot:build-image
```

Run the image locally:

```bash
docker run -p 8080:8080 demo:0.0.1-SNAPSHOT
```

Then you can check that it works in another terminal:

```bash
curl localhost:8080/actuator/health
```

Tag and push the image

```bash
docker tag demo:0.0.1-SNAPSHOT springguides/demo
```

```bash
docker push springguides/demo
```

### Deploy the Application to Kubernetes

create deployment

```bash
kubectl create deployment demo --image=springguides/demo --dry-run -o=yaml > deployment.yaml
```

create service


```bash
kubectl create service clusterip demo --tcp=8080:8080 --dry-run -o=yaml >> deployment.yaml
```

apply deployment

```bash
kubectl apply -f deployment.yaml
```