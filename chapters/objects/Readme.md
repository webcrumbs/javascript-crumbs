# Objects

An object is an unordered collection of properties, each of which has a name and a value.

```js
{
  prop1: 'string value',
  prop2: 123
}
```

`{` and `}` are used to define an object.  
Object's elements (called properties) are separated with commas.  
The key/value pairs are divided by colons, as `key: value`.  
The keys (names of the properties) can optionally be placed in quotation marks.  

> #### Example
>
>```js
>var hero = {
>  breed: 'Turtle',
>  occupation: 'Ninja'
>};
>```
>
>`hero` is the name of the variable that contains the object.


> #### Example 
>
>```js
>/* Following definitions are all the same */
>var o = {prop: 1};
>var o = {"prop": 1};
>var o = {'prop': 1};
>```

Property key name has to be quoted when:  

* is one of the reserved words in JavaScript
* contains spaces or special characters (anything other than letters, numbers, and the underscore character)
* starts with a number

> ### Example
> ```js
>var o = {
>  something: 1,
>  'yes or no': 'yes',
>  '!@#$%^&*': true
>};
>```

### Elements, properties, methods
An object contains **properties**.  
A property of an object can contain a function, because functions are just data.  
In this case, you say that this property is a **method**.  

> #### Example
>
>```js
>var dog = {
>  name: 'Benji',
>  talk: function(){
>    alert('Woof, woof!');
>  }
>};
>```

### Accessing object's properties
There are two ways to access a property of an object.

Using square bracket notation

```js
obj['property key name']
```

Or using the dot notation

```js
obj.property_key_name
```

> #### Example
>```js
>var hero = {
>  breed: 'Turtle',
>  occupation: 'Ninja',
>  'finger count':  3
>};
>```
>
> accessing a property with the dot notation
>
>```js
>hero.breed; // "Turtle"
>```
>
> accessing a property with the bracket notation
>
>```js
>hero['occupation']; // "Ninja"
>```
>
> accessing a non-existing property returns undefined
>
>```js
>hero.height; // "undefined"
>```

If property name needs quotation in definition, access needs square bracket notation.

> #### Example
> ```js
> hero['finger count']; // 3
>```

> ### Tip
>
> if property name is stored in a variable, use it with square bracket notation
>  
>```js
>var keyName = 'occupation';
>hero[keyName]; // "Ninja"
>```

Objects can contain any data, including other objects.

> ### Example
>```js
>var book = {
>  name: 'Catch-22',
>  published: 1961,
>  author: {
>    firstname: 'Joseph',
>    lastname: 'Heller'
>  }
>};
>
>book.author.firstname      // "Joseph"
>book['author']['lastname'] // "Heller"
>book.author['lastname']    // "Heller"
>book['author'].lastname    // "Heller"
>
>var key = 'firstname';
>book.author[key]; // "Joseph"
>```

### Calling an object's methods
Calling (invoking) a method is the same as calling any other function:   
just add parentheses after the method name, which effectively say "Execute!".

> #### Example
>
>```js
>var hero = {
>  breed: 'Turtle',
>  occupation: 'Ninja',
>  say: function() {
>    return 'I am ' + hero.occupation;
>  }
>}
>
>hero.say();    // "I am Ninja"
>hero['say'](); // "I am Ninja"
>```
>
> if say method had parameters...
>
>```js
>hero.say('a', 'b', 'c');
>```

### Altering properties/methods
JavaScript is a dynamic language.  
It means it's possible to alter properties and methods of existing objects at any time.  
This includes adding new properties or deleting them.  

> ### Exmaple
>
> define an empty object
>
>```js
>var hero = {};
>```
>
> access a non-existing property
>
>```js
>typeof hero.breed // "undefined"
>```
>
> add some properties and a method
>
>```js
>hero.breed = 'turtle';
>hero.name = 'Leonardo';
>hero.sayName = function() { return hero.name; };
>```
>
> call the method
>
>```js
>hero.sayName(); // "Leonardo"
>```
>
> delete a property
>
>```js
>delete hero.name; // true
>```
>
> calling the method again will no longer work
>
>```js
>hero.sayName(); // TypeError: Object #<Object> has no method 'sayName'
>```

## Using this value
Inside a method, there is a special way to access the object this method belongs to:  
by using the special value `this`.  

> #### Example
>```js
>var hero = {
>  name: 'Rafaelo',
>  sayName: function() {
>    return this.name;
>  }
>}
>
>hero.sayName();   // "Rafaelo"
>```
>

