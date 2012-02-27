# Built-in objects

## Object
Object is the parent of all JavaScript objects, which means that every created object inherits from it.  
To create a new empty object you can use the literal notation or the `Object()` constructor function.  

```js
var o = {};
var o = new Object();
```

An empty object already contains some methods and properties:

* `o.constructor` property returns the constructor function
* `o.toString()` is a method that returns a string representation of the object
* `o.valueOf()` returns a single-value representation of the object, often this is the object itself


## Array
Arrays are objects, but of a special type because:

* the names of their properties are automatically assigned using numbers starting from 0
* they have a `length` property which contains the number of elements in the array
* they have additional built-in methods in addition to those inherited from the parent object

### Array definition

#### Array initializer
Array literal notation makes use of square bracket.  
Elements of the array are separated by comma `,`.

```js
var a = [el1, el2, el3];
```

> #### Example
> an empty array: no expressions inside brackets means no elements
>
>```js
>var empty = [];
>```
>
> a 2-element array. First element is 3, second is the string `'four'`
>
>```js
>var plain = [1+2,'four'];
>```
>
> nested array
>
>```js
>var matrix = [[1,2,3], [4,5,6], [7,8,9]];
>```
>
> sparse array
>
>```js
>var sparseArray = [1,,,,5];
>```

#### Array constructor function
Arrays can be created through Arrays constructor function

```js
var empty = new Array();
```

> #### Example
>
>```js
>var plain = new Array(2+1,'four');
>var a = new Array(5);
>empty.length; // 0
>plain.length; // 2
>a.length;     // 5
>```
>
> `Array` is a constructor function for arrays
>
>```js
>plain.constructor; // function Array() ...
>```
>
> an array is an object
>
>```js
>typeof a; // "object"
>```


### Stack methods: push, pop
A stack is referred to as a last-in-first-out (LIFO) structure.  
The insertion (called a push) and removal (called a pop) of items in a stack occur at only one point: the top of the stack.  

#### push(item...)
It accepts any number of item to push in the array.  
It returns the array's new legth.

> #### Example
>```js
>var colors = new Array();   // create an array
>var count = colors.push('red', 'green'); // push any number of items
>count;  // 2
>colors; // ["red", "green"]
>
>count = colors.push('black');   // push another item on
>count;  // 3
>colors; // ["red", "green", "black"]
>```

#### pop()
It acceps no parameter.
It returns and removes the last element in the array.
If the array is empty, return `undefined`.

> #### Example
>```js
>var colors = new Array('red', 'green', 'black');
>
>var item = colors.pop(); // get the last item
>item; // "black"
>colors.length; // 2
>colors; // ["red", "green"]
>```

### Queue methods: shift, unshift
Queues restrict access in a first-in-first-out (FIFO) data structure.  
A queue adds items to the end of a list and retrieves items from the front of the list.  
It's possible to make an array behave like a queue with `push` and `shift` methods.  
An inverse queue instead is obtainable using `pop` and `unshift` methods.


#### shift()
It accepts no parameters.
It return and remove the first element in the array.
If the array is empty, return `undefined`.

> #### Example
>```js
>var colors = new Array('red', 'green', 'black');
>
>var item = colors.shift(); // get the first item
>colors.length; // 2
>item; // "red"
>```

> #### Tip
> shift is usually much slower than `pop`


#### unshift(item...)
It accepts any number of parameters to shove onto the front of te array.
It returns array's new legth. 

> #### Example
>```js
>var colors = new Array('red', 'green', 'black');
>
>var count = colors.unshift('purple', 'yellow');
>count; // 5
>colors: // ["purple", "yellow", "red", "green", "black"]
>```

### Reordering methods: reverse, sort


#### reverse()
Modify the array by reversing the order of the elements.  
It accepts no parameters.  
It returns the array.  

> #### Example
>```js
>var values = [1, 2, 3, 4, 5];
>values.reverse();
>values;   // 5,4,3,2,1
>```

