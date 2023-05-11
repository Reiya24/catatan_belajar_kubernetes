# arsitektur kubernetes

## kubernetes cluster

Saat kita menjalankan kubernetes artinya kita menjalankan sebuah cluster. dalam sebuah cluster terdapat beberapa node. node merupakan sebuah server, baik server fisik maupun virtual private server yang digunakan untuk menjalankan kubernetes. untuk membuat cluster kubernetes dibutuhkan setidaknya 2 jenis server yang dibutuhkan, yaitu master node dan worker nodes

![Untitled](arsitektur%20kubernetes%202984be398c7a48e2938f466ebb720320/Untitled.png)

## master node

master node sebagai control plane bagi cluster. bertugas untuk mengatur seluruh operasi cluster.
komponen-komponen di dalam kubernetes master diantaranya :

- kube-apiserver: bertugas sebagai API yang digunakan untuk berinteraksi dengan kubernetes cluster
- etcd: bertugas sebagai database untuk menyimpan data-data kubernetes cluster
- kube-scheduler: bertugas untuk mengamati pod baru yang belum ditempatkan di node manapun, kemudian memilihkan node di mana pod baru tersebut akan dijalankan
- kube-controller-manager: bertugas untuk mengontrol kubernetes cluster. kontroler-kontroler ini meliputi:
    - kontroler node: berfungsi untuk mengamati dan memberikan respons apabila ada jumlah node yang berkurang
    - kontroler replikasi: berfungsi untuk menjaga jumlah pod agar jumlahnya sesuai dengan kebutuhan setiap objek kontroler replikasi yang ada di sistem
    - kontroler endpoints: menginisiasi objek endpoints
    - kontroler service account & token: membuat akun dan akses token API standar untuk setiap namespaces yang dibuat
- cloud-controller-manager: bertugas untuk melakukan kontrol terhadap interaksi dengan cloud provider

## worker node

worker node berfungsi untuk menjalankan tugas yang diberikan oleh master node. komponen-komponen di dalam worker node diantaranya:

- kubelet: bertugas untuk memastikan bahwa pod kita berjalan di node
- kube-proxy: berjalan di setiap node dan bertugas sebagai proxy terhadap arus network yang masuk ke aplikasi kita, serta sebagai load balancer
- container-manager: bertugas sebagai container manager, kubernetes mendukung beberapa layanan container manager, seperti docker, containerd,cri-o, rklet