# Penjelasan

digunakan untuk:

- referensi ke timeout
- meminimalisir re-render (one-way binding)

Ketika two-way binding menggunakan useState, kita meletakkan handler onChange untuk mengupdate state dari input. Hal ini menimbulkan render lebih dari satu kali.

```js
edf Player(){
 const playerName = useRef()
 return (
  <input ref={playerName.current}>
  <button onClick={()=>playerName.}>get name</button>
 )
}
```

## Attribut yang tersedia pada element

pada playerName.current, kita dapat mengakses atribut/method dari element HTML tersebut. Dapat dicek di:
<https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input>

## Modifikasi Ref

```js
// Menggunakan ref untuk modifikasi ref
playerName.current.value = ''
```

modifikasi ref tidak mengakibatkan komponen dirender

untuk react 19.0 kebawah, kita tidak bisa mempassing langsung ref dengan props, kita harus menggunakan forwardRef, tetapi untuk diatas 19.0, kita bisa
