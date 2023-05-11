# horizontal pod autoscaler

## application scaling

saat aplikasi kita sedang sibuk, sehingga konsumsi memory atau cpu tinggi, amaka ada kemungkinan performa aplikasi kita akan turun.

saat hal ini terjadi, application scaling sangat dibutuhkan

secara garis besar, ada 2 jenis application scaling; vertical scaling dan horizontal scaling

## vertical scaling

vertical scaling adalah cara application scaling dengan cara mengupgrade computational resource di aplikasi kita

misal dari 1 cpu menjadi 2 cpu, dari 1 memory menjadi 2GB memory.

namun permasalahan vertical scaling adalah, akan ada batasnya. pod di kubernetes tidak bisa menggunakan resource melebihi resource node yang ada 

## horizontal scaling

horizontal scaling adalah application scaling dengan cara membuat pod baru agar beban pekerjaan bisa didistribusikan ke pod baru tersebut.

scalability terbaik seharusnya dicapai dengan horizontal scaling, karena dengna horizontal scaling, kita tidak butuh upgrade node dengan resourece yang lebih tinggi

## vertical pod autoscaler

vertical pod autoscaler adalah kemampuan scara otomatis application scaling secara vertical dengan cara mengupgrade resource pod dan menurunkan otomatis jika diperlukan

## horizontal pod autoscaler

horizontal pod autoscaler adalah kemampuan secara otomatis application scaling secara horizontal dengan cara menambah pod baru dan menurunkan secara otomatis jika diperlukan.

horizontal pod autoscler (HPA) merupakan object di kubernetes, kita bisa membuat HPA, dan menghapus HPA di kubernetes

HPA bekerja dengan cara mendengarkan data metrics dari setiap pod, dan jika sudah mencapai batas tertentu, HPA akan melakukan auto scaling (baik itu menaikan pod, atau menurunkan jumlah pod)

![Untitled](horizontal%20pod%20autoscaler%20fa89cc1b32ec4a7b903f465c9c6890b1/Untitled.png)

## horizontal pod autoscaler example

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nodejs-web-deployment
  labels:
    name: nodejs-web-label
spec:
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
    app: nodejs-web-service
  ports:
    - port: 3000
      targetPort: 3000
      nodePort: 30001

---

apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: nodejs-web-hpa
spec:
  minReplicas: 3
  maxReplicas: 5
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: nodejs-web-deployment
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 70
    - type: Resource
      resource:
        name: memory
        target:
          type: Utilization
          averageUtilization: 70
```