#### sort(comparefn)
It sorts the array's elements.  
It accepts an optional comparing function according to which sort the array.  
The default comparing function is the lexicographical order.  
It returns the array.

> #### Example
>```js
>var values = [0, 1, 5, 10, 15];
>values.sort(); // default behaviour
>values;   // 0,1,10,15,5
>```
>
> defining a comparing function:
>
>```js
>function compare(value1, value2) {
>  return value2 - value1;
>}
>
>var values = [0, 1, 5, 10, 15];
>values.sort(compare);
>values;   // 0,1,5,10,15
>```


### Presentation methods: join

#### join(separator)
It accepts an optional separator parameter, defaulting to `,`.  
It returns a string by making a string of each of the array’s elements, and then concatenating them all together with a separator between them.

> #### Example
>```js
>var a = ['a', 'b', 'c'];
>var c = a.join(''); // 'abcd';
>```

> #### Tip
> to assemble a string from a large number of pieces, it is usually faster to put the pieces into an array and join them than concatenate the pieces with the `+` operator


### Manipulation methods: concat, slice, splice

#### concat(item...)
It accepts any number of items.  
It returns a shallow copy of the array with the items appended to it. If an item is an array then each of its elements is appended individually.  

> #### Example
>```js
>var colors = ['red', 'green', 'blue'];
>
>var colors2 = colors.concat('yellow', ['black', 'brown']);
>colors;  // ["red", "green", "blue"]
>colors2; // ["red", "green", "blue", "yellow", "black", "brown"]
>```

#### slice(start, end)
It accepts the `start` position and optionally `end` position, which default to array's length.  
It returns a shallow copy of a portion of the array.  
If either the start or end position of `slice()` is a negative number, then the number is subtracted from the length of the array to determine the appropriate locations.  
Calling `slice(-3, -1)` on an array with five items is the same as calling `slice(2, 4)`.  
If the end position is smaller than the start, then an empty array is returned.

> #### Example
>```js
>var colors = ['red', 'green', 'blue', 'yellow', 'purple'];
>
>var colors2 = colors.slice(1);
>colors2; // ["green", "blue", "yellow", "purple"]
>
>var colors3 = colors.slice(1, 4);
>colors3; // ["green", "blue", "yellow"]
>```

#### splice(start, deleteCount, item...)
It accepts:
  `start`: the number of a position within the array  
  `deleteCount`:  the number of elements to delete starting from `start` position
  `item...`: optional, any number of items to insert starting from `start` position
It returns an array containing the deleted elements.

> #### Example
> removing elements:
>
>```js
>var colors = ['red', 'green', 'blue'];
>
>var removed = colors.splice(0,1); // remove the first item
>colors;  // green,blue
>removed; // ["red"]
>```
>
> inserting elements:
>
>```js
>var colors = ['red', 'green', 'blue'];
>
>removed = colors.splice(1, 0, 'yellow', 'orange');  // insert two items at position 1
>colors;  // green,yellow,orange,blue
>removed; // empty array
>```
>
> replacing elements:
>
>```js
>var colors = ['red', 'green', 'blue'];
>
>removed = colors.splice(1, 1, 'red', 'purple');   // insert two values, remove one
>colors;    // green,red,purple,orange,blue
>removed;   // yellow - one item array
>```

### Location methods: indexOf, lastIndexOf

#### indexOf(item, startPos) 
It accepts:
  an `item` to search for, starting from the front of the array and continues to the back  
  an optional `startPos` to indicate the starting point of the search, which default to 0. If `startPos` is negative, array's length is added to it.  
It returns the position of the item in the array or –1 if the item isn’t in the array.  
`===` is used in comparison.  

> #### Example
>```js
>var numbers = [1,2,3,4,5,4,3,2,1];
>
>var index = numbers.indexOf(4);   
>index; // 3
>```
>
>```js
>var numbers = [1,2,3,4,5,4,3,2,1];
>
>var index = numbers.indexOf(4, 4);
>index; // 5
>```
>
>```js
>var person = { name: 'Nicholas' };
>var people = [{ name: 'Nicholas' }];
>
>var morePeople = [person];
>people.indexOf(person);   // -1
>morePeople.indexOf(person);   // 0
>```

