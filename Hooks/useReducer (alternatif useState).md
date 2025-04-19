# Penjelasan

Merupakan alternatif/pengganti dari useState() untuk state manajemen yang lebih rapi. Dapat digunakan pada context API, ataupun redux.

```javascript
const counterReducer = (state, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return { count: state.count + 1 };
    case 'DECREMENT':
      return { count: state.count - 1 };
    default:
      return state;
  }
};

const [counterState, counterDispatch] = useReducer(
  counterReducer,
  {
    count: 0,
  }
);
```

## Updating state

Dalam mengubah state yang ditulis reducer, dilakukan dengan memanggil dispatch disertai dengan obj berisi type dan payload opsional

```javascript
counterDispatch({
  type: 'INCREMENT',
})
