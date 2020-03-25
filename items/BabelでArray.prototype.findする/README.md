babelで`Array.prototype.find`しようとするとTypeErrorになってしまう。

```js
[ 1, 2, 3 ].find((x) => x >= 2);
// expected
// => 2
// actual
// => Uncaught TypeError: [1,2,3].find is not a function
```

なので代わりにこっちを使えとのこと。`Array.find(arr, callback)`

```js
Array.find([ 1, 2, 3 ], (x) => x >= 2);
// => 2
```

[`Array.prototype.find` doesn't work in the runtime · Issue #892 · babel/babel](https://github.com/babel/babel/issues/892)
