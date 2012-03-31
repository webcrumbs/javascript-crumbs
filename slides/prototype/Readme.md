# Prototype

- - -
## Function's `prototype` property

- - -
# Prototype

## Function's `prototype` property


Every function has a property called `prototype`

`prototype` is an object shared by every object instantiated by the function

`protottype` is initially an empty object

```js
function foo(a, b) { return a * b; }
typeof foo.prototype // "object"
```

# Prototype

## Function's `prototype` property

### Augmenting `prototype`

`prototype` object can be augmented with properties and methods  

```js
function Circle (r) {
  this.r = r;
}
```

```js
Circle.prototype.name = 'circle';
Circle.prototype.getArea = function () {
  return Math.PI * this.r * this.r;
};
```

- - -
# Prototype

## Function's `prototype` property

### 

Methods and properties added to the `prototype` of the function `f`  
are available to every object created by function `f`  

```js
var c = new Circle(4);
c.r;          //4
c.name;       // "circle"
c.getArea();  //50.26548245743669
```

```js
var d = new Circle(2);
d.r;          //2
d.name;       //"circle"
d.getArea();  //12.566370614359172
```

- - -
# Prototype

## Function's `prototype` property

### The prototype is "live"  

Objects are passed by reference:  
the prototype is not copied with every new object instance  

```js
Circle.prototype.getCircumference = function () {
  return 2 * Math.PI * this.r;
};
```

```js
var d = new Circle(5);

c.getCircumference(); //25.132741228718345
d.getCircumference(); //31.41592653589793
```

- - -
## The prototype chain

- - -
# Prototype

## The prototype chain

### Accessing a property of an object

When you access a property `p` of an object `o` JavaScript:

1. looks for `p` in the properties of `o`
2. if it finds `p`, returns its value
3. else it looks in the prototype of `o`
4. if it finds `p`, it returns its value
5. else it look in the prototype of the prototype of `o`
6. ...

- - -
# Prototype

## The prototype chain

### Accessing a property of an object

```js
c.r; //4 - found in the properties of c
c.name; //"circle" - found in the prototype of c
```

- - -
# Prototype

## The prototype chain

### Understanding the chain

Every object `o` has a `constructor` property:  
the function which creates the object `o`

Every function `f` has a `prototype` property:  
the object shared by instances created by the function `f`

A constructor is a function, so it has a `prototype`  
A prototype is an object so it has a `constructor`

- - -
# Prototype

## The prototype chain

### Understanding the chain
  
```js
c = new Circle(4);
```

```js
typeof c; //"object"
c.constructor; //function Circle(r) {...}
c.constructor === Circle; //true
```

```js
typeof c.constructor; //"function"
c.constructor.ptototype; //"object"
```

- - -
# Prototype

## The prototype chain

### Understanding the chain

The built-in `Object` object is the highest-level parent,  
the end of the so called **prototype chain**.  

```js
c.toString();  // "[object Object]"
```

`c` doesn't have an own `toString()` method  
`c.prototype` doesn't have an own `toString()` method  
`Object.prototype` has it!

- - -
# Prototype

## The prototype chain

### Overwriting prototype's property with own property

The own property takes precedence over the prototype's.

```js
function Circle (r) {
  this.r = r;
  this.color = 'red';
}

Circle.prototype.color = 'green';
```

```js
var c = new Circle(5);

c.color; // "red"
```

```js
delete c.color;
c.color; // "green"
```

```js
c.color = 'blue';
c.color; // "blue"
```

- - -
## Useful methods

- - -
# Prototype

## Useful methods

### `hasOwnProperty(prop)`

A `for-in` loop iterates over all properties including those of the prototype.

```js
function Circle (r) {
  this.r = r;
}

Circle.prototype.color = 'green';
```

```js
var c = new Circle(3);

for (var p in c) {
  console.log(p);
}

//r
//color
```

- - -
# Prototype

## Useful methods

### `hasOwnProperty(prop)`

Use `hasOwnProperty()` to test if a property belongs to an object.

```js
var c = new Circle(3);

for (var p in c) {
  if (c.hasOwnProperty(p)) {
    console.log(p);
  }
}

//r
```

- - -
# Prototype

## Useful methods

### `isPrototypeOf(obj)`
 
This method tells whether that specific object is used as a prototype of another object.

```js
function Circle (r) {
  this.r = r;
}

Circle.prototype.color = 'green';
```

```js
var c = new Circle(4);
Circle.prototype.isPrototypeOf(c); //true
Object.prototype.isPrototypeOf(c); //true
Array.prototype.isPrototypeOf(c);  //false
```

- - -
## Some prototype gotchas

- - -
# Prototype

## Some prototype gotchas

### `prototype.constructor` is not reliable

It could be simply overwritten  
JavaScript access object's prototype through a secret link  
Some engines expose this link as a `__proto__` properties  

> #### Forbidden!
>
> Even when exposed never use secret `__proto__` property.  
> It's no standard: think it's there only for learning purpose.

- - -
# Prototype

## Some prototype gotchas

### `prototype.constructor` is not reliable

```js
function Circle (r) {
  this.r = r;
}

Circle.prototype.color = 'green';
```

```js
var c = new Circle(4);

c.constructor = 'junk'

typeof c.constructor.prototype // "undefined"
// a string object hasn't a prototype property

c.color; //"green"
// JavaScript uses immutable __proto__ secret link
```

- - -
# Prototype

## Some prototype gotchas

### `prototype.constructor` is not reliable

`__proto__` and `prototype` refer to the same object but:

* `__proto__` is a property of the instances
* `prototype` is a property of the constructor functions

```js
typeof c.__proto__   // "object"
typeof c.prototype   // "undefifined"
```
