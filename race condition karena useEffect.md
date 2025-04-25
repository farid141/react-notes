# Penjelasan

ketika sebuah useEffect depend ke sebuah atribut dan atribut tersebut berubah dengan cepat sebelum request pertama selesai. Race condition akan terjadi karena pengubahan state bersamaan.

## 1. Flag async

```javascript
useEffect(() => {
  let isSubscribed = true;

  // declare the function
  const fetchData = async () => {
    const data = await fetch(`https://yourapi.com?param=${param}`);
    const json = await response.json();

    // set state with the result if `isSubscribed` is true
    if (isSubscribed) {
      setData(json);
    }
  }

  // call the function
  fetchData()
    .catch(console.error);;

  // cancel any future `setData`
  return () => isSubscribed = false;
}, [param])
```

Ketika async selesai maka async sebelumnya tidak akan mengupdate state apabila ada async baru yang berjalan (ditandai dengan isSubscribed=false).

## 2. Debounce / Throttle

Kalau kamu ingin membatasi seberapa sering efek dijalankan, kamu bisa debounce-nya:

```javascript
import { useEffect, useState } from 'react';
import _ from 'lodash';

function MyComponent({ query }) {
  const [results, setResults] = useState([]);

  const debouncedQuery = _.debounce(query, 500);

  useEffect(() => {
    const fetchData = async () => {
      const res = await fetch(`/search?q=${debouncedQuery}`);
      const data = await res.json();
      setResults(data);
    };

    if (debouncedQuery) fetchData();
  }, [debouncedQuery]);

  return <div>{/* render results */}</div>;
}
```

Alternatifnya kamu juga bisa buat debounce pakai useRef dan setTimeout manual.

## 3. Abort Fetch / Cancel Previous Requests

Kalau pakai fetch atau axios, kamu bisa batalkan request sebelumnya jika ada request baru:

Contoh dengan AbortController:

```javascript
useEffect(() => {
  const controller = new AbortController();
  const signal = controller.signal;

  const fetchData = async () => {
    try {
      const res = await fetch(url, { signal });
      const data = await res.json();
      setData(data);
    } catch (e) {
      if (e.name !== 'AbortError') {
        console.error('Fetch error:', e);
      }
    }
  };

  fetchData();

  return () => controller.abort(); // cleanup, cancel fetch if effect runs again
}, [url]);
```