#### lastIndexOf(item, startPos) 
It accepts:
  an `item` to search for, starting from the back of the array and continues to the front 
  an optional `startPos` to indicate the starting point of the search, which default to array's length. If `startPos` is negative, array's length is added to it.
It returns the last position of the item in the array or –1 if the item isn’t in the array.  
`===` is used in comparison.  

> #### Example
>```js
>var numbers = [1,2,3,4,5,4,3,2,1];
>
>var index = numbers.lastIndexOf(3);   
>index; // 6
>```
>
>```js
>var numbers = [1,2,3,4,5,4,3,2,1];
>
>var index = numbers.lastIndexOf(4, -4);
>index; // 2
>```

### Iterative methods: every, filter, forEach, map, some
Each of the iterative methods accepts two arguments:

  1. a function to run on each item
  2. an optional scope object in which to run the function (affecting the value of `this`)

The function passed into one of these methods will receive three arguments:

  1. the array item value
  2. the position of the item in the array
  3. the array object itself

#### every(function(item, pos, array) {...}, scope)
Runs the given function on every item in the array and returns true if the function returns true for every item.

> #### Example
>```js
>var numbers = [1,2,3,4,5,4,3,2,1];
>
>var everyResult = numbers.every(function(item, index, array) {
>  return (item > 2);
>});
>
>everyResult;   //false
>```

#### some(function(item, pos, array) {...}, scope)
Runs the given function on every item in the array and returns true if the function returns true for any one item.

> #### Example
>```js
>var someResult = numbers.some(function(item, index, array) {
>  return (item > 2);
>});
>
>someResult;   //true
>```

#### filter(function(item, pos, array) {...}, scope)
Runs the given function on every item in the array and returns an array of all items for which the function returns true.

> #### Example
>```js
>var numbers = [1,2,3,4,5,4,3,2,1];
>
>var filterResult = numbers.filter(function(item, index, array){
>  return (item > 2);
>});
>
>filterResult;   //[3,4,5,4,3]
>```

#### forEach(function(item, pos, array) {...}, scope)
Runs the given function on every item in the array. This method has no return value.

> #### Example
>```js
>var numbers = [1,2,3,4,5,4,3,2,1];
>
>numbers.forEach(function(item, index, array){   
>    //do something here
>});
>```

#### map(function(item, pos, array) {...}, scope)
Runs the given function on every item in the array and returns the result of each function call in an array.

> #### Example
>```js
>var numbers = [1,2,3,4,5,4,3,2,1];
>
>var mapResult = numbers.map(function(item, index, array){
>    return item * 2;
>});
>
>mapResult;   // [2,4,6,8,10,8,6,4,2]
>```

### Reduction methods: reduce, reduceRight
Both methods accept two arguments:

  1. a function to call on each item
  2. an optional initial value upon which the reduction is based

The passed function accepts four arguments:
  1. the previous value
  2. the current value
  3. the item's index
  4. the array object

Any value returned from the function is automatically passed in as the first argument for the next item.  
The first iteration occurs on the second item in the array.  


#### reduce(function(previous, current, index, array) {...}, initVal)
Perform reduction in left-to-right order.

> #### Example
>```js
>var values = [1,2,3,4,5];
>
>var sum = values.reduce(function(previous, current, index, array){
>  return prev + cur;
>});
>
>sum;   // 15
>```

### reduceRight(function(previous, current, index, array) {...}, initVal)
Perform reduction in right-to-left order.

> #### Example
>```js
>var values = [1,2,3,4,5,15];
>
>var sum = values.reduceRight(function(previous, current, index, array){
>  return prev - cur;
>});
>
>sum;   // 0
>```

## Function

### Properties of the Function objects
Like any other object, functions have a constructor property that contains a reference to the `Function()` constructor function.

