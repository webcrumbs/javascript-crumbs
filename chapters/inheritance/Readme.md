# Inheritance

# Prototype chaining example
Prototype chaining is the default way to implement inheritance.

> ### Example
>
>```js
>function Shape(){
>  this.name = 'shape';
>  this.toString = function() { return this.name; };
>}
>
>function TwoDShape(){
>  this.name = '2D shape';
>}
>
>function Triangle(side, height) {
>  this.name = 'Triangle';
>  this.side = side;
>  this.height = height;
>    this.getArea = function() { return this.side * this.height / 2; };
>}
>```
>
> here is the inheritance magic code:
>
>```js
>TwoDShape.prototype = new Shape();
>TwoDShape.prototype.constructor = TwoDShape;
>
>Triangle.prototype = new TwoDShape();
>Triangle.prototype.constructor = Triangle;
>
>var tri = new Triangle(5, 10);
>tri.getArea(); // 25
>```


Instead of augmenting the object in the `prototype` property of `TwoDShape` with individual properties,  
completely overwrite it with another object, created by invoking the `Shape()` constructor with `new`.  

The same for `Triangle`: its prototype is replaced with an object created by `new TwoDShape()`.  

The important thing to note is that JavaScript works with objects, not classes.  

An **instance** is created using the `new Shape()` constructor and after that its properties can be inherited;  

After inheriting, whatever modification to `Shape()` function, will have no effect on `TwoDShape`.
This is because inheritance works on one instance: the instance to inherit from.  

Although the `tri` object doesn't have its own `toString()` method, it inherited one and can call it.  

> #### Example
>
>```js
>tri.toString()   // "Triangle"
>```
>
> #### Note 
> the inherited method `toString()` binds the `this` object to `tri`.  

Here is what the JavaScript engine does when you call `my.toString()`:

1. it loops through all of the properties of `tri` and doesn't find a method called `toString()`;
2. it looks at the object that `my.__proto__` points to; this object is the instance `new TwoDShape()` created during the inheritance process.
3. now the JavaScript engine loops through the instance of `TwoDShape` and doesn't find a `toString()` method. It then checks the `__proto__` of that object. This time `__proto__` points to the instance created by `new Shape()`;
4. the instance of `new Shape()` is examined and `toString()` is finally found;
5. this method is invoked in the context of `tri`, meaning that `this` points to `tri`.

> #### Note
>
>```js
>tri.constructor; // Triangle(side, height)
>```
>
>```js
>tri instanceof Shape     // true
>tri instanceof TwoDShape // true
>tri instanceof Triangle  // true
>tri instanceof Array     // false
>```
>
>```js
>Shape.prototype.isPrototypeOf(tri)     // true
>TwoDShape.prototype.isPrototypeOf(tri) // true
>Triangle.prototype.isPrototypeOf(tri)  // true
>String.prototype.isPrototypeOf(tri)    // false
>```

Of course, it's possible to create objects using the other two constructors.

> #### Example
>
>```js
>var td = new TwoDShape();
>td.constructor; // TwoDShape()
>td.toString()
>var s = new Shape();
>s.constructor; // Shape()
>```

## Moving shared properties to the prototype
When creating objects using a constructor function, own properties are added using `this`.  
This could be inefficient in cases where properties don't change across instances.  

```js
function Shape() {
  this.name = 'shape';
}
```

In the example above, every time new object is created using `new Shape()`, a new `name` property will be created and stored somewhere in memory.  
The other option is to have the `name` property added to the prototype and shared among all the instances:

```js
function Shape() {}
Shape.prototype.name = 'shape';
```

In this way every time an object is created using `new Shape()`, this object will not have its own property `name`, but will use the one added to the prototype.  
This is more efficient, but you should only use it for properties that don't change from one instance to another  
Methods are ideal for this type of sharing.  

Let's improve on the example above by adding all methods and suitable properties to the prototype.  
In the case of `Shape()` and `TwoDShape()` everything is meant to be shared.  

```js
function Shape() {}

// augment prototype
Shape.prototype.name = 'shape';
Shape.prototype.toString = function() { return this.name; };
```

```js
function TwoDShape() {}

// take care of inheritance first before augmenting the prototype,
// otherwise anything you add to TwoDShape.prototype will be wiped out when you inherit.
TwoDShape.prototype = new Shape();
TwoDShape.prototype.constructor = TwoDShape;

// augment prototype
TwoDShape.prototype.name = '2D shape';
```


The Triangle constructor is a little different, because every object it creates is a new triangle, which may have different dimensions.  
So it's good to keep `side` and `height` as its own properties and share the rest.  
The method `getArea()`, for example, is the same regardless of the actual dimensions of each triangle.

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

