# Prototype

- - -
## Function's prototype property

- - -
# Prototype

## Function's prototype property

### What is it?

`prototype` is a property of every `Function` object.  
It gets created as soon as you define the function.  
Its initial value is an empty object.  

```js
function foo(a, b) { return a * b; }
typeof foo.prototype // "object"
```

- - -
# Prototype

## Function's prototype property

### What am I doing with that?

This empty object can be augmented with properties and methods.  
They won't have any effect of the `foo()` function itself.  
They'll only be used when you use `foo()` as a _constructor_.  

Inside a function invoked with `new`, the value `this` contains the object to be returned by the constructor.  
Augmenting (adding methods and properties to) this object is the way to add functionality to the object being created.

```js
function Gadget(name, color) {
    this.name = name;
    this.color = color;
    this.whatAreYou = function() {
        return 'I am a ' + this.color + ' ' + this.name;
    }
}
```

- - -
# Prototype

## Function's prototype property

### What am I doing with that?

Methods and properties can be even added to the `prototype` property of the constructor function.

```js
Gadget.prototype.price = 100;
Gadget.prototype.rating = 3;
Gadget.prototype.getInfo = function() {
    return 'Rating: ' + this.rating + ', price: ' + this.price;
};
```

- - -
# Prototype

## Function's prototype property

### What am I doing with that

Instead of adding to the prototype object, you can overwrite the prototype completely.

```js
Gadget.prototype = {
    price: 100,
    rating: 3,
    getInfo: function() {
        return 'Rating: ' + this.rating + ', price: ' + this.price;
    }
};
```

- - -
# Prototype

## Function's prototype property

### Using prototype's stuff

All the methods and properties added to the prototype are directly available as soon as a new object is created using the constructor.

```js
var newtoy = new Gadget('webcam', 'black');
newtoy.name;          // "webcam"
newtoy.color;         // "black"
newtoy.whatAreYou();  // "I am a black webcam"
newtoy.price;         // 100
newtoy.rating;        // 3
newtoy.getInfo();     // "Rating: 3, price: 100"
```

- - -
# Prototype

## Function's prototype property

### The prototype is "live".  

Objects are passed by reference: the prototype is not copied with every new object instance.  

```js
Gadget.prototype.get = function(what) {
     return this[what];
};
newtoy.get('price');   // 100
newtoy.get('color');   // "black"
```

- - -
## The prototype chain

- - -
# Prototype

## The prototype chain

### Accessing an object's property

When trying to access a property of `newtoy`, say `newtoy.name` the JavaScript engine:

1. will look through all of the properties of the object searching for one called name
2. if it finds it, will return its value

```js
newtoy.name  // "webcam"
```

- - -
# Prototype

## The prototype chain

### Accessing a constructor prototype's property

When trying to access a property belonging to `newtoy` constructor's prototype (i.e. the prototype of the `Gadget` function), `rating` for example, the JavaScript engine:

1. will examine all of the properties of newtoy and will not find the one called `rating`
2. then will identify the prototype of the constructor function used to create this object
3. if the property is found in the prototype, this property is used

```js
newtoy.rating  // 3
```

- - -
# Prototype

## The prototype chain

### Understanding the chain

Every object has a `constructor`.  
The prototype of a constructor function is an object.  
So it must have a `constructor` too. Which in turn has a prototype.  
The built-in `Object` object is the highest-level parent, the and of the so called the **prototype chain**.  

```js
newtoy.toString()  // "[object Object]"
```

`newtoy` doesn't have an own `toString()` method and its prototype doesn't either.  
In the end Object's `toString()` will use.

- - -
# Prototype

## The prototype chain

### Overwriting prototype's property with own property

The own property takes precedence over the prototype's.

```js
function Gadget(name) {
     this.name = name;
}

Gadget.prototype.name = 'foo';   // "foo"
var toy = new Gadget('camera');>

toy.name;                        // "camera"

delete toy.name;
toy.name;                        // "foo"

toy.name = 'camera';
toy.name;                        // "camera"
```

- - -
## Useful methods

- - -
# Prototype

## Useful methods

### `Object.hasOwnProperty(prop)`

A `for-in` loop iterates over all properties including those of the prototype.

