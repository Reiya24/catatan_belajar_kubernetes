# sharing volume

karena di dalam pod kita bisa membuat lebih dari satu container, maka volume di pod pun bisa kita sharing ke beberapa container. hal ini sangat cocok ketika kita butuh sharing direktori antar container, misal container pertama membuat file, container kedua memproses file

![Untitled](sharing%20volume%207277afeb0b034e558fdf9e8bb5264c39/Untitled.png)

## sharing volume example

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
      volumes:
        - name: html
          emptyDir: {}
      containers:
        - name: nodejs-writter-container
          image: khannedy/nodejs-writer:latest
          volumeMounts:
            - mountPath: /app/html
              name: html
        - name: nginx-container
          image: nginx:latest
          ports:
            - containerPort: 80
          volumeMounts:
            - mountPath: /usr/share/nginx/html
              name: html

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
    - port: 8080
      targetPort: 80
      nodePort: 30001
```

akses menggunakan

```bash
minikube service nama_service
```

![Untitled](sharing%20volume%207277afeb0b034e558fdf9e8bb5264c39/Untitled%201.png)

![Untitled](sharing%20volume%207277afeb0b034e558fdf9e8bb5264c39/Untitled%202.png)