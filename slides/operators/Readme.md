# Operators

- - -

# Operators

## The `typeof` Operator

`typeof value` returns:

* `"undefined"` if the `value` is undefined
* `"boolean"`   if the `value` is a boolean
* `"string"`    if the `value` is a string
* `"number"`    if the `value` is a number
* `"object"`    if the `value` is an object or null
* `"function"`  if the `value` is a function

- - -

# Operators

## The `typeof` Operator

```js
typeof undefined;       // "undefined"
typeof null;            // "object"
typeof true;            // "boolean"
typeof false;           // "boolean"
typeof 'false';         // "string"
typeof 'hello';         // "string"
typeof 42;              // "number"
typeof 1.4142135;       // "number"
typeof {key: 'value' }; // "object"
typeof Math.sin;        // "function"
typeof function () {};  // "function"
```

- - -

# Operators

## The `typeof` Operator

`typeof null` returns `"object"`  
because `null` is considered an empty object reference  

`typeof` applied to a function returns `"function"` not `"object"`  
although functions are considered objects and don’t represent another data type  
they do have some special properties, which differentiate them from other objects 

- - -

# Operators

## Unary Operators

### increment/decrement

#### pre-increment

`++value` increments `value` by `1` before the statement is evaluated

```js
var a = 123;
var b = ++a;
a; //124
b; //124
```

- - -

# Operators

## Unary Operators

### increment/decrement

#### post-increment 

`value++` increments `value` by `1` after the statement is evaluated

```js
var a = 123;
var b = a++;
a; //124
b; //123
```

- - -

# Operators

## Unary Operators

### increment/decrement

#### pre-decrement 

`--value` decremented `value` by `1` before the statement is evaluated

```js
var a = 123;
var b = ++a;
b; //124
a; //124
```

- - -

# Operators

## Unary Operators

### increment/decrement

#### post-decrement 

`value--` decremented `value` by `1` after the statement is evaluated

```js
var a = 123;
var b = a--;
b; //123
a; //122
```

- - -

# Operators

## Unary Operators

### increment/decrement

if `value` is a nonnumeric value, it is converted to a number:

* a string that represent a number is converted to that number  
* a string that don't represent a number is converted to `NaN`  
* a boolean `false` is converted to number `0`  
* a boolean `true` is converted to number `1`  
* an object is converted to the value returned by its method `valueOf()`

```js
var s = "10";
++s;            //11
```
```js
var x = ":(";
++x;            //NaN
```
```js
var b = true;
++b;            //2
```
```js
var f = 0.07;
++f;            //1.07;
```
```js
var o = { valueOf: function () { return 100; } };
++o;            //101
```

- - -

# Operators

## Unary Operators

### Unary plus and minus

#### Unary plus

`+value` returns numeric value of `value`  

```js
var n = 25;
n = +n; //still 25
```
```js
var s = "01";
s = +s; //value becomes numeric 1
```
```js
var s = "1.1";
s = +s; //value becomes numeric 1.1
```
```js
var s = "z";
s = +s; //value becomes NaN
```
```js
var b = false;
b = +b; //value becomes numeric 0
```
```js
var f = 1.1;
f = +f; //still 1.1
```
```js
var o = { valueOf: function () { return 1; } };
o = +o; //value becomes numeric 1
```

- - -

# Operators

## Unary Operators

### Unary plus and minus

#### Unary minus

`-value` returns the negation of the numeric value of `value`

```js
var n = 25;
n = -n; //-25
```
```js
var s = "01";
s = -s; //value becomes numeric -1
```
```js
var s = "1.1";
s = -s; //value becomes numeric -1.1
```
```js
var s = "z";
s = -s; //value becomes NaN
```
```js
var b = false;
b = -b; //value becomes numeric 0
```
```js
var f = 1.1;
f = -f; //value becomes -1.1
```
```js
var o = { valueOf: function () { return 1; } };
o = -o; //value becomes numeric -1
```

- - -

# Operators

