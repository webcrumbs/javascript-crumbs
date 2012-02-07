# Types

## Variables

JavaScript variables are **loosely typed**:  
a variable is simply a named placeholder for a value of any type.

#### definition

To define a variable, use the `var` operator followed by the variable name.

```js
var message;
```

#### initialization

Without initialization, a variable holds the special value `undefined`.  
It’s possible to define the variable and set its value at the same time.

```js
var message = 'hello!';
```

It's possible to change the value stored in the variable and also its type.

```js
var response = 'bye!';
response = 100;        //legal, but not recommended
```

## Data types

There are five simple data types (or primitive types):

* Undefined  
* Null  
* Boolean  
* Number  
* String  

and one complex data type:

* Object

All values can be represented as one of these six data types.  

### The typeof Operator

Because ECMAScript is loosely typed, there needs to be a way to determine the data type of a given variable.
The typeof operator provides a way to determine the data type of a given variable.
Using the typeof operator on a value returns one of the following strings:

* `"undefined"` if the value is undefined
* `"boolean"` if the value is a boolean
* `"string"` if the value is a string
* `"number"` if the value is a number
* `"object"` if the value is an object or null
* `"function"` if the value is a function

```js
typeof undefined;       // "undefined"
typeof null;            // "object"
typeof true;            // "boolean"
typeof 'false';         // "string"
typeof 'hello';         // "string"
typeof 42;              // "number"
typeof 1.4142135;       // "number"
typeof {key: 'value' }; // "object"
typeof Math.sin;        // "function"
typeof function () {};  // "function"
```

> #### Note
> because `typeof` is an operator and not a function  
> no parentheses are required (although they can be used)
> 
> because special value `null` is considered an empty object reference  
> `typeof null` returns `"object"`
> 
> although functions are considered objects and don’t represent another data type  
> they do have some special properties, which differentiate them from other objects:  
> operator `typeof` applied to a function returns `"function"` not `"object"`

## Numbers

### Integer

The simplest number is an integer.

```js
var intNum1 = 1;
var intNum2 = 2;
var intNum3 = 3;
```

Integers can also be represented as either octal (base 8) or hexadecimal (base 16) literals.  

> #### Note
> Numbers created using octal or hexadecimal format are treated as decimal numbers in all arithmetic operations.

#### Octal numbers
starts with digit zero `0` followed by a sequence of octal digits (`0` through `7`).  

```js
var octalNum1 = 070; //octal for 56
var octalNum2 = 079; //invalid octal - interpreted as 79
var octalNum3 = 008; //invalid octal - interpreted as 8
```

> #### Note
> If a number out of this range is detected in the literal,  
> then the leading zero is ignored and the number is treated as a decimal.

#### Hexadecimal numbers
starts with two characters `0x` followed by a sequence of hexadecimal digits (`0` through `9`, `A` through `F`).  

```js
var hexNum1 = 0x0;  //hexadecimal for 0
var hexNum2 = 0xA;  //hexadecimal for 10
var hexNum3 = 0X1F; //hexedecimal for 31
```

> #### Note
> Letters may be in uppercase or lowercase.

### Floating-Point Values

Floating-point value must include a decimal point `.` and at least one number after the decimal point.

```js
var floatNum1 = 1.1;
var floatNum2 = 0.1;
```

> #### Convention
> Although an integer is not necessary before a decimal point, it is recommended.
> ```js
> var floatNum3 = .1;  //valid, but not recommended
> ```

Because storing floating-point values uses twice as much memory as storing integer values,
ECMAScript always looks for ways to convert values into integers.
When there is no digit after the decimal point, the number becomes an integer.
If the number being represented is a whole number (such as 1.0), the number becomes an integer.

    var floatNum1 = 1.; //missing digit after decimal - interpreted as integer 1
    var floatNum2 = 10.0; //whole number - interpreted as integer 10

