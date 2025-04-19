# Penjelasan

prop adalah parameter seperti attribute ketika memanggil komponen yang berisi data berupa variable/function/jsx

# Passing JSX
<Komponen
props={
	<div><div>

}
>

# Jika komponen sebagai wrapper, kita dapat pass special props 'children'
<Komponen>
{children}
</Komponen>


# Props destructuring
mengambil variabel lain dan mengumpulkannya dalam satu object
export default function Komponen({children, ...props}){
	return (
		<div {props}></div>
	)
}


Passing wrapper
pada saat memanggil komponen:
1. built-in element: ButtonWrapper="menu"
2. custom element: ButtonWrapper={Section}

# Lifting state up

kita dapat mempassing fungsi ke komponen yang biasanya akan untuk dipanggil dalam komponen ketika terjadi sebuah aksi terhadap elemen didalamnya.

Fungsi tersebut, memiliki akses ke komponen parentnya, sehingga dapat memodifikasi variabel di komponen parent