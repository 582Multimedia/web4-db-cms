# API

## Fetch API

[Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)

[Using the Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)

Basic Fetch example:

```js
async function getData() {
  const url = "https://dummyjson.com/test";
  try {
    const response = await fetch(url);
    if (!response.ok) {
      throw new Error(`Response status: ${response.status}`);
    }

    const json = await response.json();
    console.log(json);
  } catch (error) {
    console.error(error.message);
  }
}
```

## List of APIs

- [10 resources ready for use](https://github.com/Ovi/DummyJSON?tab=readme-ov-file#available-resources) via [DummyJSON](https://dummyjson.com/) [on GitHub](https://github.com/Ovi/DummyJSON)
- [{JSON} Placeholder](https://jsonplaceholder.typicode.com/)
- [REQRES](https://reqres.in/)
- [Sample APIs](http://sampleapis.com/) ***temporary issues / down***
