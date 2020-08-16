## var vs let

* overwriting problem

* ```let``` : the same name can only be declared once.

  ```javascript
  let camper = 'James';
  let camper = 'David'; // throws an error
  ```

* ```"use strict"``` : enables Strict Mode which catches common coding mistakes and "unsafe" actions.

  ```javascript
  "use strict";
  x = 3.14; // throws an error because x is not declared
  ```

* When you declare a variable with the `let` keyword inside a block, statement, or expression, its scope is limited to that block, statement, or expression.

* ```js
  'use strict';
  let printNumTwo;
  for (let i = 0; i < 3; i++) {
    if (i === 2) {
      printNumTwo = function() {
        return i; // value
      };
    }
  }
  console.log(printNumTwo());
  // returns 2
  console.log(i);
  // returns "i is not defined"
  ```

## const

* ```let``` features + read-only

  ```js
  "use strict";
  const FAV_PET = "Cats";
  FAV_PET = "Dogs"; // returns error
  ```

* ```const``` only prevents reassignment of the variable identifier. (can mutate)

  ```js
  "use strict";
  const s = [5, 6, 7];
  s = [1, 2, 3]; // throws error, trying to assign a const
  s[2] = 45; // works just as it would with an array declared with var or let
  console.log(s); // returns [5, 6, 45]
  ```

* To ensure your data doesn't change, JS provides ```Object.freeze```

  ```js
  let obj = {
    name:"FreeCodeCamp",
    review:"Awesome"
  };
  Object.freeze(obj);
  obj.review = "bad"; // will be ignored. Mutation not allowed
  obj.newProp = "Test"; // will be ignored. Mutation not allowed
  console.log(obj); 
  // { name: "FreeCodeCamp", review:"Awesome"}
  ```

## Arrow Functions

* Anonymous functions

  ```js
  const myFunc = function() {
    const myVar = "value";
    return myVar;
  }
  ```

* Arrow functions 

  ```js
  const myFunc = () => {
    const myVar = "value";
    return myVar;
  }
  ```

* no function body, and only a return value; omit the keyword ```return```.

  ```js
  const myFunc = () => "value";
  ```

* with parameters

  ```js
  // doubles input value and returns it
  const doubler = (item) => item * 2;
  ```

  ```js
  // the same function, without the argument parentheses
  const doubler = item => item * 2;
  ```

  ```js
  // multiplies the first input value by the second and returns it
  const multiplier = (item, multi) => item * multi;
  ```

* Default Parameters

  ```js
  const greeting = (name = "Anonymous") => "Hello " + name;
  
  console.log(greeting("John")); // Hello John
  console.log(greeting()); // Hello Anonymous
  ```

* Rest Parameter

  ```js
  function howMany(...args) {
    return "You have passed " + args.length + " arguments.";
  }
  console.log(howMany(0, 1, 2)); // You have passed 3 arguments.
  console.log(howMany("string", null, [1, 2, 3], { })); // You have passed 4 arguments.
  ```

## Spread Operator

* `...arr` returns an unpacked array. In other words, it *spreads* the array. However, the spread operator only works in-place, like in an argument to a function or in an array literal. 

  ```js
  var arr = [6, 89, 3, 45];
  var maximus = Math.max.apply(null, arr); // returns 89
  ```

  ```js
  const arr = [6, 89, 3, 45];
  const maximus = Math.max(...arr); // returns 89
  ```

  ```js
  const spreaded = ...arr; // will throw a syntax error
  ```

## Destructing Assignment

* neatly assigning values taken directly from an object.

  ```js
  const user = { name: 'John Doe', age: 34 };
  
  const name = user.name; // name = 'John Doe'
  const age = user.age; // age = 34
  
  /* ES6 */
  const { name, age } = user;
  // name = 'John Doe', age = 34
  ```

* assign a new variable name when extracting values.

  ```js
  const user = { name: 'John Doe', age: 34 };
  
  const { name: userName, age: userAge } = user;
  // userName = 'John Doe', userAge = 34
  ```

* Destructuring Assignment to Assign Variables from Nested Objects

  ```js
  const user = {
    johnDoe: { 
      age: 34,
      email: 'johnDoe@freeCodeCamp.com'
    }
  };
  
  const { johnDoe: { age, email }} = user;
  const { johnDoe: { age: userAge, email: userEmail }} = user;
  ```

* Destructuring Assignment to Assign Variables from Arrays

  * spread operator unpacks all contents of an array into a comma-separated list.

  * Destructuring array  cannot pick or choose which elements you want to assign to variables

    ```js
    const [a, b] = [1, 2, 3, 4, 5, 6];
    console.log(a, b); // 1, 2
    ```

    ```js
    const [a, b,,, c] = [1, 2, 3, 4, 5, 6];
    console.log(a, b, c); // 1, 2, 5
    ```

