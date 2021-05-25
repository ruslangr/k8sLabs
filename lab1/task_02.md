# Kubernetes resourceas introduction
```bash
kubectl run web --image=nginx:latest
```
- take a look at created resource in cmd "kubectl get pods"
- take a look at created resource in Dashboard
- take a look at created resource in cmd
```bash
minikube ssh
docker container ls
```

## [Specification](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.18/)
```bash
kubectl explain pods.spec
```

## Create yaml manifest

Create manifest for Pod
```bash
cat > pod.yaml <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - image: nginx:latest
    name: nginx
EOF
```

Create manifest for ReplicaSet
```bash
cat > rs.yaml <<EOF
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  labels:
    app: webreplica
  name: webreplica
spec:
  replicas: 1
  selector:
    matchLabels:
      app: webreplica
  template:
    metadata:
      labels:
        app: webreplica
    spec:
      containers:
      - image: nginx:latest
        name: nginx
EOF
```

Apply manifests
```bash
kubectl apply -f pod.yaml
kubectl apply -f rs.yaml
```

```bash
kubectl run web --image=nginx:latest --dry-run=client -o yaml
```
