Dalam react, statement yang terdapat dalam fungsi komponen akan dieksekusi kembali pada saat komponen di-rerender. Terkadang kita tidak ingin menjalankan statement tersebut di semua komponen re-render, tetapi hanya pada saat waktu tertentu.

Contoh kasus:
Ketika kita melakukan request api dalam fungsi komponen, request akan berjalan asinkronus. Didalam callbacknya, terdapat aksi untuk mengupdate state. Sehingga komponen akan dirender lagi dan request API dilakukan kembali terus menerus.

Untuk itu kita bisa menggunakan useEffect() hooks, yang membatasi sebuah statement hanya dijalankan ketika apa saja
