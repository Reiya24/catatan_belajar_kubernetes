# deployment

update aplikasi secara manual bukanlah hal bijak, kesalahan kecil yang kita lakukan saat update secara manual, bisa menyebabkan downtime, sehingga aplikasi kita tidak bisa diakses

kubernetes memiliki fitur deployment, yaitu resource untuk melakukan deployment aplikasi dan update aplikasi secara deklaratif menggunakan file konfigurasi.

saat ktia membuat deployment, secara otomatis kubernetes akan membuat ReplicaSet, yang mana replicaset akan secara otomatis membuat pod.

membuat deployment hampir sama seperti membuat replicationset

![Untitled](deployment%20df4b0df4dd904fa9af293b64b445c789/Untitled.png)

## membuat deployment

```bash
kubectl apply -f nama_file.yaml
```

![Untitled](deployment%20df4b0df4dd904fa9af293b64b445c789/Untitled%201.png)

## melihat deployment

```bash
kubectl get deployment
```

![Untitled](deployment%20df4b0df4dd904fa9af293b64b445c789/Untitled%202.png)

## menghapus deployment

```bash
kubectl delete deployment nama_deployment
```

## melihat detail deployment

```bash
kubectl describe deployment nama_deployment
```

## deployment example

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nodejs-web-deployment
  labels:
    name: nodejs-web-label
spec:
  revisionHistoryLimit: 5
  replicas: 3
  selector:
    matchLabels:
      name: nodejs-web-label
  template:
    metadata:
      name: nodejs-web-pod
      labels:
        name: nodejs-web-label
    spec:
      containers:
        - name: nodejs-web-container
          image: khannedy/nodejs-web:1
          ports:
            - containerPort: 3000

---
apiVersion: v1
kind: Service
metadata:
  name: nodejs-web-service
spec:
  type: NodePort
  selector:
    name: nodejs-web-label
  ports:
    - port: 3000
      targetPort: 3000
      nodePort: 30001
```