# Objects

An object is an unordered collection of properties, each of which has a name and a value.

```js
var hero = {
    breed: 'Turtle',
    occupation: 'Ninja'
};
```

`hero` is the name of the variable that contains the object.  
`{` and `}` are used to define an object.  
Object's elements (called properties) are separated with commas.  
The key/value pairs are divided by colons, as `key: value`.  
The keys (names of the properties) can optionally be placed in quotation marks.  

```js
/* Following definitions are all the same */
var o = {prop: 1};
var o = {"prop": 1};
var o = {'prop': 1};
```

You have to quote key names when the property name:  

* is one of the reserved words in JavaScript
* contains spaces or special characters (anything other than letters, numbers, and the underscore character)
* starts with a number

```js
var o = {
    something: 1,
    'yes or no': 'yes',
    '!@#$%^&*': true
};
```

## Elements, Properties, Methods
An object contains **properties**.  
A property of an object can contain a function, because functions are just data.  
In this case, you say that this property is a **method**.  

```js
var dog = {
    name: 'Benji',
    talk: function(){
        alert('Woof, woof!');
    }
};
```

## Accessing Object's properties
There are two ways to access a property of an object:

* Using square bracket notation, for example `hero['occupation']`
* Using the dot notation, for example `hero.occupation`

In some cases you have no choise: you cannot use the dot notation.

```js
var hero = {
    breed: 'Turtle',
    occupation: 'Ninja'
};

/* Accessing a property with the dot notation */
hero.breed;   // "Turtle"

/* Accessing a property with the bracket notation */
hero['occupation'];   // "Ninja"

/* Accessing a non-existing property returns undefined */
hero.hair_color;   // "undefined"
```

Objects can contain any data, including other objects.

```js
var book = {
    name: 'Catch-22',
    published: 1961,
    author: {
        firstname: 'Joseph',
        lastname: 'Heller'
    }
};

book.author.firstname        // "Joseph"
book['author']['lastname']   // "Heller"
book.author['lastname']      // "Heller"
book['author'].lastname      // "Heller"

var key = 'firstname';
book.author[key];            // "Joseph"
```

## Calling an Object's methods
Calling (invoking) a method is the same as calling any other function: just add parentheses after the method name, which effectively say "Execute!".

```js
var hero = {
    breed: 'Turtle',
    occupation: 'Ninja',
    say: function() {
        return 'I am ' + hero.occupation;
    }
}

hero.say();     // "I am Ninja"
hero['say']();  // "I am Ninja"

/* If say method had parameters... */
hero.say('a', 'b', 'c');
```

## Altering properties/methods
JavaScript is a dynamic language; it allows you to alter properties and methods of existing objects at any time.  
This includes adding new properties or deleting them.  
You can start with a blank object and add properties later.  

```js
/* An empty object */
var hero = {};

/* Accessing a non-existing property */
typeof hero.breed   // "undefifined"

/* Adding some properties and a method */
hero.breed = 'turtle';
hero.name = 'Leonardo';
hero.sayName = function() { return hero.name; };

/* Calling the method */
hero.sayName();   // "Leonardo"

/* Deleting a property */
delete hero.name;   // true

/* Calling the method again will no longer work */
hero.sayName();   // TypeError: Object #<Object> has no method 'sayName'
```

## Using this Value
In the previous example, the method `sayName()` used `hero.name` to access the name property of the hero object.  
When you're inside a method, there is another way to access the object this method belongs to: by using the special value `this`.  

```js
var hero = {
    name: 'Rafaelo',
    sayName: function() {
        return this.name;
    }
}

hero.sayName();   // "Rafaelo"
```

So when you say `this`, you are actually saying "this object" or "the current object".

## Constructor Functions
There is another way to create objects: by using constructor functions.

```js 
function Hero() {
    this.occupation = 'Ninja';
}
```

In order to create an object using this function, you use the `new` operator.

```js
var hero = new Hero();
hero.occupation;   // "Ninja"
```

The benefit of using constructor functions is that they accept parameters, which can be used when creating new objects.

