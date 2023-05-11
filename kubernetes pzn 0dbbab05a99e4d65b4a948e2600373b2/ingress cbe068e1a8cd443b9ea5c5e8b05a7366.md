# ingress

## masalah saat mengekspose service menggunakakn NodePort dan LoadBalancer

masalah saat mengekspose service menggunakan NodePort adalah, Node harus terekspose ke publik, dan client harus tau semua ip address semua node.

sementara masalah saat menggunakan LoadBalancer adalah, semua NodeBalancer juga harus terekspose ke public, dan client juga harus tau semua ip address semua LoadBalancer.

## inggress

ingress adalah salah satu cara yang bisa digunakan untuk mengekspos service.

client hanya butuh tahu satu lokasi ip address ingress. ketika client melakukan request ke ingress, pemilihan servicenya ditentukan menggunakan hostname dari request. ingress hanya mendukung procol HTTP

![Untitled](ingress%20cbe068e1a8cd443b9ea5c5e8b05a7366/Untitled.png)

## enable addon ingress

```jsx
minikube addons enable ingress
```

![Untitled](ingress%20cbe068e1a8cd443b9ea5c5e8b05a7366/Untitled%201.png)

## ingress example

```jsx
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      name: nginx-label
  template:
    metadata:
      name: nginx-container
      labels:
        name: nginx-label
    spec:
      containers:
        - name: nginx
          image: nginx:latest
          ports:
            - containerPort: 80

---

apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    name: nginx-label
  ports:
    - port: 80
      targetPort: 80

---

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx-ingress
  labels:
    name: nginx-ingress
spec:
  rules:
    - host: nginx.reiya.local
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: nginx-service
                port:
                  number: 80
```

edit /etc/hosts

![Untitled](ingress%20cbe068e1a8cd443b9ea5c5e8b05a7366/Untitled%202.png)

untuk melihat ip dari cluster minikube

```jsx
minikube ip
```

![Untitled](ingress%20cbe068e1a8cd443b9ea5c5e8b05a7366/Untitled%203.png)

## melihat ingress

```bash
kubectl get ingresses
```

![Untitled](ingress%20cbe068e1a8cd443b9ea5c5e8b05a7366/Untitled%204.png)

![Untitled](ingress%20cbe068e1a8cd443b9ea5c5e8b05a7366/Untitled%205.png)