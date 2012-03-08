# Built-ins

- - -
## Object methods

- - -
# Built-ins

## Object methods

```js
var o = {};
var o = new Object();
```

An empty object already contains some methods and properties:

* `o.constructor`
* `o.toString()`
* `o.valueOf()`

- - -
## Function methods

- - -
# Built-ins

## Function methods

### `call(thisArg, param...)`

It allows your objects to borrow methods from other objects and invoke them as their own.

```js
var greets = function (breed, birth) {
  return "Hi I'm " + this.firstName + " " + breed + 
         ", I was born in " + birth + ".";
}

var mickey = {
  firstName: 'Mickey'
};

var donald = {
  firstName: 'Donald'
};

greets.call(mickey, 'Mouse', 1928); 
//"Hi I'm Mickey Mouse, I was born in 1928."

greets.call(donald, 'Duck', 1934); 
//"Hi I'm Donald Duck, I was born in 1934."
```

- - -
# Built-ins

## Function methods

### `apply(thisArg, arrayArg)`

It has the same behaviour of `call` but different signature.

```js
var greets = function (breed, birth) {
  return "Hi I'm " + this.firstName + " " + breed + 
         ", I was born in " + birth + ".";
}

var mickey = {
  firstName: 'Mickey'
};

var donald = {
  firstName: 'Donald'
};

greets.apply(mickey, ['Mouse', 1928]); 
//"Hi I'm Mickey Mouse, I was born in 1928."

greets.call(donald, ['Duck', 1934]); 
//"Hi I'm Donald Duck, I was born in 1934."
```

- - -
# Built-ins

## Function methods

### `thisArg` parameter

 if `null` is passed defaults to the global object

```js
var greets = function (breed, birth) {
  return "Hi I'm " + this.firstName + " " + breed + 
         ", I was born in " + birth + ".";
}

greets.apply(null, ['Mouse', 1928]);
//"Hi I'm undefined Mouse, I was born in 1928."

var firstName = 'Goofy';
greets.apply(null, ['Goof', 1932]);
//"Hi I'm Goofy Goof, I was born in 1932."
```

- - -
## Array

- - -
# Built-ins

## Array

### Definition

```js
var a = ['one', 'two', 'three'];
var empty = [];
var plain = [1+2,'four'];
var matrix = [[1,2,3], [4,5,6], [7,8,9]];
var sparseArray = [1,,,,5];
```

```js
var a = new Array(['one', 'two', 'three']);
```

- - -
# Built-ins

## Array

### Definition

Arrays are objects, but of a special type because:  

* the names of their properties are automatically assigned using numbers  
* they have a `length` property which contains the number of elements in the array  

```js
var a = ['one', 'two', 'three'];
a.length; //3
typeof a; //"object"
```

- - -
# Built-ins

## Array

## Access

Arrays can be accessed through square bracket notation.

```js
var a = ['one', 'two', 'three'];
a[1]; //"two"
a['1']; //"two"
a[1] = 2
a[1]; //2
var matrix = [[1,2,3], [4,5,6], [7,8,9]];
matrix[0][1]; //2
```

- - -
## Array methods

- - -
# Built-ins

## Array methods

### Overview

```js
push(item...)
pop()
shift()
unshift(item...)
reverse()
sort(comparefn)
join(separator)
concat(item...)
slice(start, end)
splice(start, deleteCount, item...)
indexOf(item, startPos)
lastIndexOf(item, startPos)
every(function(item, index, array) {...}, scope)
some(function(item, index, array) {...}, scope)
filter(function(item, index, array) {...}, scope)
forEach(function(item, index, array) {...}, scope)
map(function(item, index, array) {...}, scope)
reduce(function(prev, cur, index, array) {...}, initVal)
reduceRight(function(prev, cur, index, array) {...}, initVal)
```

- - -
# Built-ins

## Array methods

### `push(item...)` method

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
# Built-ins

## Array methods

### `pop()` method

It acceps no parameter.  
It returns and removes the last element in the array.  
If the array is empty, return undefined.

    !js
    var colors = new Array('red', 'green', 'black');

    var item = colors.pop(); // get the last item
    item; // "black"
    colors.length; // 2
    colors; // ["red", "green"]

- - - 
# Built-ins

## Array methods

### sort(comparefn)
The default comparing function is the lexicographical order.

```js
var values = [0, 1, 5, 10, 15];
values.sort();
values;   // 0,1,10,15,5
```

```js
var compare = function (value1, value2) {
 return value2 - value1;
};

var values = [0, 1, 5, 10, 15];
values.sort(compare);
values;   // 0,1,5,10,15
```

- - -
# Built-ins

## Array methods

### Iterative methods: `every`, `filter`, `forEach`, `map`, `some`

Each of the iterative methods accepts two arguments:

* a function to run on each item
* an optional scope object in which to run the function (affecting the value of `this`)

The function passed into one of these methods will receive three arguments:

1. the array item value
2. the position of the item in the array
3. the array object itself

- - - 
# Built-ins

## Array methods

### `every(iterator, scope)`

Runs the given function on every item in the array and returns `true` if the function returns `true` for every item.

```js
var numbers = [1,2,3,4,5,4,3,2,1];

var everyResult = numbers.every(function(item, index, array) {
 return (item > 2);
});

everyResult;   //false
```

```js
var numbers = [3,5,3,4,5,4,3,8,9];

var everyResult = numbers.every(function(item) {
 return (item > 2);
});

everyResult;   //true
```

- - -
# Built-ins

