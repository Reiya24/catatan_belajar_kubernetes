# statefulset

## stateless application

pod, replicaset, replicationcontroller, deployment, itu semua cocok digunakan untuk aplikasi jenis stateless

stateless artinya aplikasi kita tidak menyimpan state atau data, jadi jika ditengah jalan aplikasi kita dihapus dan dibuat ulang, tidak akan bermasalah.

namun, bagaimana dengan aplikasi yang stateful? seperti contohnya database? yang harus menyimpan data? dan tidak bisa sembarangan dihapus di tenah jalan ketika kita melakukan update aplikasi

## statelss dengan persistent volume

persistenvolume pun tidak akan membantu jika kita memiliki aplikasi yang stateful, karena semua pod akan meng-claim persistent volume yang sama, dan direktori yang sama

sedangkat jika aplikasi kita stateful, kemungkinan besar, kita ingin memiliki data yang independen tiap pod, walaupun jenis pod nya sama

![Untitled](statefulset%20f330c018b6244f62b2aca4fd7c8009fd/Untitled.png)

![Untitled](statefulset%20f330c018b6244f62b2aca4fd7c8009fd/Untitled%201.png)

## statefulset

statefulset adalah object di kubernetes untuk memanage aplikasi jenis stateful

statefulset akan memastikan bahwa nama pod yang konsisten, identitas network yang stabil, dan persistent volume yang stabil untuk tipa pod

jika ada pod yang mati, maka statefulset akan membuat pod baru dengan nama dan informasi yang sama dengan pod yang mati

## membuat satefulset

membuat statefulset sama seperti replicaset, namun statefulset memiliki kemampuan untuk menambahkan volume claim template

## statefulset example

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: nodejs-stateful-volume
spec:
  accessModes:
    - ReadWriteOnce
  capacity:
    storage: 5Gi
  hostPath:
    path: /data/location

---

apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: nodejs-stateful-statefulset
  labels:
    name: nodejs-stateful-label
spec:
  serviceName: nodejs-stateful-service
  replicas: 3
  selector:
    matchLabels:
      name: nodejs-stateful-label
  volumeClaimTemplates:
    - metadata:
        name: nodejs-stateful-volume-claim
      spec:
        accessModes:
          - ReadWriteOnce
        volumeMode: Filesystem
        resources:
          requests:
            storage: 1Gi
  template:
    metadata:
      name: nodejs-stateful-container
      labels:
        name: nodejs-stateful-label
    spec:
      containers:
        - name: nodejs-stateful-container
          image: khannedy/nodejs-stateful:latest
          env:
            - name: POD_NAME
              valueFrom:
                fieldRef:
                  fieldPath: metadata.name
          volumeMounts:
            - mountPath: /app/data
              name: nodejs-stateful-volume-claim
```

![Untitled](statefulset%20f330c018b6244f62b2aca4fd7c8009fd/Untitled%202.png)