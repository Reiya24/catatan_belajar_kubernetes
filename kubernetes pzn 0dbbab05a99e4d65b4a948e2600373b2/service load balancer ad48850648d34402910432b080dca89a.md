# service load balancer

kubernetes bisa menggunakan LoadBalancer bawaan dari cloud provider sebagai cara untuk mengekspos service. LoadBalancer akan melakukan load balace request ke NodePort, sayangnya service LoadBalancer tidak bisa di test di local seperti menggunakan minikube

![Untitled](service%20load%20balancer%20ad48850648d34402910432b080dca89a/Untitled.png)

![Untitled](service%20load%20balancer%20ad48850648d34402910432b080dca89a/Untitled%201.png)

## contoh load balancer:

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
        - name: nginx-contianer
          image: nginx:latest
          ports:
            - containerPort: 80

---

apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: LoadBalancer
  selector:
    name: nginx-label
  ports:
    - port: 80
      targetPort: 80
```

untuk menggunakan LoadBalancer pada minikube, gunakan perintah

```bash
minikube tunnel
```

![Untitled](service%20load%20balancer%20ad48850648d34402910432b080dca89a/Untitled%202.png)

setelah mengekspose load balancer, terdapat external ip di minikube

![Untitled](service%20load%20balancer%20ad48850648d34402910432b080dca89a/Untitled%203.png)

![Untitled](service%20load%20balancer%20ad48850648d34402910432b080dca89a/Untitled%204.png)