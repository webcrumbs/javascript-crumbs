# Prototype

## Function's prototype property
`prototype` is a property of every `Function` object.  
It gets created as soon as you define the function.  
Its initial value is an empty object.  

```js
function foo(a, b) { return a * b; }
typeof foo.prototype // "object"
```

this empty object can be augmented with properties and methods.  
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

Adding methods and properties to the `prototype` property of the constructor function is another way to add functionality to the objects this constructor produces.

```js
Gadget.prototype.price = 100;
Gadget.prototype.rating = 3;
Gadget.prototype.getInfo = function() {
    return 'Rating: ' + this.rating + ', price: ' + this.price;
};
```

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

### The prototype is "live".  
Objects are passed by reference in JavaScript, and therefore the prototype is not copied with every new object instance.  
Modifying of the prototype at any time implies that all objects (even those created before the modification) will inherit the changes.  

```js
Gadget.prototype.get = function(what) {
     return this[what];
};
newtoy.get('price');   // 100
newtoy.get('color');   // "black"
```

### What's mine is mine, what's my prototype's is mine

When trying to access a property of `newtoy`, say `newtoy.name` the JavaScript engine:
1. will look through all of the properties of the object searching for one called name
2. if it finds it, will return its value

```js
newtoy.name  // "webcam"
```

When trying to access a property belonging to `newtoy` constructor's prototype (i.e. the prototype of the `Gadget` function), `rating` for example, the JavaScript engine:

1. will examine all of the properties of newtoy and will not find the one called `rating`
2. then will identify the prototype of the constructor function used to create this object
3. if the property is found in the prototype, this property is used

```js
newtoy.rating  // 3
```

Every object, in fact, has a `constructor` property, which is a reference to the function that created the object.

```js
newtoy.constructor                  // Gadget(name, color)
newtoy.constructor.prototype.rating // 3
```

Every object has a `constructor`.  
The prototype of a constructor function is an object.  
So it must have a `constructor` too. Which in turn has a prototype.  
The built-in `Object` object is the highest-level parent, the and of the so called the **prototype chain**.  

`newtoy.toString()` and `newtoy` doesn't have an own `toString()` method and its prototype doesn't either.
In the end Object's `toString()` will use.

```js
newtoy.toString()  // "[object Object]"
```

### Overwriting prototype's property with own property
What if the object does have its own property and the prototype also has one with the same name?  
The own property takes precedence over the prototype's.

```js
function Gadget(name) {
     this.name = name;
}

Gadget.prototype.name = 'foo';   // "foo"
var toy = new Gadget('camera');

toy.name;                        // "camera"

delete toy.name;
toy.name;                        // "foo"

toy.name = 'camera';
toy.name;                        // "camera"
```

## Enumerating properties
To list all properties of an object use a `for-in` loop.

```js
var o = {p1: 1, p2: 2};
for (var i in o) {
    console.log(i + '=' + o[i]);
}

// p1=1
// p2=2
```

There are some details to be aware of:

* Not all properties show up in a `for-in` loop. For example, the length (for arrays) and constructor properties will not show up. The properties that do show up are called _enumerable_. You can check which ones are enumerable with the help of the `propertyIsEnumerable()` method that every object provides.
* Prototypes that come through the prototype chain will also show up, if properties provided are enumerable. You can check if a property is an own property versus prototype's using the `hasOwnProperty()` method.
* `propertyIsEnumerable()` will return false for all of the prototype's properties, even those that are enumerable and will show up in the for-in loop.

```js
function Gadget(name, color) {
    this.name = name;
    this.color = color;
    this.someMethod = function() { return 1; }
}

Gadget.prototype.price = 100;
Gadget.prototype.rating = 3;

var newtoy = new Gadget('webcam', 'black');

for (var prop in newtoy) {
    console.log(prop + ' = ' + newtoy[prop]);
}

// name = webcam
// color = black
// someMethod = function () { return 1; } price = 100
// rating = 3
```

```js
newtoy.hasOwnProperty('name')    // true
newtoy.hasOwnProperty('price')   // false
```

```js
for (var prop in newtoy) {
    if (newtoy.hasOwnProperty(prop)) {
    console.log(prop + '=' + newtoy[prop]);
    }
}

// name=webcam
// color=black
// someMethod=function () { return 1; }
```

```js
newtoy.propertyIsEnumerable('name')          // true
newtoy.propertyIsEnumerable('constructor')   // false
newtoy.propertyIsEnumerable('price')         // false
newtoy.constructor.prototype.propertyIsEnumerable('price')   // true
```

## isPrototypeOf() method
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

## Some prototype gotchas

### prototype.constructor is not reliable
It could be simply overwritten.  
JavaScript engine access object's prototype through a secret link.  
Some engines expose this link as a `__proto__` properties.  

> #### Forbidden!
>
> Even when exposed never use secret `__proto__` property.
> It's no standard: think it's there only for learning purpose.

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
```

It is allowed to overwrite constructor property.

```js
developer.constructor = 'junk'
typeof developer.constructor.prototype // "undefifined", a string object haven't prototype property

developer.breathes  // "air", engine uses imutable __proto__ secret link
```

`__proto__` is not the same as `prototype`:

* `__proto__` is a property of the instances
* `prototype` is a property of the constructor functions.

```js
typeof developer.__proto__   // "object"
typeof developer.prototype   // "undefifined"
```

### Replacing prototype object
The prototype chain is live with the exception of when you completely replace the prototype object.

```js
function Dog(){this.tail = true;}
var benji = new Dog();
var rusty = new Dog();

Dog.prototype.say = function() { return 'Woof!'; }

benji.say();   // "Woof!"
rusty.say();   // "Woof!"

benji.constructor;   // Dog()
rusty.constructor;   // Dog()

> #### Note
> constructor of the prototype of a function is automatically set to the constructor function itself, rather than `Object()`
>
> ```js 
> benji.constructor.prototype.constructor // Dog()
>```

Let's completely overwrite the prototype object with a brand new object

```js
Dog.prototype = { paws: 4, hair: true };
```


Old objects do not get access to the new prototype's properties:  
they still keep the secret link pointing to the old prototype object.

```js
typeof benji.paws   // "undefifined"
benji.say()   // "Woof!"
```

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

To fix the unexpected behavior, you have to reset the constructor property when overwrite the prototype.

```js
Dog.prototype = {paws: 4, hair: true};
Dog.prototype.constructor = Dog;
```

> #### Best practice
> When you overwrite the prototype, it is a good idea to reset the constructor property.