## Bitwise operators

### Bitwise NOT

`~value` returns the one's complement of the number `value`.

```js
var a = 25;  //binary 0000 0000 0000 0000 0000 0000 0001 1001
var b = ~a;  //binary 1111 1111 1111 1111 1111 1111 1110 0110
b;           //-26
```

- - -

# Operators

## Bitwise operators

### Bitwise AND

`a & b` performs an AND operation between the bits of `a` and `b`

```js
var a = 25;        //binary 0000 0000 0000 0000 0000 0000 0001 1001
var b = 11;        //binary 0000 0000 0000 0000 0000 0000 0000 1011
var c = a & b;     //binary 0000 0000 0000 0000 0000 0000 0000 1001
c;                 //9
```

- - -

# Operators

## Bitwise operators

### Bitwise OR

`a | b` performs an OR operation between the bits of `a` and `b`

```js
var a = 25;        //binary 0000 0000 0000 0000 0000 0000 0001 1001
var b = 11;        //binary 0000 0000 0000 0000 0000 0000 0000 1011
var c = a | b;     //binary 0000 0000 0000 0000 0000 0000 0001 1011
c;                 //27
```

- - -

# Operators

## Bitwise operators

### Bitwise XOR

`a ^ b` performs a XOR operation between the bits of `a` and `b`

```js
var a = 25;        //0000 0000 0000 0000 0000 0000 0001 1001 
var b = 3;         //0000 0000 0000 0000 0000 0000 0000 0011
var c = a ^ b;     //0000 0000 0000 0000 0000 0000 0001 1010
c;                 //26
```

- - -

# Operators

## Logical Operators

### Logical NOT

`!value` negate the boolean value.

```js
!true;  //false
!false; //true
```

if `value` is a non-boolean value, it is converted to a boolean: 

most values are converted to `true`  
following values are converted to `false`

* the empty string `""`
* `null`
* `undefined`
* the number `0`
* the number `NaN`
* the boolean `false`

- - -

# Operators

## Logical Operators

### Logical NOT

#### Tip

If you use the logical NOT twice, you get the original value.  
Use double negation to easily convert any value to its boolean equivalent.
 
```js
!!false;     //false
!!"";        //false
!!null;      //false
!!undefined; //false
!!0;         //false
!!NaN;       //false
!!true;      //true
!!"0";       //true
!!1;         //true
```

- - -

# Operators

## Logical Operators

### Logical AND

`a && b` returns the logical AND of `a` and `b`.

```js
true && true;   //true
true && false;  //false
false && true;  //false
false && false; //false
```

- - -

# Operators

## Logical Operators

### Logical OR

`a || b` returns the logical OR of `a` and `b`

```js
true || true;   //true
true || false;  //true
false || true;  //true
false || false; //false
```

- - -

# Operators

## Logical Operators

### Operators precedence

`!` is executed first, then comes `&&` and finally `||`

Use parentheses instead of relying on operator precedence,  
in order to make your code easier to read and understand.

```js
false && false || true && true;     //true
(false && false) || (true && true); //true
```

- - -

# Operators

## Multiplicative operators

### Multiply

`*` multiply two numbers

```js
6 * 8;               //48
1e308 * 2;           //Infinity
NaN * 3;             //NaN
Infinity * 0;        //NaN
Infinity * 1;        //Infinity
Infinity * -2;       //-Infinity
Infinity * Infinity; //Infinity
"3" * true;          //3
```

- - -

# Operators

## Multiplicative operators

### Divide

`/` divides the first operand by the second operand

```js
25 * 2;              //12.5
NaN / 3;             //NaN
3 / NaN;             //NaN
0 / 0;               //NaN
1 / 0;               //Infinity
Infinity / 0;        //Infinity
Infinity / 1;        //Infinity
Infinity / -2;       //-Infinity
Infinity / Infinity; //NaN
"3" / true;          //3
```

- - -

# Operators

## Multiplicative operators

### Modulus

`%` returns the remainder of the division

