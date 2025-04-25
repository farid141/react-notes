# Penjelasan

Pada saat komponen di-rerender, statement yang terdapat dalam fungsi komponen akan dieksekusi kembali.

## Derived State

Kita dapat memanfaatkan proses rendering tersebut untuk membuat `Derived State` sebuah variable turunan dari sebuah state. Derived state dapat dirender karena merupakan variabel javascript.

## Side Effect & Infinite Loop

Terkadang kita tidak ingin menjalankan statement tersebut di semua komponen re-render, tetapi hanya pada saat waktu tertentu.

### Contoh kasus

```jsx
import React, { useState } from 'react';
import axios from 'axios';

function Users() {
  const [users, setUsers] = useState([]);

  // ⚠️ Ini akan menyebabkan infinite loop!
  axios.get('https://jsonplaceholder.typicode.com/users')
    .then(response => {
      setUsers(response.data);
    });

  return (
    <ul>
      {users.map(user => <li key={user.id}>{user.name}</li>)}
    </ul>
  );
}

```

Untuk itu kita bisa menggunakan `useEffect()` hooks, yang tidak akan dieksekusi setiap komponen di-render. Melainkan ketika dependency berubah saja.
