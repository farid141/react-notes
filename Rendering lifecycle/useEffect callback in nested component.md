# Penjelasan

Memungkinkan jika ada skenario sebuah komponen punya child, dan di kedua komponen tersebut memiliki useEffect. Lantas callback mana yang akan dieksekusi dahulu?

## Rendering concept
React melakukan rendering seperti pohon dari atas ke bawah (parent-child). Sehingga callback useEffect dilakukan ketika masing-masing komponen telah di-mount.

## useEffect Behavior
useEffect akan menjalankan fungsi callback dengan trigger dependensi berubah. Dan akan dilakukan setelah komponen tersebut selesai dimount