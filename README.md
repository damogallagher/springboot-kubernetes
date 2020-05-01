# Build application
```
.mvnw install
```

# Run application
```
java -jar target/demo-0.0.1-SNAPSHOT.jar
```

# Build container image
```
docker build -t damogallagher/demo .
```

# Run container locally
```
docker run -p 8080:8080 damogallagher/demo
```

# Push image to dockerhub
```
docker login
docker push damogallagher/demo
```


# Create kubernetes deployment and service yaml files
```
mkdir k8s
kubectl create deployment demo --image=damogallagher/demo --dry-run -o=yaml > k8s/deployment.yaml
echo --- >> k8s/deployment.yaml
kubectl create service clusterip demo --tcp=8080:8080 --dry-run -o=yaml >> k8s/deployment.yaml
```

# Run on kubernetes
```
cd k8s
kubectl apply -f .
```

# Check service and deployment are running on kubernetes
```
kubectl get all
```

# Test locally using an SSH tunnel
```
kubectl port-forward svc/demo 8080:8080
```

# Verify app is running on kubernetes
```
curl localhost:8080/actuator/health
```