```js
function Hero(name) {
    this.name = name;
    this.occupation = 'Ninja';
    this.whoAreYou = function() {
        return "I'm " + this.name + " and I'm a " + this.occupation;
    }
}

var h1 = new Hero('Michelangelo');
var h2 = new Hero('Donatello');
h1.whoAreYou();   // "I'm Michelangelo and I'm a Ninja"
h2.whoAreYou();   // "I'm Donatello and I'm a Ninja"
```

By convention, you should capitalize the first letter of your constructor functions.  

If you call a function that is designed to be a constructor, but you omit the `new` operator, this is not an error, but it may not behave as you could expect.

```js
var h = Hero('Leonardo');
typeof h   // "undefifined"
```

As there was no `new` operator, we didn't create a new object.  
The function was called like any other function, so `h` contains the value that the function returns.  
The function does not return anything (there's no return), so it actually returns `undefined`, which gets assigned to `h`.  
In this case, `this` refer to global object.

## The Global Object
The host environment provides a global object and all global variables are actually properties of the global object.  
If your host environment is the web browser, the global object is called `window`.  

```js
var a = 1;

a;   // 1

/* a is global i.e. belongs to the global object */
window['a']   // 1
```

Declaring a constructor function and calling it without new, returns `"undefined"`, and `this` result binded to global object.

```js
function Hero(name) { this.name = name; }

var h = Hero('Leonardo');
typeof h   // "undefined"
typeof h.name   // TypeError: Cannot read property 'name' of undefined

/* this is binded to global object */
name   // "Leonardo"
window.name   // "Leonardo"

/* using new operator insead */
var h2 = new Hero('Michelangelo');
typeof h2   // "object"
h2.name   // "Michelangelo"
```

## constructor property
When an object is created, a special property is assigned to it behind the scenes—the constructor property.  
It contains a reference to the constructor function used to create this object.  

```js
h2.constructor   // Hero(name)

/* Following code means:
 * "I don't care how object h2 was created,
 * but I want another one just like it" */
var h3 = new h2.constructor('Rafaello');
h3.name;   // "Rafaello"
```

If an object was created using the object literal notation, its constructor is the built-in `Object()` constructor function.

```js
var o = {};
o.constructor;   // Object();
typeof o.constructor;   // "function"
```

## instanceof operator
Using the instanceof operator, you can test if an object was created with a specific constructor function.
￼￼
```js￼
function Hero() {}
var h = new Hero();
var o = {};
h instanceof Hero;   // true
h instanceof Object;   // false
o instanceof Object;   // true
```

<!-- io questa non la metteri... mi sembra confonda invece di chiarire -->
<!-- 
## Functions that return objects
You can have a function that does some preparatory work and has an object as a return value.
This is a different way to create objects.

    function factory(name) {
        return { name: name };
    }

    var o = factory('one');
    o.name   // "one"
    o.constructor   // Object()

You can also use constructor functions and return objects, different from `this`.
This means you can modify the default behavior of the constructor function.

    /* Here's the normal constructor scenario */
    function C() { this.a = 1; }

    var c = new C();
    c.a   // 1


    /* Different scenario */
    function C2() {
        this.a = 1;
        return {b: 2};
    }

    var c2 = new C2();
    typeof c2.a   // "undefined"
    c2.b   // 2


Instead of returning the object `this`, which contains the property `a`, the constructor returned another object that contains the property `b`.
This is possible only if the return value is an object.
Otherwise, if you try to return anything that is not an object, the constructor will proceed with its usual behavior and return `this`.
-->
<!-- eliminerei la sezione precedente -->

## Passing Objects
When you copy an object or pass it to a function, you only pass a reference to that object.  
Consequently, if you make a change to the reference, you are actually modifying the original object.

```js
var original = { howmany: 1 };
var copy = original;
copy.howmany   //￼1
copy.howmany = 100;
original.howmany   // 100
```

The same thing applies when passing objects to functions:

```js
var original = { howmany: 100 };
var nullify = function(o) { o.howmany = 0; }
nullify(original);
original.howmany   // 0
```

## Comparing Objects
When you compare objects, you'll get `true` only if you compare two references to the same object.  
Comparing two distinct objects that happen to have the exact same methods and properties will return `false`.

```js
var fido  = {breed: 'dog'};
var benji = {breed: 'dog'};

/* Comparing them will return false */
benji === fido   // false
benji == fido   // false

var mydog = benji;
mydog === benji   // true
mydog === fido    // false
```
