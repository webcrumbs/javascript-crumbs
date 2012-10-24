# Inheritance

- - -

# Inheritance

## Inheritance through prototype chain

### A first geometric example

```js
function Shape(){
  this.name = 'shape';
  this.toString = function() { return this.name; };
}

function TwoDShape(){
  this.name = '2D shape';
}
```

- - -
# Inheritance

## Inheritance through prototype chain

### A first geometric example

Here is the inheritance magic code:

```js
TwoDShape.prototype = new Shape();
TwoDShape.prototype.constructor = TwoDShape;
```

- - -
# Inheritance

## Inheritance through prototype chain

### A first geometric example: explanation

We completely overwrote the object in the `prototype` property of `TwoDShape` with another object, created by invoking the `Shape()` constructor with `new`.  

The important thing to note is that JavaScript works with objects, not classes.  

An **instance** is created using the `new Shape()` constructor and after that its properties can be inherited;  

After inheriting, whatever modification to `Shape()` function, will have no effect on `TwoDShape`.
This is because inheritance works on one instance: the instance to inherit from.  

- - -
# Inheritance

## Inheritance through prototype chain

### A first geometric example

Now test it:

```js
var tds = new TwoDShape();
tds.toString(); // "2D shape"
```

> #### Note 
> the inherited method `toString()` binds the `this` object to `tri`.  

- - -
# Inheritance

## Inheritance through prototype chain

### A second geometric example

```js
function Triangle(side, height) {
  this.name = 'Triangle';
  this.side = side;
  this.height = height;
    this.getArea = function() { return this.side * this.height / 2; };
}
```

- - -
# Inheritance

## Inheritance through prototype chain

### A second geometric example

Here is the inheritance magic code:

```js
Triangle.prototype = new TwoDShape();
Triangle.prototype.constructor = Triangle;
```

- - -
# Inheritance

## Inheritance through prototype chain

### A second geometric example

Now test it

```js
var tri = new Triangle(5, 10);
tri.getArea(); //25
```

```js
tri.toString() //"Triangle"
```

> #### Note 
> the inherited method `toString()` binds the `this` object to `tri`.  

- - -
# Inheritance

## Inheritance through prototype chain

### What exactly happen

Here is what the JavaScript engine does when you call `my.toString()`:

1. it loops through all of the properties of `tri` and doesn't find a method called `toString()`;
2. it looks at the object that `my.__proto__` points to; this object is the instance `new TwoDShape()` created during the inheritance process.
3. now the JavaScript engine loops through the instance of `TwoDShape` and doesn't find a `toString()` method. It then checks the `__proto__` of that object. This time `__proto__` points to the instance created by `new Shape()`;
4. the instance of `new Shape()` is examined and `toString()` is finally found;
5. this method is invoked in the context of `tri`, meaning that `this` points to `tri`.

- - -
# Inheritance

## Inheritance through prototype chain

### Some tests

```js
tri.constructor; // Triangle(side, height)
```

```js
tri instanceof Shape     // true
tri instanceof TwoDShape // true
tri instanceof Triangle  // true
tri instanceof Array     // false
```

```js
Shape.prototype.isPrototypeOf(tri)     // true
TwoDShape.prototype.isPrototypeOf(tri) // true
Triangle.prototype.isPrototypeOf(tri)  // true
String.prototype.isPrototypeOf(tri)    // false
```

- - -
# Inheritance

## Inheritance through prototype chain

### A second geometric example - the end

Of course, it's possible to create objects using the other two constructors.

```js
var td = new TwoDShape();
td.constructor; // TwoDShape()
td.toString()
var s = new Shape();
s.constructor; // Shape()
```

- - -
## Moving shared properties to the prototype

- - -
# Inheritance

## Moving shared properties to the prototype

### The wrog way

```js
function Shape() {
  this.name = 'shape';
}
```

In this way, every time new object is created using `new Shape()`,  
a new `name` property will be created and stored somewhere in memory. 

- - -
# Inheritance

## Moving shared properties to the prototype

### The right way

```js
function Shape() {}
Shape.prototype.name = 'shape';
```

In this way every time an object is created using `new Shape()`,  
this object will not have its own property `name`,  
but will use the one added to the prototype.  

This is more efficient, but you should only use it for properties  
that don't change from one instance to another  

Methods are ideal for this type of sharing.  

- - -
# Inheritance

## Moving shared properties to the prototype

### The right way

> ### Tip
> for reasons of efficiency, it's good to add the reusable properties and methods to the prototype.

- - -
# Inheritance

## Moving shared properties to the prototype

### Improving the geometric example

```js
function Shape() {}

// augment prototype
Shape.prototype.name = 'shape';
Shape.prototype.toString = function() { 
    return this.name; 
};
```

- - -
# Inheritance

## Moving shared properties to the prototype

### Improoving the geometric example

```js
function TwoDShape() {}

// take care of inheritance first before augmenting the prototype,
// otherwise anything you add to TwoDShape.prototype will be wiped out when you inherit.
TwoDShape.prototype = new Shape();
TwoDShape.prototype.constructor = TwoDShape;

// augment prototype
TwoDShape.prototype.name = '2D shape';
```

- - -
# Inheritance

