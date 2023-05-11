# environment variable

kubernetes mendukung environment variable untuk pod yang berfungsi untuk konfigurasi aplikasi, seperti konfigurasi database, dll

## environment variable example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nodejs-writer-pod
  labels:
    app: nodejs-writer-label
spec:
  volumes:
    - name: html
      emptyDir: {}
  containers:
    - name: nodejs-writer-container
      image: khannedy/nodejs-writer:latest
      volumeMounts:
        - mountPath: /app/folder-from-env
          name: html
      env:
        - name: HTML_LOCATION
          value: /app/folder-from-env
```

masuk ke dalam container

![Untitled](environment%20variable%20b656eaacc28d49e78d11902438f821c6/Untitled.png)