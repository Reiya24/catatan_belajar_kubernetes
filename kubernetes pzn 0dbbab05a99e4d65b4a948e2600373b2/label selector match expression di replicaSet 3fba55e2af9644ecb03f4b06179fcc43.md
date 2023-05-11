# label selector match expression di replicaSet

sebelumnya, selector di replication set menggunakan matchLabels, selain menggunakan matchLabels, operasi lain yang bisa digunakan pada selector di ReplicationSet adalah menggunakan matchExpression

## operasi di match expresion

- in, value label harus ada di value in
- NotIn, value label tidak boleh ada di value in
- Exists, label harus ada
- NotExists, label tidak boleh ada

## contoh match expression

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-replicaset
spec:
  replicas: 3
  selector:
    matchExpressions:
      - key: app
        operator: In
        values:
          - nginx
      - key: env
        operator: In
        values:
          - prod
          - qa
          - dev
  template:
    metadata:
      name: nginx-pod
      labels:
        app: nginx
        env: prod
    spec:
      containers:
        - name: nginx-container
          image: nginx:latest
          ports:
            - containerPort: 80
```