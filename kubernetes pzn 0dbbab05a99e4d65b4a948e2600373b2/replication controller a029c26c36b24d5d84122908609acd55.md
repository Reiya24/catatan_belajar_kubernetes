# replication controller

replication controller bertugas untuk memastikan bahwa pod selalu berjalan. jika ada pod yang mati atau hilang, misal ketika ada node yang mati, maka replication controller secara otomatis akan menjalankan pod yang mati / hilang tersebut

## isi replication controller

- label selector: sebagai penanda pod
- replica count: jumlah pod yang seharusnya berjalan
- pod template: template yang digunakan untuk menjalankan pod

## contoh replication controller

```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: nginx-replication-controller
spec:
  replicas: 3
  selector:
    app: nginx-label
  template:
    metadata:
      name: nginx-pod
      labels:
        app: nginx-label
    spec:
      containers:
        - name: nginx
          image: nginx:latest
          ports:
            - containerPort: 80
```

- selector harus sama dengan labels yang ada di template

jalankan file konfigurasi, lalu secara otomatis replicationcontroller akan membuat 3 pod dengan nama yang unik

![Untitled](replication%20controller%20a029c26c36b24d5d84122908609acd55/Untitled.png)

## melihat replication controller

```yaml
kubectl get replicationcontrollers
kubectl get replicationcontroller
kubectl get rc
```

![Untitled](replication%20controller%20a029c26c36b24d5d84122908609acd55/Untitled%201.png)

## menghapus replication controller

saat menghapus replication controller, maka secara otomatis pod yang berada pada label selectornya akan ikut terhapus. jika ingin menghapus replication controller tanpa menghapus pod yang berada pada label selectornya, tambahkan opsi —cascade-false

```yaml
kubectl delete rc nama_rc
kubectl delete rc nama_rc --cascade=false
```

![Untitled](replication%20controller%20a029c26c36b24d5d84122908609acd55/Untitled%202.png)