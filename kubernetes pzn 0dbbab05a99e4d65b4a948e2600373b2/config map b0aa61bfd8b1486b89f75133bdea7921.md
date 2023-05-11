# config map

## masalah dengan hardcorde konfigurasi

saat kita meng-hardcode konfigurasi environment variable di file yaml kubernetes, artinya kita harus siap-siap membuat file konfigurasi berbeda-beda tiap jenis environment.

misal jika kita punya environment production, development, dan qa, kita harus membuat file untuk tiap environment

jjika sampai kita lupa meng-update file konfigurasi, maka salah-salah kita bisa menggunakan konfigurasi environment yang salah

## config map

kubernetes memiliki kemampuan memisahkan konfigurasi dalam object bernama configmap, yang berisi konfigurasi key-value

aplikasi tidak perlu membaca konfigurasi langsung ke configMap, melainkan kubernetes akan mengirim konfigurasi di configmap ke dalam environment variable

![Untitled](config%20map%20b0aa61bfd8b1486b89f75133bdea7921/Untitled.png)

## config map example

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: nodejs-env-config
data:
  APPLICATION: My Cool Application
  VERSION: 1.0.0

---

apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nodejs-env-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      name: nodejs-env-label
  template:
    metadata:
      name: nodejs-env-pod
      labels:
        name: nodejs-env-label
    spec:
      containers:
        - name: nodejs-env-container
          image: khannedy/nodejs-env:latest
          ports:
            - containerPort: 3000
          envFrom:
            - configMapRef:
                name: nodejs-env-config

---

apiVersion: v1
kind: Service
metadata:
  name: nodejs-env-service
spec:
  type: NodePort
  selector:
    name: nodejs-env-label
  ports:
    - port: 3000
      targetPort: 3000
      nodePort: 30001
```

masuk ke dalam container

![Untitled](config%20map%20b0aa61bfd8b1486b89f75133bdea7921/Untitled%201.png)

expose keluar

![Untitled](config%20map%20b0aa61bfd8b1486b89f75133bdea7921/Untitled%202.png)

![Untitled](config%20map%20b0aa61bfd8b1486b89f75133bdea7921/Untitled%203.png)

## melihat detail configmap

![Untitled](config%20map%20b0aa61bfd8b1486b89f75133bdea7921/Untitled%204.png)

![Untitled](config%20map%20b0aa61bfd8b1486b89f75133bdea7921/Untitled%205.png)