# localStorage

[mdn reference](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)

The following snippet accesses the current domain's local Storage object and adds a data item to it using Storage.setItem().

```js
localStorage.setItem("myCat", "Tom");
```

The syntax for reading the `localStorage` item is as follows:

```js
const cat = localStorage.getItem("myCat");
```

The syntax for removing the `localStorage` item is as follows:

```js
localStorage.removeItem("myCat");
```

The syntax for removing all the `localStorage` items is as follows:

```js
localStorage.clear();
```