```js
var g = new Gadget('puppet', 'pink');

for (var p in g) {
  console.log(p);
}

//name
//color
//whatAreYou
//price
//rating
//getInfo
```

- - -
# Prototype

## Useful methods

### `Object.hasOwnProperty(prop)`

Use `hasOwnProperty()` to test if a property belongs to object.

```js
var g = new Gadget('puppet', 'pink');

for (var p in g) {
  if (g.hasOwnProperty(p)) {
    console.log(p);
  }
}

//name
//color
//whatAreYou
```

- - -
# Prototype

## Useful methods

### `Object.isPrototypeOf(obj)`

Every object gets the `isPrototypeOf()` method.  
This method tells whether that specific object is used as a prototype of another object.

```js
var monkey = {
    hair: true,
    feeds: 'bananas',
    breathes: 'air'
};

function Human(name) {
    this.name = name;
}

Human.prototype = monkey;

var george = new Human('George');

monkey.isPrototypeOf(george)   // true
```

- - -
## Some prototype gotchas

- - -
# Prototype

## Some prototype gotchas

### `prototype.constructor` is not reliable

It could be simply overwritten.  
JavaScript engine access object's prototype through a secret link.  
Some engines expose this link as a `__proto__` properties.  

> #### Forbidden!
>
> Even when exposed never use secret `__proto__` property.
> It's no standard: think it's there only for learning purpose.

- - -
# Prototype

## Some prototype gotchas

### `prototype.constructor` is not reliable

```js
var monkey = {
    feeds: 'bananas',
    breathes: 'air'
};

function Human() {}
Human.prototype = monkey;

var developer = new Human();
developer.feeds = 'pizza';
developer.hacks = 'JavaScript';

developer.hacks  // "JavaScript", found in the object
developer.feeds  // "pizza", found in the object

developer.breathes // "air", found in the prototype

developer.constructor = 'junk'
typeof developer.constructor.prototype // "undefifined" 
// a string object haven't prototype property

developer.breathes  // "air"
// engine uses imutable __proto__ secret link
```
- - -
# Prototype

## Some prototype gotchas

### `prototype.constructor` is not reliable

`__proto__` is not the same as `prototype`:

* `__proto__` is a property of the instances
* `prototype` is a property of the constructor functions.

 #### Example

```js
typeof developer.__proto__   // "object"
typeof developer.prototype   // "undefifined"
```

- - -
# Prototype

## Some prototype gotchas

### Replacing prototype object

The prototype chain is live but what happened when you completely replace the prototype object?

```js
function Dog(){this.tail = true;}
var benji = new Dog();
var rusty = new Dog();

Dog.prototype.say = function() { return 'Woof!'; }

benji.say();   // "Woof!"
rusty.say();   // "Woof!"

benji.constructor;   // Dog()
rusty.constructor;   // Dog()
```

- - -
# Prototype

## Some prototype gotchas

### Replacing prototype object

> #### Note
> constructor of the prototype of a function is automatically set to the constructor function itself, rather than `Object()`


```js 
benji.constructor.prototype.constructor // Dog()
```

- - -
# Prototype

## Some prototype gotchas

### Replacing prototype object

Let's completely overwrite the prototype object with a brand new object

``js
Dog.prototype = { paws: 4, hair: true };
```

Old objects do not get access to the new prototype's properties:  
they still keep the secret link pointing to the old prototype object.

```js
typeof benji.paws   // "undefifined"
benji.say()   // "Woof!"
```

- - -
# Prototype

## Some prototype gotchas

### Replacing prototype object

Any new objects created from now on will use the updated prototype.

```js
var lucy = new Dog();
lucy.say()   // TypeError: lucy.say is not a function
lucy.paws    // 4

lucy.constructor    // Object()
benji.constructor   // Dog()

typeof lucy.constructor.prototype.paws    // "undefifined"
typeof benji.constructor.prototype.paws   // "number"
```

- - -
# Prototype

## Some prototype gotchas

### Replacing prototype object

To fix the unexpected behavior, you have to reset the constructor property when overwrite the prototype.

```js
Dog.prototype = {paws: 4, hair: true};
Dog.prototype.constructor = Dog;
```

> #### Best practice
> When you overwrite the prototype, reset the constructor property.