> #### Tip
> when you say `this`, you are actually saying "this object" or "the current object".

## Constructor functions
There is another way to create objects: by using **constructor functions***.  
In order to create an object using this kind of function, use the `new` operator.

> #### Exmaple
>```js 
>function Hero() {
>  this.occupation = 'Ninja';
>}
>```
>
>```js
>var hero = new Hero();
>hero.occupation; // "Ninja"
>```

The benefit of using constructor functions is that they accept parameters, which can be used when creating new objects.

> #### Example
>```js
>function Hero(name) {
>  this.name = name;
>  this.occupation = 'Ninja';
>  this.whoAreYou = function() {
>    return "I'm " + this.name + " and I'm a " + this.occupation;
>  }
>}
>
>var h1 = new Hero('Michelangelo');
>var h2 = new Hero('Donatello');
>h1.whoAreYou(); // "I'm Michelangelo and I'm a Ninja"
>h2.whoAreYou(); // "I'm Donatello and I'm a Ninja"
>```

> #### Convention
> capitalize the first letter of your constructor functions

> #### Warning 
> calling a function that is designed to be a constructor but
> omitting the `new` operator may result in a behaviour you could not expect.
>
> ```js
> var h = Hero('Leonardo');
> typeof h   // "undefifined"
> ```
>
> As there was no `new` operator, it didn't create a new object.  
> The function was called like any other function, so `h` contains the value that the function returns.  
> The function does not return anything (there's no `return`),  
> so it actually returns `undefined`, which gets assigned to `h`.  
> In this case, `this` refer to global object.

## The global object
The host environment provides a global object and all global variables are actually properties of the global object.  
If your host environment is the web browser, the global object is called `window`.  

> #### Exmaple
>```js
>var a = 1;
>a;   // 1
>```
>
> a is global i.e. belongs to the global object
>
>```js
>window['a']   // 1
>```

Declaring a constructor function and calling it without `new`, returns `"undefined"`, and `this` result binded to global object.

> #### Exmaple
>```js
>function Hero(name) { this.name = name; }
>
>var h = Hero('Leonardo');
>typeof h   // "undefined"
>typeof h.name   // TypeError: Cannot read property 'name' of undefined
>
> `this` is binded to global object
> 
>```js
>name   // "Leonardo"
>window.name   // "Leonardo"
>```
>
> using new operator instead
>
>```js
>var h2 = new Hero('Michelangelo');
>typeof h2   // "object"
>h2.name   // "Michelangelo"
>```

## constructor property
When an object is created, a special property is assigned to it behind the scenes—the constructor property.  
It contains a reference to the constructor function used to create this object.  

> #### Exmaple
>```js
>function Hero(name) { this.name = name; }
>var h = Hero('Leonardo');
>
>h2.constructor // Hero(name)
>```
>
> following code means:
> "I don't care how object h2 was created,
> but I want another one just like it"
>
> ```js
> var h2 = new h2.constructor('Rafaello');
> h3.name; // "Rafaello"
> ```

If an object was created using the object literal notation, its constructor is the built-in `Object()` constructor function.

> #### Example
>
>```js
>var o = {};
>o.constructor; // Object();
>typeof o.constructor; // "function"
>```

## instanceof operator
Using the instanceof operator, you can test if an object was created with a specific constructor function.

> #### Example￼
>```js￼
>function Hero() {}
>var h = new Hero();
>var o = {};
>h instanceof Hero;   // true
>h instanceof Object; // false
>o instanceof Object; // true
>```

## Passing objects
When you copy an object or pass it to a function, you only pass a reference to that object.  
Consequently, if you make a change to the reference, you are actually modifying the original object.

> #### Example
>```js
>var original = { howmany: 1 };
>var copy = original;
>copy.howmany; //￼1
>copy.howmany = 100;
>original.howmany; // 100
>```

The same thing applies when passing objects to functions:

> #### Example
> ```js
> var original = { howmany: 100 };
> var nullify = function(o) { o.howmany = 0; }
> nullify(original);
> original.howmany; // 0
> ```

## Comparing objects
When you compare objects, you'll get `true` only if you compare two references to the same object.  
Comparing two distinct objects that happen to have the exact same methods and properties will return `false`.

> #### Example
> ```js
> var fido  = {breed: 'dog'};
> var benji = {breed: 'dog'};
> ```
>
> ```js
> benji === fido // false
> benji == fido  // false
> ```
>
> ```js
> var mydog = benji;
> mydog === benji // true
> mydog === fido  // false
> ```
