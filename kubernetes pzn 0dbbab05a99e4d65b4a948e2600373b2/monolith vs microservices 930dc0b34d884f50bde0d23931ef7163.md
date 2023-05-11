# monolith vs microservices

## monolith

Arsitektur Monolith merupakan sebuah arsitektur dimana semua komponen berada di dalam satu kesatuan yang sama, karena itu proses pengembangan jauh lebih mudah, Karena berada dalam satu server, dengan begitu juga, latency komunikasinya antar komponen jauh lebih cepat, Namun arsitektur ini juga memiliki beberapa konsekuensi, karena semua komponen berada di dalam server yang sama, bila terjadi pemeliharanan atau sedang terjadi masalah, Semua komponen tersebut tidak akan berjalan karena semuanya berada di dalam satu server. Serta arsitektur ini juga memiliki keterbatasan dalam scaling, dimana kita hanya bisa menduplikasi secara keseluran komponen tersebut.

## microservices

Sedangkan arsitektur Microserves adalah kebalikannya dari arsitektur monolith, dimana suatu kesatuan tersebut dipecah ke dalam infrastrukturnya sendiri-sendiri, dengan begitu proses scalingnya bisa lebih fleksibel, Serta jika terjadi proses pemeliharaan atau sedang terjadi masalah, hanya suatu komponen saja yang down, komponen komponen lainnya masih bisa bekerja karena terpisah dengan komponen yang sedang down, namun microservices juga tetap memiliki kekurangan, diantaranya proses pengembangannya jauh lebih rumit karena memiliki arsitektur yang kompleks, serta butuh biaya yang lebih tinggi dibandingkan arsitektur monolith