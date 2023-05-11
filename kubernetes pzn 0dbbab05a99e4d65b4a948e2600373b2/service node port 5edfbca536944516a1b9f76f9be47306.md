# service node port

Service NodePort pada Kubernetes adalah salah satu jenis layanan yang memungkinkan akses ke aplikasi yang dijalankan di dalam cluster Kubernetes dari luar cluster menggunakan NodePort. NodePort adalah nomor port yang dikaitkan dengan setiap node dalam cluster Kubernetes, yang memungkinkan lalu lintas masuk dari luar cluster untuk diarahkan ke layanan yang terkait.

![Untitled](service%20node%20port%205edfbca536944516a1b9f76f9be47306/Untitled.png)

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      name: nginx-label
  template:
    metadata:
      name: nginx-pod
      labels:
        name: nginx-label
    spec:
      containers:
        - name: nginx-container
          image: nginx:latest
          ports:
            - containerPort: 80

---

apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    name: nginx-label
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30002
```

## mengekspose NodePort di Minikube

```bash
minikube service nama-service
```

![Untitled](service%20node%20port%205edfbca536944516a1b9f76f9be47306/Untitled%201.png)