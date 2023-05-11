# multi container pod

saat kita mendeploy aplikasi di kubernetes, maka akan disimpan ke dalam 1 pod, dan di dalam pod, kita bisa menambahkan lebih dari 1 container.

antar container akan menggunakan IP yang sama, jadi pastikan antar container portnya berbeda

![Untitled](multi%20container%20pod%2088548d1ed2944b7283344b5bfb8e159f/Untitled.png)

## multi container example

```jsx
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
        - name: nodejs-web-container
          image: khannedy/nodejs-web:latest
          ports:
            - containerPort: 3000

---

apiVersion: v1
kind: Service
metadata:
  name: nginx-service
  labels:
    name: nginx-label
spec:
  type: ClusterIP
  selector:
    name: nginx-label
  ports:
    - port: 8080
      targetPort: 80
      name: nginx
    - port: 3000
      targetPort: 3000
      name: nodejs-web

---

apiVersion: v1
kind: Pod
metadata:
  name: curl-pod
  labels:
    name: curl-label
spec:
  containers:
    - name: curl-container
      image: khannedy/nginx-curl:latest
```

jalankan file konfigurasi

masuk ke dalam container 

![Untitled](multi%20container%20pod%2088548d1ed2944b7283344b5bfb8e159f/Untitled%201.png)