# ekspose service

kadang ada kebutuhan kita perlu untuk mengeskpos service keluar, tujuannya adalah agar aplikasi dari luar kubernetes cluster bisa mengakses pod yang berada di belakang service tersebut

![Untitled](ekspose%20service%201583edde70f14288b9e707a82ed9cc43/Untitled.png)

## tipe service

- service memiliki beberapa tipe, yaitu:
- clusterIP: mengkspose servcie di dalam internal kubernetes cluster
- externalName: memetakan service ke externalName (misalnya: example.com)
- nodeport: mengekspose service pada setiap IP node dan port yang sama, kita dapat mengakses service dengan tipe ini, dari luar cluster melalui <node_ip>:<node_port>
- loadBalancer: mengekspos service secara eksternal dengan menggunakan LoadBalancer yang disediakan oleh penyedia layanan cloud

## cara untuk mengekspos service

ada 3 cara untuk mengekspose service keluar yaitu:

- NodePort: sehingga node akan membuka port yang akan menneruskan request ke service yang dituju
- LoadBalancer, sehingga service bisa diakses via LoadBalancer, dan LoadBalancer akan menruskan request ke NodePort dan dilanjutkan ke Service
- Ingress, dimana ingress adalah resource yang memang ditunjukan untuk mengekspos service. namun ingress hanya beroperasi di level HTTP