## Array methods

### `some(iterator, scope)`

Runs the given function on every item in the array and returns `true`if the function returns `true` for any one item.

```js
var numbers = [1,2,3,4,5,4,3,2,1];

var someResult = numbers.some(function(item, index, array) {
 return (item > 2);
});

someResult;   //true
```

```js
var numbers = [1,2,3,4,5,4,3,2,1];

var someResult = numbers.some(function(item, index, array) {
 return (item > 5);
});

someResult;   //false
```

- - -
# Built-ins

## Array methods

### `filter(iterator, scope)`

Runs the given function on every item in the array and returns an array of all items for which the function returns `true`.

```js
var numbers = [1,2,3,4,5,4,3,2,1];

var filterResult = numbers.filter(function(item, index, array){
 return (item > 2);
});

filterResult;   //[3,4,5,4,3]
```

- - -
# Built-ins

## Array methods

### `forEach(oterator, scope)`

Runs the given function on every item in the array. This method has no return value.

```js
var numbers = [1,2,3,4,5,4,3,2,1];

numbers.forEach(function(item, index, array){   
   //do something here
});
```

- - -
# Built-ins

## Array methods

### `map(iterator, scope)`

Runs the given function on every item in the array and returns the result of each function call in an array.

```js
var numbers = [1,2,3,4,5,4,3,2,1];

var mapResult = numbers.map(function(item, index, array){
   return item * 2;
});

mapResult;   // [2,4,6,8,10,8,6,4,2]
```

- - -
# Built-ins

## Array methods

### Reduction methods: `reduce`, `reduceRight`

Both methods accept two arguments:

* a function to call on each item
* an optional initial value upon which the reduction is based

The passed function accepts four arguments: 

1. the previous value 
2. the current value 
3. the item's index 
4. the array object

Any value returned from the function is automatically passed in as the first argument for the next item.

- - -
# Built-ins

## Array methods

### `reduce(iterator, initVal)`

Perform reduction in left-to-right order.

```js
var values = [1,2,3,4,5];

var sum = values.reduce(function(prev, cur, index, array){
 return prev + cur;
});

sum; // 15
```

- - -
# Built-ins

## Array methods

### `reduceRight(iterator, initVal)`

Perform reduction in right-to-left order.

```js
var values = [1,2,3,4,5,15];

var diff = values.reduceRight(function(prev, cur, index, array){
 return prev - cur;
});

diff; // 0
```

- - -
# Built-in object `Math`

- - -
# Built-ins

## Built-in object `Math`

### Properties overview

```js
Math.E        // the value of e, the base of the natural logarithms
Math.LN10     // the natural logarithm of 10
Math.LN2      // the natural logarithm of 2
Math.LOG2E    // the base 2 logarithm of e
Math.LOG10E   // the base 10 logarithm of e
Math.PI       // the value of π
Math.SQRT1_2  // the square root of 1⁄2
Math.SQRT2    // the square root of 2
```

- - -
# Built-ins

## Built-in object `Math`

### Methods overview

```js
Math.min(n0,n1,...)  // Returns the minimum value
Math.max(n0,n1,...)  // Returns the maximum value
Math.ceil(num)       // Rounds number up to the nearest integer value
Math.floor(num)      // Rounds number down to the nearest integer value
Math.round(num)      // Rounds number
Math.random()        // Returns a random number in [0,1)
Math.exp(num)        // Returns Math.E raised to the power of num
Math.log(num)        // Returns the natural logarithm of num
Math.pow(num, power) // Returns num raised to the power of power
Math.sqrt(num)       // Returns the square root of num
Math.acos(x)         // Returns the arc cosine of x
Math.asin(x)         // Returns the arc sine of x
Math.atan(x)         // Returns the arc tangent of x
Math.atan2(y, x)     // Returns the arc tangent of y/x
Math.cos(x)          // Returns the cosine of x
Math.sin(x)          // Returns the sine of x
Math.tan(x)          // Returns the tangent of x
```

- - -
## RegExp

- - -
# Built-ins

## RegExp

### Regex literals

```js
var expression = /pattern/flags;
```

Flags can be:

* g — global mode, meaning the pattern will be applied to all of the string instead of stopping after the first match is found
* i — case-insensitive mode, meaning the case of the pattern and the string are ignored when determining matches
* m — multiline mode, meaning the pattern will continue looking for matches after reaching the end of one line of text

- - -
# Built-ins

## RegExp

### Methods overview

```js
exec(str)
test(str)
```

- - -
## String methods

- - -
# Built-ins

## String methods

### Overview

```js
charAt(pos)
charCodeAt(pos)
concat(str...)
indexOf(searchString, position)
lastIndexOf(searchString, position)
match(regexp)
search(regexp)
slice(start, end)
split(separator, limit)
toLowerCase()
toUpperCase()
```

- - -
## Date

- - -
# Built-ins

## Date

### Definition

The Date type stores dates as the number of milliseconds that have passed since midnight on January 1, 1970 UTC (Universal Time Code)

```js
var now = new Date();
```

```js
now.toDateString(); //"Thu Mar 08 2012"
now.toString();     //"Thu Mar 08 2012 10:41:02 GMT+0100 (CET)"
```

- - -
# Built-ins

## Date

### Definition

Date constructor accept many format

```js
var someDate = new Date("May 25, 2004");
var someDate = new Date("25/5/2004");
var someDate = new Date('Tue May 25 2004 00:00:00 GMT-0700');
var someDate = new Date('2004-05-25T00:00:00');
```
