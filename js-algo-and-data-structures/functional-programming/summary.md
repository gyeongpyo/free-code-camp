## Intro

- Functions are independent from the state of the program or global variables. They only depend on the arguments passed into them to make a calculation
- Functions try to limit any changes to the state of the program and avoid changes to the global objects holding data
- Functions have minimal side effects in the program

> INPUT -> PROCESS -> OUTPUT

1. Isolate functions - there is no dependence on the state of program.
2. Pure functions - the same input always gives the same output.
3. Functions with limited side effect = any changes to the state of the program outside the function are carefully controlled.

## Terminology

* *Callbacks*: the functions that are slipped or passed into another function to decide the invocation of that function.
* *First class functions*: functions that can be assigned to a variable, passed into another function, or returned from another function just like any other normal value, (In JS, all functions are first class func.)

* *Higher order functions*: take a function as an argument, or return a function as a return value 

* *Lambda*: When the functions are passed in to another function or returned from another function, then those functions which gets passed in or returned.

## the Hazards of Using Imperative Code

* functional programming is a form of declarative programming. You tell the computer what you want done by calling a method or function.
* Instead of using the `for` loop mentioned above, you could call the `map` method which handles the details of iterating over an array.

## Avoid Mutations and Side Effects Using Functional Programming

* It's easier to prevent bugs knowing that your functions don't change anything, including the function arguments or any global variable.
* *mutation*: changing or altering things 
* *side effect*: the outcome (by mutation)

## Pass Arguments to Avoid External Dependence in a Function

* Another principle of functional programming is to always declare your dependencies explicitly. This means if a function depends on a variable or object being present, then pass that variable or object directly into the function as an argument.

## Use the map Method to Extract Data from an Array

* `Array.prototype.map()`: iterates over each item in an array and returns a new array containing the results of calling the callback function on each element. It does this without mutating the original array.
* Callback functions Parameter
  * First: the current element being processed.
  * Second: the index of that element
  * Third: the array upon which the `map` method was called.

```js
const users = [
  { name: 'John', age: 34 },
  { name: 'Amy', age: 20 },
  { name: 'camperCat', age: 10 }
];

const names = users.map(user => user.name);
console.log(names); // [ 'John', 'Amy', 'camperCat' ]
```

## Use the filter Method to Extract Data from an Array

* `Array.prototype.filter()`: calls a function on each element of an array and returns a new array containing only the elements for which that function returns `true`

* Callback functions parameter
  * First: the current element being processed.
  * Second: the index of that element.
  * Third: the array upon which the `filter` method was called.

```js
const users = [
  { name: 'John', age: 34 },
  { name: 'Amy', age: 20 },
  { name: 'camperCat', age: 10 }
];

const usersUnder30 = users.filter(user => user.age < 30);
console.log(usersUnder30); // [ { name: 'Amy', age: 20 }, { name: 'camperCat', age: 10 } ]
```

## Return Part of an Array Using the slice Method

* It's possible to use to make a copy of the entire array or some consecutive part.

  ```js
  var arr = ["Cat", "Dog", "Tiger", "Zebra"];
  var newArray = arr.slice(1, 3);
  // Sets newArray to ["Dog", "Tiger"]
  ```

## Remove Elements from an Array Using slice Instead of splice

* `splice` method mutates the original array it is called on.
* Using the `slice` method instead of `splice` helps to avoid any array-mutating side effects.

## Combine Two Arrays Using the concat Method

```js
[1, 2, 3].concat([4, 5, 6]);
// Returns a new array [1, 2, 3, 4, 5, 6]
```

* It returns a new array and does not mutate either of the original arrays. On the other hand, `push` adds an item to the end of the same array it is called on, which mutates that array.

## Use the reduce Method to Analyze Data

* The `reduce` method iterates over each item in an array and returns a single value.
* Callback parameter
  * First: the accumulator gets assigned the return value of the callback function from the previous iteration.
  * Second: the current element being processed.
  * Third: the index of that element
  * Fourth: the array upon which `reduce` is called.

* In addition to the callback function, `reduce` has an additional parameter which takes an initial value for the accumulator. If omitted, then the first iteration is skipped and the second iteration gets passed the first element of the array as the accumulator.

```js
const users = [
  { name: 'John', age: 34 },
  { name: 'Amy', age: 20 },
  { name: 'camperCat', age: 10 }
];

const sumOfAges = users.reduce((sum, user) => sum + user.age, 0);
console.log(sumOfAges); // 64
```

```js
const users = [
  { name: 'John', age: 34 },
  { name: 'Amy', age: 20 },
  { name: 'camperCat', age: 10 }
];

const usersObj = users.reduce((obj, user) => {
  obj[user.name] = user.age;
  return obj;
}, {});
console.log(usersObj); // { John: 34, Amy: 20, camperCat: 10 }
```

## Sort an Array Alphabetically using the sort Method

```js
function ascendingOrder(arr) {
  return arr.sort(function(a, b) {
    return a - b;
  });
}
ascendingOrder([1, 5, 2, 3, 4]);
// Returns [1, 2, 3, 4, 5]

function reverseAlpha(arr) {
  return arr.sort(function(a, b) {
    return a === b ? 0 : a < b ? 1 : -1;
  });
}
reverseAlpha(['l', 'h', 'z', 'b', 's']);
// Returns ['z', 's', 'l', 'h', 'b']
```

## Split a String into an Array Using the split Method

* `split`: splits a string into an array of strings.
* It takes an argument for the delimiter, which can be a character to use to break up the string or a regular expression.

```js
var str = "Hello World";
var bySpace = str.split(" ");
// Sets bySpace to ["Hello", "World"]

var otherString = "How9are7you2today";
var byDigits = otherString.split(/\d/);
// Sets byDigits to ["How", "are", "you", "today"]
```

## Combine an Array into a String Using the join Method

```js
var arr = ["Hello", "World"];
var str = arr.join(" "); // delimiter
// Sets str to "Hello World"
```

## Use the every Method to Check that Every Element in an Array Meets a Criteria

* `every`: check if *every* element of array passes a particular test. return a Boolean

```js
var numbers = [1, 5, 8, 0, 10, 11];
numbers.every(function(currentValue) {
  return currentValue < 10;
});
// Returns fals
```

## Use the some Method to Check that Any Elements in an Array Meet a Criteria

* `some` if *any* element of array passes a particular test.

```js
var numbers = [10, 50, 8, 220, 110, 11];
numbers.some(function(currentValue) {
  return currentValue < 10;
});
// Returns true
```

## Introduction to Currying and Partial Application

* The *arity* of a function is the number of arguments it requires.

* Currying a function means to convert a function of N arity into N functions of arity 1.

```js
//Un-curried function
function unCurried(x, y) {
  return x + y;
}

//Curried function
function curried(x) {
  return function(y) {
    return x + y;
  }
}
//Alternative using ES6
const curried = x => y => x + y

curried(1)(2) // Returns 3
```

* This is useful in your program if you can't supply all the arguments to a function at one time. You can save each function call into a variable,

```js
// Call a curried function in parts:
var funcForY = curried(1);
console.log(funcForY(2)); // Prints 3
```

* partial application can be described as applying a few arguments to a function at a time and returning another function that is applied to more arguments

```js
//Impartial function
function impartial(x, y, z) {
  return x + y + z;
}
var partialFn = impartial.bind(this, 1, 2);
partialFn(10); // Returns 13
```



