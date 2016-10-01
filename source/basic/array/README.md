# Arrayパターン

## Arrayの要素を全削除

```js
var array = [1,2,3];
array.length = 0;
console.log(array[0] === undefined); // => true
```

## Arrayのコピー

Shallow copyの流派concatとsliceがある

```js
var array = [1,2,3];
var copyC = array.concat()
var copyS = array.slice();
console.log(array !== copyC); // => true
console.log(array !== copyS); // => true
console.log(copyC !== copyS); // => true
```

## new Array join

`new Array(len)` で指定した`length`の**疎の配列**を作る事ができます。
しかし、この配列の要素は`undefined`が値として入っているわけではありません。
単純に何も入ってないから `array[0]` とした時にプロパティがないため `undefined`が返ってきているだけです。

```js
var array = new Array(10);
console.log(array.length === 10);// => true
console.log(array[0] === undefined); // => true
// hasOwnPropertyでプロパティを持っているかで確認できる
var a = [undefined];
var b = new Array(1);
console.log(a.hasOwnProperty(0)); // => true
console.log(b.hasOwnProperty(0)); // => false
```

これにより`new Array`では配列中の値がないので`Array#map`などが意図した挙動にはなりません
`Array#map`などは配列中の値がない添字をスキップします。

```js
var array = new Array(10).map((item. index) => {
  return index
});
console.log(array[0] === undefined);// => false
```

そのため、これを回避する場合は明示的に値を入れた配列を使うか、
`Array.from`を使うことで**疎の配列**も扱えます。

明示的に値を埋める、いわゆる0埋めのような操作は`Array#fill`を使うのが簡単です。

```js
var array = new Array(10).fill(0).map((item. index) => {
  return index
});
console.log(array[9] === 9);// => true
```

`Array.from`メソッドはArray-likeやiterableなオブジェクトから新しく配列を作る静的メソッドです。

- [Array.from() - JavaScript | MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/from "Array.from() - JavaScript | MDN")

先ほどの`new Array`で作った疎の配列もlengthは持っているので、for文などで走査することはできます。
`Array.from`は、`arguments`のようなArray-likeや疎の配列も、意図したように列挙できる`Array#map`のような仕組みを持っています。

```js
var array = Array.from(new Array(10), (item. index) => {
  return index
});
console.log(array[9] === 9);// => true
```

他にも、Iterableを配列にできるので、Mapなどを配列にしたい場合に使えます。

```js
var map = new Map([[1, 2], [2, 4], [4, 8]]);
console.log(Array.from(map));// => [[1, 2], [2, 4], [4, 8]]
```

これは、Spread Operator（`...`）を使うことでも同様の事が行なえます。
`Array.from`は第二引数でマッピング方法を指定できるのでより柔軟な処理が書けるという違いがあります。

```js
var map = new Map([[1, 2], [2, 4], [4, 8]]);
console.log(...map);// => [[1, 2], [2, 4], [4, 8]]
```

## flatten

配列の配列を、配列にfattenしたというケース

`[[1], [2], [3]]` => `[1, 2, 3]`

## map => reduce

## entriesで何か

## values?

## flatten

## indexOf => findIndex

## indexOf !== -1 => includes

## splice => ...

immutable版

## some

## every

## location.split().pop()

## new Array and fill 

http://qiita.com/s-shin/items/88b2b6d4387312fe000a

## 交換

var [a, b] = [b, a];

http://es6-features.org/#ArrayMatching
