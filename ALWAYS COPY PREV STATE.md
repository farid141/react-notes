# Penjelasan

Ketika bekerja dengan state, pastikan copy state sebelumnya dengan menggunakan destructuring prev value. Jangan sampai memodifikasi obj/array sebelumnya, karena array dan object pada javascript bersifat mutable. Hal ini dapat menyebabkan bug, unpredicted behavior yang sulit ditrace.

## Adding item to Array

### Adding array value
Using Array spread syntax

```js
setArtists( // Replace the state
  [ // with a new array
    ...artists, // that contains all the old items
    { id: nextId++, name: name } // and one new item at the end
  ]
);

// The code above will add new item to the last index. If you want to add it in the first index, you can do it like this
[
  { id: nextId++, name: name }
  ...artists,
]
```

## Updating Array

### Wrong way
```js
const myNextList = [...myList];
const artwork = myNextList.find(a => a.id === artworkId);
artwork.seen = nextSeen; // Problem: mutates an existing item
setMyList(myNextList);
```

Although the `myNextList` array itself is new, the items themselves are **`the same` as in the original myList array**. So changing artwork.seen changes the original **`artwork item`**. That artwork item is also in yourList, which causes the bug. Bugs like this can be difficult to think about, but thankfully they disappear if you avoid mutating state.

### Solution
```js
setYourList(yourList.map(artwork => {
  if (artwork.id === artworkId) {
    // Create a *new* object with changes
    return { ...artwork, seen: nextSeen };
  } else {
    // No changes
    return artwork;
  }
}));
```

## Removing an array
```js
setArtists(
  artists.filter(a => a.id !== artist.id)
);
```