- - -

# Operators

## Additive Operators

### Add

`+` returns the sum of its operands

```js
1 + NaN;               //NaN
NaN + 1;               //NaN
Infinity + Infinity;   //Infinity
-Infinity + -Infinity; //-Infinity
Infinity + -Infinity;  //NaN
0 + 0;                 //0
-0 + 0;                //0
-0 + -0;               //-0
1 / (-0 + -0);         //-Infinity
5 + 7;                 //12
"5" + 7;               //"57"
5 + "7";               //"57"
true + 5;              //6
true + "5";            //"true5"
```

- - -

# Operators

## Additive Operators

### Subtract

`-` returns the difference of its operands

```js
NaN - 1;               //NaN
2 - NaN;               //NaN
Infinity - Infinity;   //NaN
-Infinity - -Infinity; //NaN
Infinity - -Infinity;  //Infinity
-Infinity - Infinity;  //-Infinity
+0 - +0;               //+0
+0 - -0;               //-0
-0 - -0;               //+0
3 - true;              //2 - because true is converted to 1
NaN - 1;               //NaN
5 - 3;                 //2
5 - "";                //5 - because "" is converted to 0 
5 - "2";               //3 - because "2" is converted to 2
5 - null;              //5 - because null is converted to 0
```

- - -

# Operators

## Relational Operators

* less-than `<`
* greater-than `>`
* less-than-or-equal-to `<=`
* greater-than-or-equal-to `>=` 

- - -

# Operators

## Relational Operators

When using different data types:

* if the operands are numbers, perform a numeric comparison
* if the operands are strings, perform a lessicographic comparison
* if an operand is a number, convert the other operand to a number  
and perform a numeric comparison
* if an operand is an object, call its `valueOf()` method  
and use its result to perform the comparison,  
* if an operand is a boolean, convert it to a number and perform the comparison

- - -

# Operators

## Equality operators

### Equal and Not Equal

`a == b` returns `true` if `a` is equals to `b`  

`a != b` returns `true` if `a` is not equals to `b`  

#### Attention!
`==` and `!=` perform a type conversions

```js
null == undefined; //true
"NaN" == NaN;      //false
5 == NaN;          //false
NaN == NaN;        //false
NaN != NaN;        //true
false == 0;        //true
true == 1;         //true
true == 2;         //false
undefined == 0;    //false
null == 0;         //false
"5" == 5;          //true
```

- - -

# Operators

## Equality operators

### Strict Equal and Not Strict Equal

`===` returns `true` only if the operands are equal (without conversion)

`!==` returns `true` only if the operands are not equal (without conversion)

```js
"55" == 55;  //true  - equal because of conversion
"55" === 55; //false - not equal because different data types
```
```js
"55" != 55;  //false - equal because of conversion
"55" !== 55; //true  - not equal because different data types
```
```js
null == undefined;  //true  - because they are similar values  
null === undefined; //false - because they are not the same type
```

- - -

# Operators

## Equality operators

### Conditional Operator

```js
conditional_expression ? true_case : false_case;
```

if `conditional_expression` is `true`  
then returns `true_case` value  
else returns `false_case` value

```js
var max = (a > b) ? a : b;
```

- - -

# Operators

## Assignment Operators

### Simple assignment

`=` assigns the value on the right to the variable on the left

```js
var variable = value;
```

- - -

# Operators

## Assignment Operators

### Compound assignment

* multiply/assign `*=`
* divide/assign `/=`
* modulus/assign `%=`
* add/assign `+=`
* subtract/assign `-=`
* left shift/assign `<<=`
* signed right shift/assign `>>=`
* unsigned right shift/assign `>>>=`

- - -

# Operators

## Comma Operator

allows execution of more than one operation in a single statement

#### Tip
Comma operator can be used in the declaration of variables

```js
var a, b = 1, c = 2;
a; //undefined
b; //1
c; //2
```

```js 
var n = (0, 1, 2, 3, 4, 5);
n; //5
```
