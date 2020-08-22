- [Create an Object](#create-an-object)
- [this Keyword](#this-keyword)
- [Define a Constructor Function](#define-a-constructor-function)
- [Use a Constructor to Create Objects](#use-a-constructor-to-create-objects)
- [Verify an Object's Constructor with instanceof](#verify-an-object-s-constructor-with-instanceof)
- [Own Properties](#own-properties)
- [Prototype Properties](#prototype-properties)
- [the Constructor Property](#the-constructor-property)
- [Where an Object's Prototype Comes From](#where-an-object-s-prototype-comes-from)
- [Prototype Chain](#prototype-chain)
- [Don't Repeat Yourself(DRY) - Inheritance](#don-t-repeat-yourself-dry----inheritance)
- [Inherit Behaviors from a Supertype](#inherit-behaviors-from-a-supertype)
- [Reset an Inherited Constructor Property](#reset-an-inherited-constructor-property)
- [Add Methods After Inheritance](#add-methods-after-inheritance)
- [Override Inherited Methods](#override-inherited-methods)
- [Use a Mixin to Add Common Behavior Between Unrelated Objects](#use-a-mixin-to-add-common-behavior-between-unrelated-objects)
- [Use Closure to Protect Properties Within an Object from Being Modified Externally](#use-closure-to-protect-properties-within-an-object-from-being-modified-externally)
- [the Immediately Invoked Function Expression (IIFE)](#the-immediately-invoked-function-expression--iife-)
- [Use an IIFE to Create a Module](#use-an-iife-to-create-a-module)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>

## Create an Object

* properties

  ```js
  let duck = {
    name: "Aflac",
    numLegs: 2
  };
  console.log(duck.name);
  // This prints "Aflac" to the console
  ```

* Method

  ```js
  let duck = {
    name: "Aflac",
    numLegs: 2,
    sayName: function() {return "The name of this duck is " + duck.name + ".";}
  };
  duck.sayName();
  // Returns "The name of this duck is Aflac."
  ```

## this Keyword

* Using variable name has a pitfall that if the variable name changes, any code referencing the original name would need to be updated as well.

  * To avoid this, use `this` keyword.

    ```js
    let duck = {
      name: "Aflac",
      numLegs: 2,
      sayName: function() {return "The name of this duck is " + this.name + ".";}
    };
    ```

## Define a Constructor Function

* Constructors are functions that create new objects. (like a blueprint)

```js
function Bird() {
  this.name = "Albert";
  this.color = "blue";
  this.numLegs = 2;
}
```

* Conventions

  * Defined with a capitalized name
  * Use `this`, `this` refers to the new object it will create.
  * Define properties and behaviors instead of returning a value as other functions might.

* To receive Arguments

  ```js
  function Bird(name, color) {
    this.name = name;
    this.color = color;
    this.numLegs = 2;
  }
  ```

## Use a Constructor to Create Objects

```js
function Bird() {
  this.name = "Albert";
  this.color  = "blue";
  this.numLegs = 2;
  // "this" inside the constructor always refers to the object being created
}

let blueBird = new Bird();
blueBird.name; // => Albert
blueBird.color; // => blue
blueBird.numLegs; // => 2
blueBird.name = 'Elvira';
blueBird.name; // => Elvira
```

* Without the `new` operator, `this` inside the constructor would not point to the newly created object, giving unexpected results.

## Verify an Object's Constructor with instanceof

* `instanceof` allow you to compare an object to a constructor, returning `true` and `false` based on whether or not that object was created with the constructor.

```js
let Bird = function(name, color) {
  this.name = name;
  this.color = color;
  this.numLegs = 2;
}

let crow = new Bird("Alexis", "black");

crow instanceof Bird; // => true
```

```js
let canary = {
  name: "Mildred",
  color: "Yellow",
  numLegs: 2
};

canary instanceof Bird; // => false
```

## Own Properties

* Each objects has its own separate copy of these properties.

```js
let ownProps = [];

for (let property in duck) {
  if(duck.hasOwnProperty(property)) {
    ownProps.push(property);
  }
}

console.log(ownProps); // prints [ "name", "numLegs" ]
```

## Prototype Properties

* To reduce a duplicated variables(property), use `prototype`

* Properties in the `prototype` are shared among ALL instance of a constructor.

* How to add

  ```js
  Bird.prototype.numLegs = 2;
  console.log(duck.numLegs);  // prints 2
  console.log(canary.numLegs);  // prints 2
  ```

* Nearly every object in JavaScript has a `prototype` property which is part of the constructor function that created it.

* A more efficient way is to set the `prototype` to a new object that already contains the properties.

  ```js
  Bird.prototype = {
    numLegs: 2, 
    eat: function() {
      console.log("nom nom nom");
    },
    describe: function() {
      console.log("My name is " + this.name);
    }
  };
  ```

* Side effect of manually setting the prototype

  *  It erases the `constructor` property.

    ```js
    duck.constructor === Bird; // false -- Oops
    duck.constructor === Object; // true, all objects inherit from Object.prototype
    duck instanceof Bird; // true, still works
    ```

  * To fix this, whenever a prototype is manually set to a new object, remember to define the `constructor` property.

    ```js
    Bird.prototype = {
      constructor: Bird, // define the constructor property
      numLegs: 2,
      eat: function() {
        console.log("nom nom nom");
      },
      describe: function() {
        console.log("My name is " + this.name); 
      }
    };
    ```

## the Constructor Property

* `constructor` property is a reference to the constructor function that created the instance.

```js
let duck = new Bird();
let beagle = new Dog();

console.log(duck.constructor === Bird);  //prints true
console.log(beagle.constructor === Dog);  //prints true
```

## Where an Object's Prototype Comes From

* An object(instance) inherits its `prototype` directly from the constructor functions that created it.

```js
function Bird(name) {
  this.name = name;
}

let duck = new Bird("Donald"); // duck inherits its prototype from the Bird
```

```js
Bird.prototype.isPrototypeOf(duck);
// returns true
```

## Prototype Chain

* An object's `prototype` itself is an object. Thus a `prototype` can have its own `prototype`

  ```js
  function Bird(name) {
    this.name = name;
  }
  
  typeof Bird.prototype; // yields 'object'
  ```

  ```js
  Object.prototype.isPrototypeOf(Bird.prototype); // returns true
  // the prototype of Bird.prototype is Object.prototype.
  ```

The `hasOwnProperty` method is defined in `Object.prototype`, which can be accessed by `Bird.prototype`, which can then be accessed by `duck`. This is an example of the `prototype` chain. In this `prototype` chain, `Bird` is the `supertype` for `duck`, while `duck` is the `subtype`. `Object` is a `supertype` for both `Bird` and `duck`. `Object` is a `supertype` for all objects in JavaScript. Therefore, any object can use the `hasOwnProperty` method.

## Don't Repeat Yourself(DRY) - Inheritance

```js
Bird.prototype = {
  constructor: Bird,
  describe: function() {
    console.log("My name is " + this.name);
  }
};

Dog.prototype = {
  constructor: Dog,
  describe: function() {
    console.log("My name is " + this.name);
  }
};
```

* To follow the DRY principle by creating a `supertype` called `Animal`

  ```js
  function Animal() { };
  
  Animal.prototype = {
    constructor: Animal, 
    describe: function() {
      console.log("My name is " + this.name);
    }
  };
  Bird.prototype = {
    constructor: Bird
  };
  
  Dog.prototype = {
    constructor: Dog
  };
  ```

## Inherit Behaviors from a Supertype

* inheritance

  * First step: making a new instance of `Animal`

  ```js
  function Animal() { }
  Animal.prototype.eat = function() {
    console.log("nom nom nom");
  };
  let animal = Object.create(Animal.prototype);
  animal.eat(); // prints "nom nom nom"
  animal instanceof Animal; // => true
  ```

  ```js
  Bird.prototype = Object.create(Animal.prototype);
  ```
  * `Object.create(obj)` creates a new object, and sets `obj` as the new object's `prototype`
  * Second step: set the `prototype` of the subtype to be and instance of `Animal`

  ```js
  Bird.prototype = Object.create(Animal.prototype);
  let duck = new Bird("Donald");
  duck.eat(); // prints "nom nom nom"
  ```

## Reset an Inherited Constructor Property

```js
function Bird() { }
Bird.prototype = Object.create(Animal.prototype);
let duck = new Bird();
duck.constructor // function Animal(){...}
```

* `duck` and all instances of `Bird` should show that they were constructed by `Bird` and not `Animal`

  ```js
  Bird.prototype.constructor = Bird;
  duck.constructor // function Bird(){...}
  ```

## Add Methods After Inheritance

```js
function Animal() { }
Animal.prototype.eat = function() {
  console.log("nom nom nom");
};
function Bird() { }
Bird.prototype = Object.create(Animal.prototype);
Bird.prototype.constructor = Bird;

Bird.prototype.fly = function() {
  console.log("I'm flying!");
};

let duck = new Bird();
duck.eat(); // prints "nom nom nom"
duck.fly(); // prints "I'm flying!"
```

## Override Inherited Methods

* by adding a method to `ChildObject.prototype` using the same method name as the one to override

```js
function Animal() { }
Animal.prototype.eat = function() {
  return "nom nom nom";
};
function Bird() { }

// Inherit all methods from Animal
Bird.prototype = Object.create(Animal.prototype);

// Bird.eat() overrides Animal.eat()
Bird.prototype.eat = function() {
  return "peck peck peck";
};
```

* How JavaScript looks for the method on `duck's` `prototype` chain:
  * duck => Is eat() defined here? No.
  * Bird => Is eat() defined here? => Yes. Execute it and stop searching.
  * Animal => eat() is also defined, but JavaScript stopped searching before reaching this level.
  * Object => JavaScript stopped searching before reaching this level.

## Use a Mixin to Add Common Behavior Between Unrelated Objects

* Inheritance does not work well for unrelated objects like `Bird` and `Airplane`. They can both fly, but a `Bird` is not a type of `Airplane` and vice versa.
* A mixin allows other object to use a collection of functions.

```js
let flyMixin = function(obj) {
  obj.fly = function() {
    console.log("Flying, wooosh!");
  }
};
let bird = {
  name: "Donald",
  numLegs: 2
};

let plane = {
  model: "777",
  numPassengers: 524
};

flyMixin(bird);
flyMixin(plane);
// assigns the fly function to each object.
bird.fly(); // prints "Flying, wooosh!"
plane.fly(); // prints "Flying, wooosh!"
```

## Use Closure to Protect Properties Within an Object from Being Modified Externally

* The simplest way to make this public property private is by creating a variable within the constructor function
* This changes the scope of that variable to be within the constructor function versus available globally. 
* This way, the variable can only be accessed and changed by methods also within the constructor function.

```js
function Bird() {
  let hatchedEgg = 10; // private variable

  /* publicly available method that a bird object can use */
  this.getHatchedEggCount = function() { // privileged method
    return hatchedEgg;
  };
}
let ducky = new Bird();
ducky.getHatchedEggCount(); // returns 10
```

* In JavaScript, a function always has access to the context in which it was created. This is called `closure`.

## the Immediately Invoked Function Expression (IIFE)

* A common pattern in JavaScript is to execute a function as soon as it is declared

```js
(function () {
  console.log("Chirp, chirp!");
})(); // this is an anonymous function expression that executes right away
// Outputs "Chirp, chirp!" immediately
```

* Note that the function has no name and is not stored in a variable. 
* This pattern is known as an *immediately invoked function expression* or *IIFE*.

## Use an IIFE to Create a Module

* IIFE is often used to group related functionality into a single object or module

```js
let motionModule = (function () {
  return {
    glideMixin: function(obj) {
      obj.glide = function() {
        console.log("Gliding on the water");
      };
    },
    flyMixin: function(obj) {
      obj.fly = function() {
        console.log("Flying, wooosh!");
      };
    }
  }
})(); // The two parentheses cause the function to be immediately invoked
```

* Benefit

  * The advantage of the IIFE is that any `var`s declared inside it are inaccessible to the outside world

    ```js
    var batman = (function () {
        var identity = "Bruce Wayne";
    
        return {
            fightCrime: function () {
                console.log("Cleaning up Gotham.");
            },
    
            goCivilian: function () {
                console.log("Attend social events as " + identity);
            }
        };
    })();
    
    // Outputs: undefined
    console.log(batman.identity);
    
    // Outputs: "Attend social events as Bruce Wayne"
    batman.goCivilian();
    ```

  * As you can see, we were able to use the IFFE's return value to make `batman`'s utility functions publicly accessible. And at the same time we were able to ensure that `batman`'s `identity` remains a secret from any clowns who want to mess with it.

* Reference

  * [http://adripofjavascript.com/blog/drips/understanding-the-module-pattern-in-javascript.html#:~:text=The%20advantage%20of%20the%20IIFE,just%20like%20any%20other%20function.](http://adripofjavascript.com/blog/drips/understanding-the-module-pattern-in-javascript.html#:~:text=The advantage of the IIFE,just like any other function.)