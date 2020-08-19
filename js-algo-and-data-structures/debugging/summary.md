* `console.log()`: useful tool for debugging.
* `console.clear()`: clear the console.

## Use typeof to Check the Type of a Variable

```js
console.log(typeof ""); // outputs "string"
console.log(typeof 0); // outputs "number"
console.log(typeof []); // outputs "object"
console.log(typeof {}); // outputs "object"
```

* recognize six primitive(immutable) data type:`Boolean`, `Null`, `Undefined`, `Number`, `String`, and `Symbol`, and one type for mutable items: `Object`

> arrays are technically a type of object

## Off-By-One Error (OBOE)

reference: https://stackoverflow.com/questions/2939869/what-is-an-off-by-one-error-and-how-do-i-fix-it

```js
let alphabet = "abcdefghijklmnopqrstuvwxyz";
let len = alphabet.length;
for (let i = 0; i <= len; i++) {
  // loops one too many times at the end
  console.log(alphabet[i]);
}
for (let j = 1; j < len; j++) {
  // loops one too few times and misses the first character at index 0
  console.log(alphabet[j]);
}
for (let k = 0; k < len; k++) {
  // Goldilocks approves - this is just right
  console.log(alphabet[k]);
}
```

