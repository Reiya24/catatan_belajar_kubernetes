# kubernetes dashboard

di kenyataan mungkin kita akan menggunakan cloud proice untuk manage object di kubernetes, dimana cloud provicer sudah menyediakan web user interface untuk manage object kubernetesnya

atau jika kita menginstall kubernetes di datacenter sendiri, kita bisa menginstall web user interface untuk manage object di kubernetes, namanya adalah kubernetes dashboard, sebuah aplikasi opensource yang digunakan untuk manage object di kubernetes menggunakan web

## kubernetes dashboard di minikube

install minikube dashboard dan metrics-server

```yaml
minikube addons enable dashboard
minikube addons enable metrics-server
```

![Untitled](kubernetes%20dashboard%209cb05e801a4e455cba19458c5c7abd14/Untitled.png)

untuk menjalankanya, gunakan perintah

```yaml
minikube dashboard
```

![Untitled](kubernetes%20dashboard%209cb05e801a4e455cba19458c5c7abd14/Untitled%201.png)