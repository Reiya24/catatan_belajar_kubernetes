# manage kubernetees object

## imperative management

- kubectl create -f nama_file.yaml > membuat kubernetes object
- kubectl replace -f nama_file.yaml > mengupdate kuberbetes object (namun tidak semua kubernetes object bisa diupdate)
- kubectl get -f nama_file.yaml -o yaml/json > melihat kubernetes object
- kubectl delete -f nama_file.yaml kubernetes objecct

## declarative management

kubectl apply -f nama_file.yaml > membuat atau mengupdate kubernetes object

saat menggunakan declarative management, file konfigurasi akan disimpan di dalam annotations object

hal ini sangat bermanfaat saat menggunakan object deployment

declarative management lebih sering digunakan dibanding imperative management