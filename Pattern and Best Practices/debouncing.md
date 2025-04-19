# 🌀 Debouncing

## 📌 Pengertian

**Debouncing** adalah pola (pattern) untuk menunda eksekusi suatu fungsi sampai selang waktu tertentu telah berlalu **sejak terakhir kali fungsi tersebut dipanggil**. Tujuannya adalah untuk **mengurangi frekuensi update**, misalnya saat user mengetik di input field atau saat event `resize`/`scroll`.

## 📘 Use Case

- Input pencarian: fetch API hanya setelah user berhenti mengetik selama beberapa saat.
- Resize window: menunggu sampai user selesai mengubah ukuran.
- Scroll listener: menghindari terlalu banyak render.

---

## 🎯 Konsep

Menggunakan:

- `setTimeout` untuk menjadwalkan update.
- `clearTimeout` untuk membatalkan timeout jika ada event baru.
- `useRef` untuk menyimpan timeout ID agar tidak reset pada re-render.
- `useState` untuk update nilai secara reactive.

---

## 📄 Contoh Kode: Input dengan Debounce

```jsx
import { useState, useRef } from 'react';

function DebouncedInput() {
  const [search, setSearch] = useState('');
  const [debouncedValue, setDebouncedValue] = useState('');
  const timeoutRef = useRef(null);

  const handleChange = (e) => {
    const value = e.target.value;
    setSearch(value);

    // Clear timeout sebelumnya
    if (timeoutRef.current) {
      clearTimeout(timeoutRef.current);
    }

    // Set timeout baru
    timeoutRef.current = setTimeout(() => {
      setDebouncedValue(value); // Update state setelah delay
    }, 500); // Delay 500ms
  };

  return (
    <div>
      <input type="text" value={search} onChange={handleChange} placeholder="Ketik sesuatu..." />
      <p>Hasil debounce: {debouncedValue}</p>
    </div>
  );
}
```

---

- `search`: state langsung dari input.
- `debouncedValue`: hanya berubah jika user berhenti mengetik selama 500ms.
- `useRef` menyimpan timeout ID agar bisa dibatalkan sebelum membuat timeout baru.
- Tidak terjadi update state berkali-kali saat user aktif mengetik.

---

Kalau kamu mau contoh lain (seperti resize listener atau penggunaan di API call), tinggal bilang aja ya!