```js
function myfunc(a) { return a; }
myfunc.constructor   // Function()
```

Functions also have a `length` property, which contains the number of parameters the function accepts.

> #### Example
>```js
>function myfunc(a, b, c) { return true; }
>myfunc.length   // 3
>```

The most important property of a function is the `prototype` property.  
The `prototype` property of a function contains an object.  
It is only useful when you use this function as a constructor.  
All objects created with this function keep a reference to the `prototype` property and can use its properties as their own.

> #### Example
>```js
>var some_obj = {
>  name: 'Ninja',
>  say: function(){
>    return 'I am a ' + this.name;
>  }
>}

An hollow function automatically has a prototype property that contains an empty object.

> #### Example
>```js
>function F() {}
>typeof F.prototype // "object"
>
>F.prototype = some_obj;
>
>var obj = new F();
>obj.name;  // "Ninja"
>obj.say(); // "I am a Ninja"
>```

### Methods of the Function objects
Two useful methods of the function objects are `call()` and `apply()`.  
They allow your objects to borrow methods from other objects and invoke them as their own.


#### call(thisArg, param...)
It accepts:
`thisArg` parameter will be bind to `this` in function execution, which default to the global object (even if `null` is passed);  
any number of `params` to pass to the function.

> #### Example
>```js
>var some_obj = {
>  name: 'Ninja',
>  say: function(who) {
>    return 'Haya ' + who + ', I am a ' + this.name;
>  }
>}
>
>some_obj.say('Dude');   // "Haya Dude, I am a Ninja"
>
>my_obj = {name: 'Scripting guru'};
>
>some_obj.say.call(my_obj, 'Dude')   // "Haya Dude, I am a Scripting guru"
>```

When `say()` was invoked with `call`, the references to `this` value that it contains, pointed to `my_obj`.  
This way `this.name` didn't return `Ninja`, but `Scripting guru` instead.

If you don't pass an object as a first parameter to `call()` or pass `null`, the global object will be assumed.

#### apply(thisArg, arrayArg)
It accepts:
`thisArg` parameter will be bind to `this` in function execution, which default to the global object (even if `null` is passed);  
an array of parameters to pass to the function.  

> #### Example
> the two following code line are equivalent
>
>```js
>some_obj.someMethod.apply(my_obj, ['a', 'b', 'c']);
>some_obj.someMethod.call(my_obj, 'a', 'b', 'c');
>
>some_obj.say.apply(my_obj, ['Dude']);   // "Haya Dude, I am a Scripting guru"
>```

## Boolean
`Boolean()` Function is the constructor for the wrapping object of the Boolean values.  

```js
var booleanObject = new Boolean(true);
```

Pay attention to not use Boolean object as Boolean expression.

```js
var falseObject = new Boolean(false);
var result = falseObject && true;
result; // true

var falseValue = false;
result = falseValue && true;
result; // false

