# Types

- - -

# Types

## Variables

JavaScript variables are **loosely typed**:  
a variable is simply a named placeholder for a value of any type.

- - -

# Types

## Variables

#### definition

To define a variable, use the `var` operator followed by the variable name.

```js
var variable_name;
```

- - -

# Types

## Variables

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

- - -

# Types

## Data types

There are five simple data types (or primitive types):

* Null  
* Undefined  
* Boolean  
* Number  
* String  

and one complex data type:

* Object

All values can be represented as one of these six data types.  

- - -

# Types

## Data types

### Null

`null` is a special value that all variables are considered to have  
if they have been defined but have not been assigned a value. 

`null` is a reserved word and cannot be used for anything,  
but to check that a variable does not have an assigned value.

- - -

# Types

## Data types

### Undefined

Javascript treats `undefined` as being equal to `null`.  

The one difference between `null` and `undefined` is that  
`null` is a reserved word while `undefined` is not. 

```js
var undefined = 'hello'; // legal, but not reccomended
```

- - -

# Types

## Data types

### Booleans

Boolean data type has only two values:  
`true` and `false`, used without quotes.

```js
var t = true;
var f = false;
```

- - -

# Types

## Data types

### Numbers

#### Integer

```js
var int1 = 1;
var int2 = 2;
var int3 = 3;
// ...
```

- - -

# Types

## Data types

### Numbers

#### Octal numbers

starts with digit zero `0`  
followed by a sequence of octal digits (`0` through `7`).  
 
```js
var octal1 = 070; //octal for 56
var octal2 = 079; //invalid octal - interpreted as 79
var octal3 = 008; //invalid octal - interpreted as 8
```

> #### Note
> If a number out of the range `0`-`7` is detected in the literal,  
> then the leading zero is ignored and the number is treated as a decimal.

- - -

# Types

## Data types

### Numbers

#### Hexadecimal numbers

starts with two characters `0x`  
followed by a sequence of hexadecimal digits (`0` through `9`, `A` through `F`).  

```js
var hex1 = 0x0;  //hexadecimal for 0
var hex2 = 0xA;  //hexadecimal for 10
var hex3 = 0X1F; //hexedecimal for 31
```

> #### Note
> Letters may be in uppercase or lowercase.

- - -

# Types

## Data types

### Numbers

#### Floating-Point Values

must include a decimal point `.`  
and at least one number after the decimal point.

```js
var float1 = 0.1;
var float2 = 1.2;
var float3 = 3.14;
```

- - -

# Types

## Data types

### Numbers

#### Floating-Point Values

decimal or digits after decimal can be omitted.

```js
var float4 = .07;  //missing decimal - interpreted as 0.07 preferred
var float5 = 1.;   //missing digit after decimal - interpreted as integer 1
var float6 = 10.0; //whole number - interpreted as integer 10
```

- - -

# Types

## Data types

### Numbers

#### e-notation

starts with a number (integer or floating-point)  
followed by letter `e` (or `E`)  
followed by the power of 10 to multiply by.

```js
1e1;    //10
1e+1;   //10
2e+3;   //2000
2e-3;   //0.002
123E-3; //0.123
```

- - -

# Types

## Data types

### Numbers

### Range of Values

the smallest representable number is  
`5e-324` stored in `Number.MIN_VALUE` 

the largest representable number is  
`1.7976931348623157e+308` stored in `Number.MAX_VALUE`

- - -

# Types

## Data types

### Numbers

#### Infinity

represents a number out of range of values  
(Number.MIN_VALUE through Number.MAX_VALUE)

the positive infinity is  
`Infinity` stored in `Number.POSITIVE_INIFINITY`

the negative infinity is  
`–Infinity` stored in `Number.NEGATIVE_INFINITY`

- - -

# Types

## Data types

### Numbers

#### Infinity

If a calculation returns either positive or negative Infinity,  
that value cannot be used in any further calculations,  
because Infinity has no numeric representation with which to calculate.

```js
Infinity - 1e307;    //Infinity 
Infinity - Infinity; //NaN
-Infinity * -1;      //Infinity
Infinity * -1;       //-Infinity
```

- - -

# Types

## Data types

### Numbers

#### Testing if a value is not out of range

To determine if a value is finite there is the `isFinite()` function.

```js
isFinite(Infinite);  //false
isFinite(-Infinite); //false
isFinite(Number.MAX_VALUE + Number.MAX_VALUE); //false
isFinite(Number.POSITIVE_INFINITE); //false
isFinite(Number.NEGATIVE_INFINITE); //false
isFinite(0); //true
isFinite(1.7e308); //true
isFinite(1.8e308); //false
```

- - -

# Types

## Data types

### Numbers

#### NaN

is the value that represent Not a Number,  

The value `NaN` has a couple of unique properties:

* `NaN` is contagious, any operation involving `NaN` always returns `NaN`
* `NaN` is not equal to any value, including `NaN`

```js
Nan + 1 * 2 / 3; //NaN
NaN == NaN;      //false
```

- - -

# Types

## Data types

### Numbers

#### Testing if a value is not a number

To determine if a value is "not a number" there is the `isNaN()` function.  

```js
isNaN(NaN);    //true  - NaN is NaN :)
isNaN(10);     //false - 10 is a number
isNaN("10");   //false - can be converted to number 10
isNaN("blue"); //true  - cannot be converted to a number
isNaN(true);   //false - can be converted to number 1
```

- - -

# Types

## Data types

## Strings

A string is a sequence of character placed between single or double quotes.

```js
"some characters";
'some characters and numbers 123 5.87';
'1';
"";
"'hello'";
'"hello"';
'hello"; //syntax error - quotes must match
```

- - -

# Types

## Data types

## Strings

#### Character Literals

nonprintable or otherwise useful characters

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


- - -

# Types

## Data types

## Strings

#### Character Literals

```js
'he said \'hello\''; //"he said 'hello'"
"he said \"hello\""; //"he said "hello""
'\u03a3';            //"Σ"
'\x41';              //"A"
```

- - -

# Types

## Data types

## Object

An object is an unordered collection of key/value pairs,  
separated by commas `,`, placed within curly braces `{` and `}`.

The keys are strings, the values can be of any type (even Object).

```js
{
    s: 'string value'
  , n: 123
  , b: true
  , o: {
      k: 2
    }
}
```

- - -

# Types

## Data types

## Object

The keys can optionally be placed in quotation marks.  

```js
var obj = {
    "s": 'string value'
  , 'key': 'another value'
  , "name with spaces": true
}; 

