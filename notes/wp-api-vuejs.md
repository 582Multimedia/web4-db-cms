# Interfacing Wordpress API with Vue.js

## Advanced styling

```bash
npm install -D sass-embedded
```

We'll use SASS to help organize and structure our css better.

From now on, we'll use this for our style tag:

```html
<style lang="scss" scoped>
</style>
```

We will quickly explore some SASS syntax, [click here to see documentation](https://sass-lang.com/documentation/syntax/).

Quick example of wordpress info

```html
<style lang="scss" scoped>
.wordpress {
  background-color: #f0f0f0;
  padding: 20px;
  border-radius: 5px;

  & :deep(*) {
    margin: 0 !important;
    padding: 0 !important;
    box-sizing: border-box;
  }

  & :deep(h1) {
    font-size: 2.5em !important;
    margin-bottom: 1.5rem !important;
    font-weight: 700 !important;
  }

  & :deep(h2),
  & :deep(h3),
  & :deep(h4),
  & :deep(h5),
  & :deep(h6) {
    font-size: 2em !important;
    margin-bottom: 1rem !important;
    font-weight: 700 !important;
  }

  & :deep(p) {
    max-width: 35rem;
    font-size: 1em !important;
    margin-bottom: 1rem !important;
  }

  & :deep(img) {
    max-width: 100%;
    height: auto;
  }
}
</style>
```