typeof falseObject; // object
typeof falseValue;  // boolean
falseObject instanceof Boolean; // true
falseValue instanceof Boolean;  // false
```

The `Boolean()` function is useful when called as a normal function, without `new`.  
This converts non-booleans to booleans (which is the same as using a double negation `!!` value).  

> #### Example
>```js
>Boolean("test") // true
>Boolean("")     // false
>Boolean({})     // true
>```

## Number
`Number()` Function is the constructor for the wrapping object of the numeric values.

> #### Example
>```js
>var numberObject = new Number(10);
>```

Pay attention to use Number instead of primitive Number value.

```js
var numberObject = new Number(10);
var numberValue = 10;
typeof numberObject;   // "object"
typeof numberValue;   // "number"
numberObject instanceof Number; // true
numberValue instanceof Number;  // false
```

`Number()` function contains some interesting built-in properties (which you cannot modify):

```js
Number.MAX_VALUE   // 1.7976931348623157e+308
Number.MIN_VALUE   // 5e-324
Number.POSITIVE_INFINITY   // Infinity
Number.NEGATIVE_INFINITY   //-Infinity
Number.NaN   // NaN
```

`Number()` function without `new` converts any value ti a number.

> #### Example
>```js
>var n = Number('12.12');
>n   // 12.12
>typeof n   // "number"
>```

### Number object's methods
#### toString(radix)
It optionally accepts a single argument indicating the radix in which to represent the number.  
It returns a string representation of the number in the given radix.  

> #### Example
>```js
>var num = 10;
>num.toString();   // "10"
>num.toString(2);  // "1010"
>num.toString(8);  // "12"
>num.toString(10); // "10"
>num.toString(16); // "a"
>```

#### toFixed(dec)
It accepts an arguments indicating how many decimal places should be displayed.  
It returns a string representation of a number with a specified number of decimal points.  

> #### Example
>```js
>var num = 10;
>num.toFixed(2); // "10.00"
>
>var num = 10.005;
>num.toFixed(2); // "10.01"
>```

#### toExponential(dec)
It accepts one argument, which is the number of decimal places to output.  
It returns a string with the number formatted in exponential notation.  

> #### Example
>```js
>var num = 10;
>num.toExponential(1);   // "1.0e+1"
>```

#### toPrecision(digits)
It accepts the total number of digits to use to represent the number (not including exponents).  
It returns either the fixed or the exponential representation of a number, depending on which makes the most sense.  

> #### Example
>```js
>var num = 99;
>num.toPrecision(1);   // "1e+2"
>num.toPrecision(2);   // "99"
>num.toPrecision(3);   // "99.0"
>```

## String
String type is the object representation for strings.  
`length` property indicates number of character.  

> #### Example
>```js
>var stringObject = new String('I love JavaScript!');
>console.log(stringObject.length);   // > 11
>```

Strings allow for bracket notation access to single character.

> #### Example
>```js
>var stringValue = 'hello world';
>console.log(stringValue[1]);   // > "e"
>```

`String()` function without `new` converts the parameter to a primitive string.

> #### Example
>```js
>String(1) // "1"
>String({p: 1}) // "[object Object]"
>String([1,2,3]) // "1,2,3"
>```

### String object's methods

#### charAt(pos)
It accepts a single argument, which is the character’s zero-based position.  
It returns the character in the given position as a single-character string, like bracket notation access.  

> #### Example
>```js
>var stringValue = 'hello world';
>stringValue.charAt(1); // > "e"
>```

#### charCodeAt(pos)
It accepts a single argument, which is the character’s zero-based position.  
It returns the character code in the given string position.  

> #### Example
>```js
>var stringValue = 'hello world';
>stringValue.charCodeAt(1); // 101
>```

#### concat(str...)  
It accepts any number of strings to concatenate as arguments.  
It returns a new string obtained by concatenating one or more strings to another.

> #### Example
>```js
>var stringValue = 'hello, ';
>var result = stringValue.concat('my ', 'name ', 'is ', 'Bob');
>result; // "hello, my name is Bob"
>stringValue; // "hello, "
>```

#### indexOf(searchString, position)
It accepts:
a string to search for inside string;  
an optional starting search position.  
It returns the position of the first matched character; if no mathes are found, it returns –1.  

> #### Example
>```js
>var text = 'Mississippi';
>var p = text.indexOf('ss');
>console.log(p);   // 2
>p = text.indexOf('ss', 3);   // 5
>p = text.indexOf('ss', 6);   // -1
>```

#### lastIndexOf(searchString, position)
Like the `indexOf` method, except that it searches from the end of the string instead of the front:

> #### Example
>```js
>var text = 'Mississippi';
>var p = text.lastIndexOf('ss');
>p; // 5
>
>p = text.lastIndexOf('ss', 3);
>p; // 2
>
>p = text.lastIndexOf('ss', 6);
>p; // 5
>```

#### match(regexp)
The match method matches a string and a regular expression.  
It accepts a regexp.  
If the `g` flag is setted then it returns an array of all the matches but excludes the capturing groups.  
Otherwise the result of calling string.match(regexp) is the same as calling regexp.exec(string).  

> #### Example
>```js
>var text = '<html><body bgcolor=linen><p>' + 'This is <b>bold<\/b>!<\/p><\/body><\/html>';
>
>var tags = /[^<>]+|<(\/?)([A-Za-z]+)([^<>]*)>/g;
>text.match(tags); // ["<html>", "<body bgcolor=linen>", "<p>", "This is ", "<b>", "bold", "</b>", "!", "</p>", "</body>", "</html>"]
>```

#### replace(searchValue, replaceValue)
The replace method does a search and replace operation on the string, producing a new string.  
The `searchValue` argument can be a string or a regular expression object.  
If it is a string, only the first occurrence of the `searchValue` is replaced.

> #### Example
>```js
>var result = "mother_in_law".replace('_', '-');
>result; // "mother-in_law"
>```

If `searchValue` is a regular expression and if it has the `g` flag, then it will replace all occurrences.  
If it does not have the `g` flag, then it will replace only the first occurrence.

> #### Example
>```js
>var result = "mother_in_law".replace(/_/g, '-');
>result; // "mother-in-law"
>```
>
>```js
>var result = "mother_in_law".replace(/_/, '-');
>result; // "mother-in-law"
>```

The `replaceValue` can be a string or a function.  
If `replaceValue` is a string, the character `$` has special meaning:

```js
$ sequence | replacement
-----------|------------
$$           $
$&           The matched text
$number      Capture group text
$`           The text preceding the match 
$'           The text following the match
```

