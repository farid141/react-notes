## Aturan hooks
dua aturan utama hooks:
1. Hanya bisa dipanggil dalam komponen
2. Tidak bisa dalam nested block

## Kegunaan
- reusability code lebih rapi, seperti pola dalam kasus useEffect, didalamnya berisi request ke api dan menghasilkan state data, loading dan error 
- bisa memanage state, ketika state dalam custom hook update, komponen pemanggil akan re-render
- bisa outsource setter dan getter dari state

## Membuat custom hook
1. buat folder dengan nama hooks (bebas)
2. buat misal useFetch.js


>nama fungsi custom hooks harus berawalan use- agar "aturan utama hooks" diterapkan dan error warning aktif

## Contoh
Let's take **`useFetch`** as a practical example of an advanced custom hook. It's commonly used for making API requests inside React components, and it helps abstract away the fetch logic, loading state, and error handling.

---

### 🔧 **`useFetch` Custom Hook**

```js
import { useState, useEffect, useCallback } from 'react';

function useFetch(url, options = {}) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState(null);
  const [trigger, setTrigger] = useState(0);

  const refetch = useCallback(() => {
    setTrigger(prev => prev + 1);
  }, []);

  useEffect(() => {
    if (!url) return;

    const controller = new AbortController();
    const signal = controller.signal;

    const fetchData = async () => {
      setLoading(true);
      setError(null);

      try {
        const res = await fetch(url, { ...options, signal });
        if (!res.ok) throw new Error(`HTTP error! status: ${res.status}`);
        const json = await res.json();
        setData(json);
      } catch (err) {
        if (err instanceof Error && err.name !== 'AbortError') {
          setError(err);
        }
      } finally {
        setLoading(false);
      }
    };

    fetchData();

    return () => controller.abort();
  }, [url, trigger]); // tergantung pada trigger

  return { data, loading, error, refetch };
}

```

---

### 📦 **Usage Example**

```js
function UsersList() {
  const { data, loading, error, refetch } = useFetch('https://jsonplaceholder.typicode.com/users');

  return (
    <div>
      <button onClick={refetch}>🔄 Refresh</button>

      {loading && <p>Loading users...</p>}
      {error && <p>Error: {error.message}</p>}

      {data && (
        <ul>
          {data.map(user => (
            <li key={user.id}>{user.name}</li>
          ))}
        </ul>
      )}
    </div>
  );
}

```