## Moving shared properties to the prototype

### Improving the geometric example

```js
function Triangle(side, height) {
  this.side = side;
  this.height = height;
}

// take care of inheritance first before augmenting the prototype,
Triangle.prototype = new TwoDShape();
Triangle.prototype.constructor = Triangle;

// augment prototype
Triangle.prototype.name = 'Triangle';
Triangle.prototype.getArea = function() { return this.side * this.height / 2; };
```

- - -
# Inheritance

## Moving shared properties to the prototype

### Testing the improved geometric example

```js
var tri = new Triangle(5, 10);
tri.getArea();  // 25
tri.toString(); // "Triangle"

tri.hasOwnProperty('side'); // true
tri.hasOwnProperty('name'); // false

TwoDShape.prototype.isPrototypeOf(tri); // true
tri instanceof Shape // true
```

- - -
## Inheriting the prototype only

- - -
# Inheritance

## Inheriting the prototype only

### How to do it

Inheriting the object contained in `Shape.prototype` could be better than inheriting the object created with `new Shape()`.  

```js
function Shape() {}

// augment prototype
Shape.prototype.name = 'shape';
Shape.prototype.toString = function() {return this.name;};


function Triangle(side, height) {
  this.side = side;
  this.height = height;
}

// take care of inheritance
Triangle.prototype = Shape.prototype;
Triangle.prototype.constructor = Triangle;

// augment prototype
Triangle.prototype.name = 'Triangle';
Triangle.prototype.getArea = function() { return this.side * this.height / 2; }
```

- - -
# Inheritance

## Inheriting the prototype only

### Testing this approach

```js
var tri = new Triangle(5, 10);
tri.getArea();  // 25
tri.toString(); // "Triangle"
```

So the lookup is only a two-step process as opposed to four.  

Simply copying the prototype is more efficient but it has a side effect:

```js
var s = new Shape();
s.name // "Triangle"
```

- - -
## A temporary constructor `new F()`

- - -
# Inheritance

## A temporary constructor `new F()`

### Explanation

A solution to the problem outlined above, is to use an intermediary to break the chain.  
The intermediary is in the form of a temporary constructor function.  

Creating an empty function `F()` and setting its prototype to the prototype of the parent constructor, allows to call `new F()` and create objects that have no properties of their own, but inherit everything from the parent's prototype.  

- - -
# Inheritance

## A temporary constructor `new F()`

### How to do it

```js
function Shape() {}

// augment prototype
Shape.prototype.name = 'shape';
Shape.prototype.toString = function() {
    return this.name;
};
```

- - -
# Inheritance

## A temporary constructor `new F()`

### How to do it

```js
function Triangle(side, height) {
  this.side = side;
  this.height = height;
}

// take care of inheritance
var F = function() {};
F.prototype = Shape.prototype;


Triangle.prototype = new F();
Triangle.prototype.constructor = Triangle;

// augment prototype
Triangle.prototype.name = 'Triangle';
Triangle.prototype.getArea = function() { return this.side * this.height / 2; };
```

- - -
# Inheritance

## A temporary constructor `new F()`

### Testing this approach

```js
var my = new Triangle(5, 10);
my.getArea();  // 25
my.toString(); // "Triangle"
```

Using this approach, we keep the prototype chain in place  
and the parents' properties are not overwritten by the children.  
In fact:

```js
var s = new Shape();
s.name; // "shape"
```

- - -
# Inheritance

## A temporary constructor `new F()`

### The idea behind

This approach supports the idea that:

* only properties and methods added to the prototype should be inherited, and
* own properties should not be inherited.

- - -
## Isolating the inheritance part into a function

- - -
# Inheritance

## Isolating the inheritance part into a function

### `inherits(Child, Parent)`

Let's move the code that takes care of all of the inheritance details into a reusable `inherits()` function:

```js
function inherits(Child, Parent) {
  var F = function() {};
  F.prototype = Parent.prototype;
  Child.prototype = new F();
  Child.prototype.constructor = Child;
}
```

- - -
# Inheritance

## Isolating the inheritance part into a function

### `inherits(Child, Parent)`

Using this function (or your own custom version of it) will help you keep your code clean with regard to the repetitive inheritance-related tasks.  
This way you can inherit by simply using:

```js
inherits(Child, Parent);
```

- - -
# Inheritance

## Isolating the inheritance part into a function

### Applying `inherits(Child, Parent)` function

```js
function Shape() {}

// augment prototype
Shape.prototype.name = 'shape';
Shape.prototype.toString = function() {
    return this.name;
};
```

- - -
# Inheritance

## Isolating the inheritance part into a function

### Applying `inherits(Child, Parent)` function

```js
function Triangle(side, height) {
    this.side = side;
    this.height = height;
}

// take care of inheritance
inherits(Triangle, TwoDShape);

// augment prototype
Triangle.prototype.name = 'Triangle';
Triangle.prototype.getArea = function() { return this.side * this.height / 2; };
```

- - -
# Inheritance

## Isolating the inheritance part into a function

### Testing `inherits(Child, Parent)` function

```js
var my = new Triangle(5, 10);
my.getArea();  // 25
my.toString(); // "Triangle"

var shape = Shape();
shape.name; //"Shape"
```