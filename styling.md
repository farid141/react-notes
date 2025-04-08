# vanilla-css (NON-Scoped)

untuk conditional-styling dinamis, bisa memainkan toggle class (ternary-operator) pada komponen

# Inline-styling (scoped)

menggunakan atribut `style` pada element dalam jsx yang berisi object styling css:

- string -> style={{'text-align': 'center'}}
- camelCase -> style={{textAlign: 'center'}}

Dapat pula dituliskan

# css modules ([filename].module.css) (scoped)

Import secara default dari nama css tersebut ke komponen. Hasil import akan berisi object dengan atribut class-selector yang dapat digunakan.

```jsx
import classes from "test.module.css";

<div className={classclasses.paragraph}></div>;
```

4. 3rd-party-package "styled-components"

Membuat sebuah komponen kontainer

```jsx
import {style} from styled-components

const ControlContainer = style.div`
//format atribut css pada file .css
```

5. TailwindCSS
   styling menggunakan class

> SCOPED = hanya ke komponen tersebut
> NON-SCOPED = Berdampak ke child
