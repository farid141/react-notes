# Penjelasan

Terdapat beberapa cara dalam melakukan styling ke element ketika menggunakan react.

## 1. vanilla-css (NON-Scoped)

untuk conditional-styling dinamis, bisa memainkan toggle class (ternary-operator) pada komponen.

## 2. Inline-styling (scoped)

menggunakan atribut `style` pada element dalam jsx yang berisi object styling css:

- string -> style={{'text-align': 'center'}}
- camelCase -> style={{textAlign: 'center'}}

Dapat pula dituliskan

## 3. CSS modules (scoped)

1. Buat CSS dalam ([filename].module.css)
2. Import secara default dari nama css tersebut ke komponen.

Import tersebut akan berisi object dengan atribut class-selector yang dapat digunakan.

```jsx
import classes from "test.module.css";

<div className={classes.paragraph, classes.classSelector}></div>;
```

kebab-case pada classname selector bisa diakses dengan camelCase

## 4. 3rd-party-package "styled-components" (Not-recommend)

Merupakan CSS-in-JS. Membuat sebuah komponen kontainer melalui styled

```jsx
import styled from 'styled-components';

const MyButton = styled.button`color: red;`;

// Hasil
function MyButton(props) {
  return <button style={{ color: 'red' }} {...props} />;
}
```

## 5. TailwindCSS (Scoped)

styling menggunakan attribut className ke element secara langsung
