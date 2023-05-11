# persistent volume

persistent volume hampir sama dengan volume, namun cara kerjanya berbeda.

cara pembuatan persistent volume sedikit lebih kompleks dibanding volume, namun ada beberapa benefit yang bisa didapat jika menggunakan persistent volume

## jenis-jenins persistence volume

- HostPath, berkas disimpan di Node, tidak direkomentasikan di production, hanya untuk testing
- GCEPersistentDisk, Google Cloud Persistence Disk
- AWSElasticBlockStore, amazon web service persistence disk
- AzureFile / AzureDisk, microsoft Azure Persistence disk
- dsb

## tahapan membuat persistent volume

- buat persistent volume
- buat persistent volume claim
- menambahkan persistent volume claim ke pod

![Untitled](persistent%20volume%202eb474838dad4ac087d6dacce2abfcac/Untitled.png)

## melihat persistent volume

```bash
kubectl get pv
kubectl describe pv namapv
```

![Untitled](persistent%20volume%202eb474838dad4ac087d6dacce2abfcac/Untitled%201.png)

## melihat persistent volume claim

```bash
kubectl get pvc
kubectl describe pvc nama_pvc
```

![Untitled](persistent%20volume%202eb474838dad4ac087d6dacce2abfcac/Untitled%202.png)

## persistent volume example

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: nodejs-writer-volume
spec:
  accessModes:
    - ReadWriteOnce
  capacity:
    storage: 5Gi
  hostPath:
    path: /data/location

---

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: nodejs-writter-volume-claim
spec:
  accessModes:
    - ReadWriteOnce
  volumeMode: Filesystem
  resources:
    requests:
      storage: 1Gi

---

apiVersion: v1
kind: Pod
metadata:
  name: nodejs-writer
  labels:
    name: nodejs-writer-label
spec:
  volumes:
    - name: html
      persistentVolumeClaim:
        claimName: nodejs-writer-volume-claim
  containers:
    - name: nodejs-writer-container
      image: khannedy/nodejs-writer:latest
      volumeMounts:
        - mountPath: /app/html
          name: html
```

- ReadWriteOnce -- volume dapat dipasang sebagai *read-write* oleh satu *node*
- ReadOnlyMany -- volume dapat dipasang sebagai *read-only* oleh banyak *node*
- ReadWriteMany -- volume dapat dipasang sebagai *read-write* oleh banyak *node*

## masuk ke dalam container

![Untitled](persistent%20volume%202eb474838dad4ac087d6dacce2abfcac/Untitled%203.png)