If the `replaceValue` is a function, it will be called for each match.  
That funciton accepts the matched text as first argument, following by text of capturing groups.  
The string returned by the function will be used as the replacement text.  

> #### Example
>```js
>function entitify (str) {
>
>  function replaceFunc (c) {
>    var character = {
>      '<' : '&lt;',
>      '>' : '&gt;',
>      '&' : '&amp;',
>      '"' : '&quot;'
>    };
>
>    return character[c];
>  }
>
>  return str.replace(/[<>&"]/g, replaceFunc);
>}
>
>var test = '<&>';
>entitify(test) // &lt;&amp;&gt;
>```

#### search(regexp)
It accepts a regular expression object.  
It returns the position of the first character of the first match, if there is one, or –1 if the search fails.  
The g flag is ignored.

> #### Example
>```js
>var text = 'and in it he says "Any damn fool could"';
>var pos = text.search(/["']/);  
>pos; // 18
>```

#### slice(start, end)
It returns a new string by copying a portion of another string.  
It accepts two arguments: _start_ and _end_ position of the string portion.  
End argument is optional, its default value is _string.length_.  
If _start_ or _end_ are negative then _string.length_ is added to them.

> #### Example
>```js
>var text = 'and in it he says "Any damn fool could"';
>var a = text.slice(18);
>a; // ""Any damn fool could"
> 
>var b = text.slice(0, 3);
>b; // "and"
>
>var c = text.slice(-5);
>c; // "could"
>
>var d = text.slice(19, 32);
>d; // "Any damn fool"
>```

#### split(separator, limit) 
It accepts a `separator` string or regexp and an optional `limit` parameter to limit the number of pieces that will be split.  
It returns a new array of strings by splitting the string into pieces.

> #### Example
>```js
>var digits = '0123456789';
>var a = digits.split('', 5); // ["0", "1", "2", "3", "4"]
>```
>
>```js
>var ip = '192.168.1.0';
>var b = ip.split('.');
>b; // ["192", "168", "1", "0"]
>```
>
>```js
>var ip = '192.168.1.0';
>var c = ip.split('.', 2);
>c; // ["192", "168"]
>```
>
>```js
>var text = 'last,  first  ,middle';
>var d = text.split(/\s*,\s*/);
>d; // ["last", "first", "middle"]
>```

