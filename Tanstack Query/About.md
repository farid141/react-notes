# About

Merupakan package pihak ketiga dengan kegunaan:

- membuat simple code dengan pola "fetch data, set loading, message, error" seperti custom hooks
- caching data hasil fetch
- automatic listening database response change

```bash
npm i @tanstack/react-query
```

## Cara Kerja

Ketika navigasi ke halaman melookup key untuk mengambil data cache. Tetapi dibalik layar sebenarnya masih memanggil fetching, dan mere-render jika ada perubahan.

Jika kita pindah layar dan balik lagi ke halaman, akan di re-fetch langsung

## Penggunaan

1. tuliskan `useQuery()` pada awal komponen

    ```js
    const {data, isPending, isError, error} = useQuery({
        queryKey: ['some-key'], // array of keyword
        queryFn: fetchData, // pointer ke fungsi fetch data
    })
    ```

    > pastikan fungsi fetchData melakukan `throw errorMessage` jika error. Agar bisa menggunakan `isError` dan `error`

    ```js
    const response = await fetch('abc.com');

    if(!response.ok){
        const error = new Error('An error occured while fetching the events')
        error.code = response.status
        error.info = await response.json();
        throw error
    }

    const {events} = await.response.json();
    return events
    ```

### Parameter lain

- `staleTime=0`:,(waktu ms, kapan data harus di re-render lagi saat navigasi)
- `gcTim=300000e`(waktu ms, lama data akan disimpan di cache)

2. wrap komponen (bisa main) dengan provider tanstack

```js
const queryClient = new QueryClient();

<QueryClientProvider client={queryClient}>
    <App />
</QueryClientProvider>
```

## QueryFn

Merupakan sebuah fungsi yang dijalankan sebagai sumber data. Secara default menerima beberapa parameter, maka jika kita tambahkan param ke url harus disesuaikan dengan destructuring.

```js
queryFn: ({signal})=>searchEvents({signal, searchTerm})

export func searchEvents({signal, searchTerm}){
    // signal dapat dimanfaatkan untuk abort request (otomatis dipanggil ketika pindah halaman)
    fetch('abc.com', signal)
}
```