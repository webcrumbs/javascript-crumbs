# Objects
 
- - -
# Objects

## Using `this` value

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

- - -
# Objects

## Constructor functions

They are another way to create objects.  
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

- - -
# Objects

## Constructor functions

Constructor functions accept parameters, which can be used when creating new objects.

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

- - -
# Objects

## Constructor functions

> #### Warning 
> calling a function that is designed to be a constructor but
> omitting the `new` operator may result in a behaviour you could not expect.
>
> ```js
> var h = Hero('Leonardo');
> typeof h   // "undefifined"
> ```
>
> #### Note
> In this case, `this` refer to global object.

- - -
# Objects

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

- - -
# Objects

## The global object

> #### Exmaple
>```js
>function Hero(name) { this.name = name; }
>
>var h = Hero('Leonardo');
>typeof h   // "undefined"
>typeof h.name   // TypeError: Cannot read property 'name' of undefined
>```
>
> `this` is binded to global object
> 
> continue...

- - -
# Objects

## The global object

> ...continue
> 
>```js
>name   // "Leonardo"
>window.name   // "Leonardo"
>```
>
> using `new` operator instead
>
>```js
>var h2 = new Hero('Michelangelo');
>typeof h2   // "object"
>h2.name   // "Michelangelo"
>```

- - -
#Objects

## `constructor` property

When an object is created, this special property is assigned to it behind the scenes.  
It contains a reference to the constructor function used to create this object.  

> #### Exmaple
>```js
>function Hero(name) { this.name = name; }
>var h = new Hero('Leonardo');
>
>h.constructor // Hero(name)
>```
>
> following code means:
> "I don't care how object `h` was created,
> but I want another one just like it"
>
> ```js
> var h2 = new h.constructor('Rafaello');
> h2.name; // "Rafaello"
> ```

- - -
#Objects

## `constructor` property

If an object was created using the object literal notation,  
its constructor is the built-in `Object()` constructor function.

> #### Example
>
>```js
>var o = {};
>o.constructor; // Object();
>typeof o.constructor; // "function"
>```

- - -
# Objects

## `instanceof` operator
Using the instanceof operator, you can test if an object was created with a specific constructor function.

> #### Example￼
>
>```js￼
>function Hero() {}
>var h = new Hero();
>var o = {};
>h instanceof Hero;   //true
>h instanceof Object; //true
>o instanceof Object; //true
>o instanceof Hero;   //false
>```

- - -
# Objects

## Passing objects

When you copy an object or pass it to a function, you only pass a reference to that object.  
Consequently, if you make a change to the reference, you are actually modifying the original object.

> #### Example
>
>```js
>var original = { howmany: 1 };
>var copy = original;
>copy.howmany; //￼1
>copy.howmany = 100;
>original.howmany; // 100
>```

The same thing applies when passing objects to functions:

> #### Example
>
> ```js
> var original = { howmany: 100 };
> var nullify = function(o) { o.howmany = 0; }
> nullify(original);
> original.howmany; // 0
> ```

- - -
# Objects

## Comparing objects

When you compare objects, you'll get `true` only if you compare two references to the same object.  
Comparing two distinct objects that happen to have the exact same methods and properties will return `false`.

> #### Example
>
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