#### substr(start, length) 
It returns a new string by copying a portion of another string.  
It accepts two arguments: the _start_ position and the _length_ of the string portion.  
_length_ argument is optional: its default value is `string.length - start`
If _start_ is negative then _string.length_ is added to it.

> #### Example
>```js
>var text = 'and in it he says "Any damn fool could"';
>var a = text.substr(10,7);
>a; // "he says"
>```

#### toLowerCase()
It returns a new string that is made by converting the string to lowercase.

#### toUpperCase()
It returns a new string that is made by converting the string to uppercase.

#### fromCharCode(char...)
It accepts any number of char code.
It returns a string from these series of char code.

> #### Example
>```js
>var a = String.fromCharCode(67, 97, 116);
>a; // "Cat"
>```

## Date
the Date type stores dates as the number of milliseconds that have passed since midnight on January 1, 1970 UTC (Universal Time Code)

### Date definition
Date objects can be created through Date constructor function.  

> #### Example
>```js
>var now = new Date();
>
>now.toDateString();
>now.toString();
>```

Date constructor accept many format:

* month/date/year (such as 6/13/2004)
* month_name date, year (such as January 12, 2004)
* day_of_week month_name date year hours:minutes:seconds time_zone (such as Tue May 25 2004 00:00:00 GMT-0700)
* ISO 8601 extended format YYYY-MM-DDTHH:mm:ss.sssZ (such as 2004-05-25T00:00:00)

> #### Example
>```js
>var someDate = new Date("May 25, 2004");
>var someDate = new Date("25/5/2004");
>var someDate = new Date('Tue May 25 2004 00:00:00 GMT-0700');
>var someDate = new Date('2004-05-25T00:00:00');
>```

### Date methods

### now
It accepts no parameters.  
It returns elapsed time since January 1, 1970 UTC in milliseconds.  

> #### Example 
>```js
>var start = Date.now(); //get start time   
>
>//call a function 
>doSomething();
>
>var stop = Date.now(); //get stop time
>var result = stop – start;
>```

> #### Tip
> now method is useful for profile function

## RegExp

### Regex literals

