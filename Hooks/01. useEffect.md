# Penjelasan

Akan dieksekusi saat pertama rendering dan dependency berubah.Dependency dapat berupa apapun (state/variable biasa)

## Penggunaan

- tanpa params: useEffect(callback), dijalankan setiap re-render
- dengan params kosong: useEffect(callback, []) dijalankan ketika mount saja
- tanpa params: useEffect(callback, [param1, param2]) dijalankan saat mount + setiap param berubah

bisa diletakkan sebuah cleanup function untuk freeup resource/event

1. semisal vent ketika window di-resize, hanya ketika mount saja

```js
return () => {
  document.removeEventListener('click', () => {
    setCount(count + 1);
  }); // Free up resources
};

return () => {
  clearInterval(intervalId); // Free up resources
};
```

## Rendering lifecycle

1. Komponen re-render 🧠
2. Virtual DOM diffing & commit ke real DOM 🧱
3. Cleanup function dijalankan (dari useEffect sebelumnya) 🧹
4. useEffect yang baru dijalankan 🔧

## Tambahan

- Cleanup juga dijalankan ketika komponen akan di-unmount. Meskipun render berikutnya bukan ke komponen effect tersebut.

- Lebih detail:
  - 🔧 Setup function jalan        // `**Saat mount pertama**`
  - 🧹 Cleanup function jalan      // Saat dependency berubah (re-render)
  - 🔧 Setup function jalan        // Efek baru dijalankan
  - 🧹 Cleanup function jalan      // Lagi-lagi, karena dependency berubah
  - 🔧 Setup function jalan