For very large or very small numbers, floating-point values can be represented using e-notation.
E-notation is used to indicate a number that should be multiplied by 10 raised to a given power.
E-notation format starts with a number (integer or floating-point)
followed by letter e (case-insensitive), followed by the power of 10 to multiply by.

    1e1;    //10
    1e+1;   //10
    2e+3;   //2000
    2e-3;   //0.002
    123E-3; //0.123

### Range of Values

Not all numbers in the world can be represented in JavaScript, because of memory constraints.
The smallest number is 5e-324, stored in Number.MIN_VALUE;
the largest number is 1.7976931348623157e+308, stored in Number.MAX_VALUE.

There is a special value in JavaScript called Infinity.
It represents a number too big for JavaScript to handle.
Infinity is indeed a number.

    typeof Infinity; //"number"

Any positive number that can’t be represented is Infinity (positive infinity), stored in Number.POSITIVE_INIFINITY.
any negative number that can’t be represented is –Infinity (negative infinity),

If a calculation returns either positive or negative Infinity, that value cannot be used in any further calculations,
because Infinity has no numeric representation with which to calculate.

To determine if a value is finite there is the isFinite() function.

    isFinite(Number.MAX_VALUE + Number.MAX_VALUE); //false
    isFinite(Infinite); //false
    isFinite(-Infinite); //false
    isFinite(Number.POSITIVE_INFINITE); //false
    isFinite(Number.NEGATIVE_INFINITE); //false
    isFinite(0); //true
    isFinite(1.7e308); //true
    isFinite(1.8e308); //false

Though it is rare to do calculations that take values outside of the range of finite numbers,
it is possible and should be monitored when doing very large or very small calculations.
You can also get the values of positive and negative Infinity by accessing Number.NEGATIVE_INFINITY and Number.POSITIVE_INFINITY.
As you may expect, these properties contain the values –Infinity and Infinity, respectively.

### NaN

There is a special numeric value called NaN, short for Not a Number,
which is used to indicate when an operation intended to return a number has failed (as opposed to throwing an error).

The value NaN has a couple of unique properties:

* NaN is contagious, any operation involving NaN always returns NaN
* NaN is not equal to any value, including NaN

    Nan + 1 * 2 / 3; //NaN
    NaN == NaN; //false

To determine if the value is “not a number” there is the isNaN() function.
When a value is passed into isNaN(), an attempt is made to convert it into a number.
Some non-number values convert into numbers directly, such as the string “10” or a Boolean value.
Any value that cannot be converted into a number causes the function to return true.

    isNaN(NaN); //true
    isNaN(10); //false - 10 is a number
    isNaN("10"); //false - can be converted to number 10
    isNaN("blue"); //true - cannot be converted to a number
    isNaN(true); //false - can be converted to number 1

## Strings

A string is a sequence of characters used to represent text.
In JavaScript, any value placed between single or double quotes is considered a string.

    var s = "some characters";
    var s = 'some characters and numbers 123 5.87';
    var s = '1';
    var s = "";
    var s = "'hello'";
    var s = '"hello"';
    var s = 'hello"; //syntax error - quotes must match

### Character Literals

The String data type includes several character literals to represent nonprintable or otherwise useful characters:

* `\n` new line
* `\t` tab
* `\b` backspace
* `\r` carriage return
* `\f` form feed
* `\\` backslash (`\`)
* `\'` single quote (`'`) — used when the string is delineated by single quotes.
* `\"` double quote (`"`) — used when the string is delineated by double quotes.
* \xnn a character represented by hexadecimal code nn (where n is a hexadecimal digit 0-F).
* \unnnn a unicode character represented by the hexadecimal code nnnn (where n is a hexadecimal digit 0-F).

for example:

    s = 'he said \'hello\''; //"he said 'hello'"
    s = "he said \"hello\""; //"he said "hello""
    s = '\u03a3';            //"Σ"
    s = '\x41';              //"A"

## Booleans

There are only two values that belong to the boolean data type: the values true and false, used without quotes.

    var b = true;
    typeof b; //"boolean"

    var b = false;
    typeof b; //"boolean"