[Regular expressions](http://www.regular-expressions.info/) are easy to create.

```js
var expression = /pattern/flags;
```

Flags can be:

* `g` — global mode, meaning the pattern will be applied to all of the string instead of stopping after the first match is found
* `i` — case-insensitive mode, meaning the case of the pattern and the string are ignored when determining matches
* `m` — multiline mode, meaning the pattern will continue looking for matches after reaching the end of one line of text


> #### Example
> match all instances of "at" in a string
>```js
>var pattern1 = /at/g;
>```
>
> match the first instance of "bat" or "cat", regardless of case
> 
> ```js
>var pattern2 = /[bc]at/i;
>```
>
> match all three-character combinations ending with "at", regardless of case
>
>```js
>var pattern3 = /.at/gi;
>```
>
>_meta-characters_ : `( [ { \ ^ $ | ) ] } ? * + .`
>
>
> match the first instance of "bat" or "cat", regardless of case
>```js
>var pattern1 = /[bc]at/i;
>```
>
> match the first instance of "[bc]at", regardless of case
>
>```js
>var pattern2 = /\[bc\]at/i;
>
> match all three-character combinations ending with "at", regardless of case
>
>```js
>var pattern3 = /.at/gi;
>```
>
> match all instances of ".at", regardless of case
>
>```js
>var pattern4 = /\.at/gi;
>```
>
> match the first instance of "bat" or "cat", regardless of case
>
>```js
>var pattern1 = /[bc]at/i;
>```
>
> same as pattern1, just using the constructor
>
> ```js
>var pattern2 = new RegExp("[bc]at", "i");
>```

### Instance methods: exec, test

#### exec
It is intended for use with capturing groups `( ... )`.  
It accepts a single argument, which is the string on which to apply the pattern.  
It returns an array of information about the first match or _null_ if no match was found.  
The returned array, though an instance of Array, contains two additional properties:

  1. `index`, which is the location in the string where the pattern was matched
  2. `input`, which is the string that the expression was run against.

In the array, the first item is the string that matches the entire pattern, any additional items represent captured groups inside the expression.

> #### Example
>
>```js
>var text = "mom and dad and baby";
>var pattern = /mom( and dad( and baby)?)?/gi;
>
>var matches = pattern.exec(text);
>matches.index; // 0
>matches.input; // "mom and dad and baby"
>matches[0]; // "mom and dad and baby"
>matches[1]; // " and dad and baby"
>matches[2]; // " and baby"
>```
>
>```js
>var text = "cat, bat, sat, fat";
>var pattern1 = /.at/;
>
>var matches = pattern1.exec(text);
>matches.index; // 0
>matches[0]; // cat
>pattern1.lastIndex; // 0>
>
>matches = pattern1.exec(text);
>matches.index; // 0
>matches[0]; // cat
>pattern1.lastIndex; // 0
>```
>
>```js
>var text = "cat, bat, sat, fat";
>var pattern2 = /.at/g;
>
>var matches = pattern2.exec(text);
>matches.index; // 0
>matches[0]; // cat
>pattern2.lastIndex; // 0
>
>matches = pattern2.exec(text);
>matches.index; // 5
>matches[0]; // bat
>pattern2.lastIndex; // 8
>```

#### test
It accepts a string argument.
It returns _true_ if the pattern matches the argument and _false_ if it does not.

> Example
>```js
>var text = “000-00-0000";
>var pattern = /\d{3}-\d{2}-\d{4}/;
>if (pattern.test(text)) {
>  "The pattern was matched.";
>}
>```

## Math object
The built-in `Math` object is the common location for mathematical formulas and information.  
The computations available on the `Math` object execute faster than if you were to write the computations in JavaScript directly.

### Math object properties
The Math object has several properties, consisting mostly of special values in the world of mathematics.

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

### Math object methods

#### Math.min(n0,n1,...)
It accepts any number of values.  
It returns the minimum value.

> #### Example
>```js
>var min = Math.min(3, 54, 32, 16); alert(min); // 3
>```
>
>To find the maximum or the minimum value in an array, use the `apply()` method
>
>```js
>var values = [1, 8, 3, 5, 6, 7, 2];
>var maxValue = Math.max.apply(Math, values); // 8
>var minValue = Math.min.apply(Math, values); // 1
>```

#### Math.max(n0,n1,...)
It accepts any number of values.  
It returns the maximum value.

> #### Example
> ```js
>var maxValue = Math.max(3, 54, 32, 16); alert(max);   
>maxValue;// 54
>```
>
> To find the maximum or the minimum value in an array, use the `apply()` method
>
> ```js
>var values = [1, 8, 3, 5, 6, 7, 2];
>var maxValue = Math.max.apply(Math, values);
>maxValue; // 8
>```

#### Math.ceil(num)
It accepts a number.  
It rounds numbers up to the nearest integer value.

> #### Example
>```js
>Math.ceil(25.9); // 26
>Math.ceil(25.5); //26
>Math.ceil(25.1); // 26
>```

#### Math.floor(num)
It accepts a number.  
It rounds rounds numbers down to the nearest integer value.

> #### Example
>```js
>Math.floor(25.9);   // 25
>Math.floor(25.5);   // 25
>Math.floor(25.1);   // 25
>```

#### Math.round(num)
It accepts a number.  
It rounds up if the number is at least halfway to the next integer value (0.5 or higher) and rounds down if not.

> #### Example
>```js
>Math.round(25.9);   // 26
>Math.round(25.5);   // 26
>Math.round(25.1);   // 25
>```

#### random()
It accepts no parameters.  
It returns a random number between the 0 and the 1, not including either 0 or 1.

> #### Example
>```js
>```js
>/* To select a number between 1 and 10 */
>var num = Math.floor(Math.random() * 10 + 1);
>```

### Other Methods

```js
Math.abs(num)        // Returns the absolute value of num
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