var tri = new Triangle(5, 10);
tri.getArea();  // 25
tri.toString(); // "Triangle"

tri.hasOwnProperty('side'); // true
tri.hasOwnProperty('name'); // false

TwoDShape.prototype.isPrototypeOf(tri); // true
tri instanceof Shape // true
```

## Inheriting the prototype only

> ### Tip
> for reasons of efficiency, it's good to add the reusable properties and methods to the prototype.

If previous tip is received, then it's probably a good idea to inherit only the prototype, because all the reusable code is there.  
This means that inheriting the object contained in `Shape.prototype` is better than inheriting the object created with `new Shape()`.  

To gain a little more efficiency:  
not creating a new object for the sake of inheritance alone, 
not having less lookups during runtime when it comes to searching for `toString()` for example.

```js
function Shape() {}

// augment prototype
Shape.prototype.name = 'shape';
Shape.prototype.toString = function() {return this.name;};


function TwoDShape() {}

// take care of inheritance
TwoDShape.prototype = Shape.prototype;
TwoDShape.prototype.constructor = TwoDShape;

// augment prototype
TwoDShape.prototype.name = '2D shape';


function Triangle(side, height) {
  this.side = side;
  this.height = height;
}

// take care of inheritance
Triangle.prototype = TwoDShape.prototype;
Triangle.prototype.constructor = Triangle;

// augment prototype
Triangle.prototype.name = 'Triangle';
Triangle.prototype.getArea = function() { return this.side * this.height / 2; }


var tri = new Triangle(5, 10);
tri.getArea();  // 25
tri.toString(); // "Triangle"
```

So the lookup is only a two-step process as opposed to four (in the previous example) or three (in the first example).  

Simply copying the prototype is more efficient but it has a side effect:  
because all of the children and parents point to the same object, when a child modifies the prototype, the parents get the changes, and so do the siblings.

```js
Triangle.prototype.name = 'Triangle'; //it effectively changes Shape.prototype.name

var s = new Shape();
s.name // "Triangle"
```

## A temporary constructor `new F()`
A solution to the problem outlined above, is to use an intermediary to break the chain.  
The intermediary is in the form of a temporary constructor function.  
Creating an empty function `F()` and setting its prototype to the prototype of the parent constructor, allows to call `new F()` and create objects that have no properties of their own, but inherit everything from the parent's prototype.  

```js
function Shape() {}

// augment prototype
Shape.prototype.name = 'shape';
Shape.prototype.toString = function() {return this.name;};


function TwoDShape() {}

// take care of inheritance
var F = function(){};
F.prototype = Shape.prototype;
TwoDShape.prototype = new F();
TwoDShape.prototype.constructor = TwoDShape;

// augment prototype
TwoDShape.prototype.name = '2D shape';


function Triangle(side, height) {
  this.side = side;
  this.height = height;
}

// take care of inheritance
var F = function(){};
F.prototype = TwoDShape.prototype;


Triangle.prototype = new F();
Triangle.prototype.constructor = Triangle;

// augment prototype
Triangle.prototype.name = 'Triangle';
Triangle.prototype.getArea = function() { return this.side * this.height / 2; };

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

At the same time, this approach supports the idea that:

* only properties and methods added to the prototype should be inherited, and
* own properties should not be inherited.

The rationale behind this is are that own properties are likely to be too specific to be reusable.

## Isolating the inheritance part into a function
Let's move the code that takes care of all of the inheritance details into a reusable `inherits()` function:

```js
function inherits(Child, Parent) {
  var F = function() {};
  F.prototype = Parent.prototype;
  Child.prototype = new F();
  Child.prototype.constructor = Child;
}
```

Using this function (or your own custom version of it) will help you keep your code clean with regard to the repetitive inheritance-related tasks.  
This way you can inherit by simply using:

```js
inherits(Child, Parent);
```

So in our shapes examples, inheritance works as follow:

> #### Example
>
>```js
>function Shape() {}
>
>// augment prototype
>Shape.prototype.name = 'shape';
>Shape.prototype.toString = function() {return this.name;};
>
>
>function TwoDShape() {}
>
>// take care of inheritance
>inherits(TwoDShape, Shape);
>
>// augment prototype
>TwoDShape.prototype.name = '2D shape';
>
>
>function Triangle(side, height) {
>  this.side = side;
>  this.height = height;
>}
>
>// take care of inheritance
>inherits(Triangle, TwoDShape);
>
>// augment prototype
>Triangle.prototype.name = 'Triangle';
>Triangle.prototype.getArea = function() { return this.side * this.height / 2; };
>
>var my = new Triangle(5, 10);
>my.getArea();  // 25
>my.toString(); // "Triangle"
>```
