# From past lessons...

- - -
## types

* `null`
* `undefined`
* `boolean`
* `number`
* `string`
* `object`

- - -
## operators

* `typeof`
* `===`, `!==`
* `!`, `&&`, `||`

- - -
## Logical AND

### `&&` operator
    
    !js
    var v = v && 15;
    console.log(v);

Experiment by first setting `v` to `100`, `0`, `null`.

### Exmaple:

    !js
    var test = true;
    test && console.log('test is true!');

- - -
## Logical OR

### `||` operator
    
    !js
    var v = v || 10;

Experiment by first setting `v` to `100`, `0`, `null`.

### Exmaple:

    !js
    var empty = "";
    var myString = empty || "Hello Web :)";
    console.log(myString);

- - -

# New stuff

- - -

# Statements

- - -
## `if`

blabla
- - -
## `while`

blabla
- - -
## `do while`

blabla
- - -
## `for`

blabla
- - -
## `for in`

blabla
- - -
# Objects

- - -
## definition
Objects are colleciton of key/value pairs.

    !js
    var hero = {
      breed: 'Turtle',
      occupation: 'Ninja'
    };

Keys are strings: sometimes you have to quote them.
    
    !js
    var o = {
     something: 1,
     'yes or no': 'yes',
     '!@#$%^&*': true
    };
- - -
## access properties
    
    !js
    var hero = {
     breed: 'Turtle',
     occupation: 'Ninja',
     'finger count':  3
    };

### Dot notation.

    !js
    hero.breed; // "Turtle"

### Square bracket notation.

    !js
    hero['finger count']; // 3

### If property name is stored in a variable, use it with square bracket notation.

    !js
    var keyName = 'occupation';
    hero[keyName]; // "Ninja"
- - -
## set properties

### Properties can be dynamically added and modified using both notations.

    !js
    var hero = {};
    hero.breed = 'turtle';
    hero['name'] = 'Leonardo';
    console.log(hero);

- - -
## delete properties

### Properties can be even deleted.

    !js
    var hero = {};
    hero.breed = 'turtle';
    hero['name'] = 'Rafaelo';
    delete hero.breed;

- - -
# Functions

- - -
## definition

blabla
- - -
## invocation

blabla
- - -
## arguments

blabla
- - -
## function as value

blabla
- - -
# Object methods

- - -
## definition
An object contains properties.  
Since functions are just data, a property of an object can contain a function.  
In this case, you say that this property is a *method*.

    !js
    var dog = {
     name: 'Benji',
     talk: function(){
       alert('Woof, woof!');
     }
    };

- - -
## invocation

    !js
    var hero = {
     breed: 'Turtle',
     occupation: 'Ninja',
     say: function() {
       return 'I am ' + hero.occupation;
     }
    }

    hero.say();    // "I am Ninja"
    hero['say'](); // "I am Ninja"

- - -
## `this` value 

Inside a method, there is a special way to access the object this method belongs to:  
by using the special value `this`.

    !js
    var hero = {
     name: 'Rafaelo',
     sayName: function() {
       return this.name;
     }
    }

    hero.sayName();   // "Rafaelo"
- - -
# Array

- - -
## definition

    !js
    var a = ['one', 'two', 'three'];
    var empty = [];
    var plain = [1+2,'four'];
    var matrix = [[1,2,3], [4,5,6], [7,8,9]];
    var sparseArray = [1,,,,5];

Arrays are objects, but of a special type because:  

* the names of their properties are automatically assigned using numbers starting from 0  
* they have a `length` property which contains the number of elements in the array  

    !js
    var a = ['one', 'two', 'three'];
    a.length; //3
    typeof a; //"object"

- - -
## access

Arrays can be accessed through square bracket notation.

    !js
    var a = ['one', 'two', 'three'];
    a[1]; //"two"
    a['1']; //"two"
    a[1] = 2
    a[1]; //2
    var matrix = [[1,2,3], [4,5,6], [7,8,9]];
    matrix[0][1]; //2

- - -
## `push(item...)` method

It accepts any number of item to push in the array.  
It returns the array's new length.  

    !js
    var colors = [];   // create an array
    var count = colors.push('red', 'green'); // push any number of items
    count;  // 2
    colors; // ["red", "green"]

    count = colors.push('black');   // push another item on
    count;  // 3
    colors; // ["red", "green", "black"]
- - - 
## `pop()` method

It acceps no parameter.  
It returns and removes the last element in the array.  
If the array is empty, return undefined.

    !js
    var colors = new Array('red', 'green', 'black');

    var item = colors.pop(); // get the last item
    item; // "black"
    colors.length; // 2
    colors; // ["red", "green"]



