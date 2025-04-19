# Redux toolkit

Redux Toolkit adalah library resmi dari Redux yang dirancang untuk memudahkan pengembangan aplikasi menggunakan Redux.

1. Instalasi

    ```bash
    npm install @reduxjs/toolkit react-redux
    ```

2. Struktur File

    ```tree
    store
    ├─ index.js
    ├─ counter.js
    ```

---

## Keunggulan `createSlice()` dari redux, dibanding `createReducer()` dari redux-toolkit

### ✅ Modular & Simpel

`createSlice()` memudahkan pengelolaan state dan reducer dalam satu tempat (per modul/file).

#### ✅ Tidak Perlu Cek `action.type` Manual

Reducer langsung berbentuk fungsi, bukan switch-case panjang.

#### ✅ Boleh Mutasi State Langsung

Berkat bantuan **Immer** di balik layar, kita bisa langsung ubah `state` tanpa `return` object baru.

---

```js
// counter.js
import { createSlice } from '@reduxjs/toolkit';

const counterSlice = createSlice({
  name: 'counter',
  initialState: { counter: 0 },
  reducers: {
    increment(state, action) {
      state.counter += action.payload;
    },
  },
});


export const counterActions = counterSlice.actions;
export default counterSlice.reducer;
```

---

## 🏗️ Mengelola Banyak Reducer: `configureStore()`

Alih-alih `createStore()` dari redux, gunakan `configureStore()` dari Redux Toolkit. Ini otomatis:

- Menggabungkan banyak reducer
- Menyediakan middleware secara default
- Mengaktifkan Redux DevTools

Fungsi ini menerima parameter objek berisi field reducer didalamnya terdapat reducer dari berbagai slice yang telah dibuat.

```js
// index.js
import { configureStore } from '@reduxjs/toolkit';

const store = configureStore({
  reducer: {
    counter: counterSlice.reducer,
    // tambah reducer lain di sini
  },
});

export default store;
```

> 🗝 Key pada objek `reducer` menentukan nama slice di global state.

---

## Penggunaan state redux di komponen lain

```jsx
import { useSelector, useDispatch } from 'react-redux';
import { counterActions } from '../store/counter';

const Counter = () => {
  const dispatch = useDispatch();
  const counter = useSelector((state) => state.counter.counter);
  const show = useSelector((state) => state.counter.showCounter);

  const incrementHandler = () => {
    dispatch(counterActions.increment());
  };

  const increaseHandler = () => {
    dispatch(counterActions.increase(10)); // { type: SOME_UNIQUE_IDENTIFIER, payload: 10 }
  };
}
```

---

> Kita juga dapat menginstall ekstensi redux devtools pada browser untuk dapat melihat global state dengan mudah dan dapat merekam sebuah perubahan state
