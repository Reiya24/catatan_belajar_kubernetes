# membuat service cluster IP

## bagaimana menentukan pod untuk service

service akan mendistribusikakn trafik ke pod yang ada di belakangnya secara seimbang

service akan menggunakan label selector untuk mengetahui pod mana yang ada dibelakang service tersebut

## contoh service

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
  type: ClusterIP
  selector:
    name: nginx-label
  ports:
    - port: 8080
      targetPort: 80

---

apiVersion: v1
kind: Pod
metadata:
  name: curl-pod
  labels:
    name: curl-pod
spec:
  containers:
    - name: curl
      image: khannedy/nginx-curl
```

*Cluster IP hanya mengekspose ke cluster  

setelah file konfigurasi dijalankan, lihat cluster ip dari service dengan menggunakan perintah

```bash
kubectl get services
```

![Untitled](membuat%20service%20cluster%20IP%2040e351f8b210484a8ae66f3d39d13bd6/Untitled.png)

kita bisa masuk ke dalam pod menggunakan perintah

```yaml
kubectl exec -it nama_pod -- /bin/sh
curl http://cluster-ip:port
```

![Untitled](membuat%20service%20cluster%20IP%2040e351f8b210484a8ae66f3d39d13bd6/Untitled%201.png)

## melihat semua service

```yaml
kubectl get service
```

![Untitled](membuat%20service%20cluster%20IP%2040e351f8b210484a8ae66f3d39d13bd6/Untitled%202.png)

## melihat detail service

```yaml
kubectl describe service nama_service
```

![Untitled](membuat%20service%20cluster%20IP%2040e351f8b210484a8ae66f3d39d13bd6/Untitled%203.png)

## mengakses service

seandainya aplikasi di pod butuh mengakses pod lain via service, bagaimana cara mengetahui IP Adress service tersebut?

### menggunakan environment variable

exec pod manggunakan perintah — env | grep NAMA_SERVICE

```yaml
kubectl exec -it nama_pod -- env | grep NAMA_SERVICE
```

![Untitled](membuat%20service%20cluster%20IP%2040e351f8b210484a8ae66f3d39d13bd6/Untitled%204.png)

### menggunakan DNS

```yaml
kubectl exec -it nama_pod -- curl http://nama_service.nama_namespace.svc.cluster.local:port
```

![Untitled](membuat%20service%20cluster%20IP%2040e351f8b210484a8ae66f3d39d13bd6/Untitled%205.png)

## melihat semua endpoint

```yaml
kubectl get endpoints
```

![Untitled](membuat%20service%20cluster%20IP%2040e351f8b210484a8ae66f3d39d13bd6/Untitled%206.png)

![Untitled](membuat%20service%20cluster%20IP%2040e351f8b210484a8ae66f3d39d13bd6/Untitled%207.png)