# computational resources

saat kita membuat pod, secara default kita akan menggunakan resource yang dimiliki oleh node dimana pod berada

kadang ada kebutuhan untuk membatasi jumlah resource yang digunakan oleh pod, hal ini dilakukan agar tidak terjadi perebutan resource antar pod

jangan sampai jika ada pod yang sibuk, membuat semua pod di node yang sama menjadi lambat karena resourcenya terpakai penuh oleh pod yang sibuk

## request dan limit

request dan limit adalah mekanisme kubernetes untuk mengontrol mekanisme penggunaan memory dan CPU

request adalah apa yang container digaransi didapatkan, jika sebuah contaienr me-request resource, maka kubernetes hanya akan menjalankan di node yang memiliki resource tersebut.

sedangkan limit adalah untuk memastikan container tidak akan pernah melwati resource tersebut, container hanya boleh menggunakan resource sampai limit, tidak boleh lebih