* Destructuring Assignment with the Rest Parameter to Reassign Array Elements
  similar to``` Array.prototype.slice()```

  ```js
  const [a, b, ...arr] = [1, 2, 3, 4, 5, 7];
  console.log(a, b); // 1, 2
  console.log(arr); // [3, 4, 5, 7]
  ```

* Use Destructuring Assignment to Pass an Object as a Function's Parameters

  ```js
  const profileUpdate = (profileData) => {
    const { name, age, nationality, location } = profileData;
    // do something with these variables
  }
  ```

  ```js
  const profileUpdate = ({ name, age, nationality, location }) => {
    /* do something with these fields */
  }
  ```

## Template Literals

* allow you to create multi-line strings and to use string interpolation features to create strings.

  ```js
  const person = {
    name: "Zodiac Hasbro",
    age: 56
  };
  
  // Template literal with multi-line and string interpolation
  const greeting = `Hello, my name is ${person.name}!
  I am ${person.age} years old.`;
  
  console.log(greeting); // prints
  // Hello, my name is Zodiac Hasbro!
  // I am 56 years old.
  ```

* Write concise object literal declarations using object property shorthand.

  ```js
  const getMousePosition = (x, y) => ({ x, y });
  ```

## Concise Declarative Functions
* ES5
```js
const person = {
  name: "Taylor",
  sayHello: function() {
    return `Hello! My name is ${this.name}.`;
  }
};
```
* ES6
```js
const person = {
  name: "Taylor",
  sayHello() {
    return `Hello! My name is ${this.name}.`;
  }
};
```

## Class syntax to define a constructor function

* not a full-fledged class-based implementation of an object-oriented paradigm

* ES5

  ```js
  var SpaceShuttle = function(targetPlanet){
    this.targetPlanet = targetPlanet;
  }
  var zeus = new SpaceShuttle('Jupiter');
  ```

* ES6

  ```js
  class SpaceShuttle {
    constructor(targetPlanet) {
      this.targetPlanet = targetPlanet;
    }
  }
  const zeus = new SpaceShuttle('Jupiter');
  ```

## getters and setters

```js
class Book {
  constructor(author) {
    this._author = author;
  }
  // getter
  get writer() {
    return this._author;
  }
  // setter
  set writer(updatedAuthor) {
    this._author = updatedAuthor;
  }
}
const lol = new Book('anonymous');
console.log(lol.writer);  // anonymous
lol.writer = 'wut';
console.log(lol.writer);  // wut
```

* convention: precede the name of a private variable with an underscore.

## Module

* For more modular, clean, and maintainable

```js
<script type="module" src="filename.js"></script>
//For now, we can use import and export fetures
```

* This involves exporting parts of a file for use in one or more other files, and importing the parts you need, where you need them.

* export to share a code block

  ```js
  export const add = (x, y) => {
    return x + y;
  }
  ```

  ```js
  const add = (x, y) => {
    return x + y;
  }
  
  export { add };
  ```

* Using import

  * ```import``` allow you to choose which part of a file or module to load.

    ```js
    import { add } from './math_functions.js';
    ```

    ```js
    import * as myMathModule from "./math_functions.js";
    // will create myMathModule object
    myMathModule.add(2,3);
    myMathModule.subtract(5,3);
    ```

* Create an Export fallback with export default

  * ```export default```: used to declare a fallback value for a module or file, you can only have one value be a default export in each module or file.

    ```js
    // named function
    export default function add(x, y) {
      return x + y;
    }
    
    // anonymous function
    export default function(x, y) {
      return x + y;
    }
    ```

  * Additionally, you cannot use `export default` with `var`, `let`, or `const`

* Import a default export

  ```js
  import add from "./math_functions.js";
  ```

  * `add` here is simply a variable name for whatever the default export of the `math_functions.js` file is

## Promise

* you use it to make a promise to do something, usually asynchronously.
* When the task completes, you either fulfill your promise or fail to do so
* `Promise` is a constructor function

```js
const myPromise = new Promise((resolve, reject) => {

});
```

* Complete a promise with resolve and reject

  * three states: ```pending```, ```fulfilled```, ```rejected```
  * ```resolve```: when you want your promise to succeed.
  * ```reject``` when you want it to fail.

  ```js
  const myPromise = new Promise((resolve, reject) => {
    if(condition here) {
      resolve("Promise was fulfilled");
    } else {
      reject("Promise was rejected");
    }
  });
  ```

* Handle a fulfilled promise with then
  * ```then``` method is executed immediately after your promise is fulfilled with ```resolve```

  ```js
  myPromise.then(result => {
    // do something with the result.
  });
  ```

  * `result` comes from the argument given to the `resolve` method.

* Handle a rejected promise with catch
  * ```catch```: the method used when your promise has been rejected.

  ```js
  myPromise.catch(error => {
    // do something with the error.
  });
  ```
  * ```error```: passed in to the reject method.