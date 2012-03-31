# Operators

## The `typeof` Operator

Because JavaScript is loosely typed, there needs to be a way to determine the data type of a given variable.  
The `typeof` operator provides a way to determine the data type of a given variable.  
Using the `typeof` operator on a value returns one of the following strings:

* `"undefined"` if the value is undefined
* `"boolean"` if the value is a boolean
* `"string"` if the value is a string
* `"number"` if the value is a number
* `"object"` if the value is an object or null
* `"function"` if the value is a function

> #### Example
>
> ```js
> typeof undefined;       // "undefined"
> typeof null;            // "object"
> typeof true;            // "boolean"
> typeof 'false';         // "string"
> typeof 'hello';         // "string"
> typeof 42;              // "number"
> typeof 1.4142135;       // "number"
> typeof {key: 'value' }; // "object"
> typeof Math.sin;        // "function"
> typeof function () {};  // "function"
> ```

> #### Note
> because `typeof` is an operator and not a function  
> no parentheses are required (although they can be used)
> 
> ```js
> typeof('hello'); //OK
> typeof 'hello';  //OK
> ```
> 
> #### Note
> because special value `null` is considered an empty object reference  
> `typeof null` returns `"object"`
> 
> ```js
> typeof null; // "object"
> ```
>
> #### Note
> although functions are considered objects and don’t represent another data type  
> they do have some special properties, which differentiate them from other objects:  
> `typeof` applied to a function returns `"function"` not `"object"`
> 
> ```js
> typeof function(){}; // "function"
> ```

## Unary Operators

Unary operators are operators that work on only one value.  
They are the simplest operators in JavaScript.

### increment/decrement

The increment operator is represented by `++` and increments the value by 1;  
the decrement operator is represented by `--` and decrements the value by 1.

The increment and decrement operators can be used in two versions, prefix and postfix:  

* the prefix versions of the operators are placed before the variable they work on,  
and is applied before the statement is evaluated;
* the postfix versions of the operators are placed after the variable,  
and is applied after the statement is evaluated.

#### pre-increment 
increments the input value by 1 before the statement is evaluated.

> #### Example
> ```js
> var a = 123;
> var b = ++a;
> a; //124
> b; //124
> ```

#### post-increment 
increments the input value by 1 after the statement is evaluated.

> #### Example
> ```js
> var a = 123;
> var b = a++;
> a; //124
> b; //123
> ```

#### pre-decrement 
decremented the input value by 1 before the statement is evaluated.

> #### Example
> ```js
> var a = 123;
> var b = --a;
> b; //122
> a; //122
> ```

#### post-decrement 
decremented the input value by 1 after the statement is evaluated.

> #### Example
> ```js
> var a = 123;
> var b = a--;
> b; //123
> a; //122
> ```

When used on a nonnumeric value, these operators convert the value to a number and then apply the change:

* when used on a string that is a valid number, convert to a number and apply the change;  
the variable is changed from a string to a number
* when used on a string that is not a valid number, convert to `NaN`;  
the variable is changed from a string to a number  
* when used on a boolean, convert to a number (`false` in `0`, `true` in `1`) and apply the change;  
the variable is changed from a boolean to a number
* when used on a floating-point value, apply the change;  
the variable is just a number
* when used on an object, call its `valueOf()` method to get a value to work with and apply the change;  
the variable is changed from an object to a number

> #### Example
> ```js
> var s = "10";
> ++s; //11
> ```
> ```js
> var x = "hello";
> ++x; //NaN
> ```
> ```js
> var b = true;
> ++b; //2
> ```
> ```js
> var f = 0.07;
> ++f; 1.07;
> ```
> ```js
> var o = { valueOf: function () { return 100; } };
> ++o; //101
> ```

### Unary plus and minus

#### Unary plus
is represented by a single plus sign `+` placed before a variable and returns its numeric value:  
when used on a numeric values, it does nothing to a numeric value but return the value;  
when used on a nonnumeric value, it converts the value to a number and return the result:

* when used on a string that is a valid number, convert to a number and return the result
* when used on a boolean, convert to a number (`false` in `0`, `true` in `1`) and return the result
* when used on an object, call its `valueOf()` method to get a value to work with and return the result

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

#### Unary minus
is represented by the character minus `-` placed before a value and simply negate it:  
when used on a numeric value, it simply negates the value;  
when used on nonnumeric values, it applies all of the same rules as unary plus and then negates the result.

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

## Bitwise operators

#### Bitwise NOT
is represented by the tilde character `~` and simply returns the one’s complement of the number.

```js
var num1 = 25;     //binary 0000 0000 0000 0000 0000 0000 0001 1001
var num2 = ~num1;  //binary 1111 1111 1111 1111 1111 1111 1110 0110
console.log(num2); //-26
```

#### Bitwise AND
is represented by the ampersand character `&` and works on two values;  
it lines up the bits in each number and then performs an AND operation between the bits in the same position.

```js
var a = 25;        //binary 0000 0000 0000 0000 0000 0000 0001 1001
var b = 11;        //binary 0000 0000 0000 0000 0000 0000 0000 1011
var c = a & b;     //binary 0000 0000 0000 0000 0000 0000 0000 1001
console.log(c);    //9
```

#### Bitwise OR
is represented by the pipe character `|` and works on two values;  
it lines up the bits in each number and then performs an OR operation between the bits in the same position.

```js
var a = 25;        //binary 0000 0000 0000 0000 0000 0000 0001 1001
var b = 11;        //binary 0000 0000 0000 0000 0000 0000 0000 1011
var c = a | b;     //binary 0000 0000 0000 0000 0000 0000 0001 1011
console.log(c);    //27
```

#### Bitwise XOR
is represented by the caret character `^` and works on two values;  
it lines up the bits in each number and then performs a XOR operation between the bits in the same position.

```js
var a = 25;        //0000 0000 0000 0000 0000 0000 0001 1001 
var b = 3;         //0000 0000 0000 0000 0000 0000 0000 0011
var c = a ^ b;     //0000 0000 0000 0000 0000 0000 0001 1010
console.log(c);    //26
```

## Logical Operators

#### Logical NOT
is represented by `!` and negate the boolean value.

```js
!true;  //false
!false; //true
```

when used on a non-boolean value, it converts the value to a boolean and return the result;  
most values convert to `true` with the exception of the following (which convert to `false`):

* the empty string `""`
* `null`
* `undefined`
* the number `0`
* the number `NaN`
* the boolean `false`

> #### Tip
> If you use the logical NOT twice, you get the original value.  
> Use double negation to easily convert any value to its boolean equivalent.
>  
> ```js
> !!false;     //false
> !!"";        //false
> !!null;      //false
> !!undefined; //false
> !!0;         //false
> !!NaN;       //false
> !!true;      //true
> !!"0";       //true
> !!1;         //true
> ```

#### Logical AND
is represented by `&&` and returns the logical AND of the operands.

```js
true && true;   //true
true && false;  //false
false && true;  //false
false && false; //false
```

#### Logical OR
is represented by `||` and returns the logical OR of the operands.

```js
true || true;   //true
true || false;  //true
false || true;  //true
false || false; //false
```

> #### Tip
> If you mix logical operators in the same expression,  
> you should use parentheses to clarify how you intend the operation to work.
> 
> ```js
> false && false || true && true;     //true
> false && (false || true) && true;   //false
> ```
> 
> Assuming there are no parentheses that demand otherwise,  
> `!` is executed first, then comes `&&` and finally `||`.
> 
> ```js
> false && false || true && true;     //true
> (false && false) || (true && true); //true
> ```
> 
> Use parentheses instead of relying on operator precedence,  
> in order to make your code easier to read and understand.

## Multiplicative operators

#### Multiply
is represented by an asterisk `*` and is used, as one might suspect, to multiply two numbers:  

* if the operands are numbers, performs regular arithmetic multiplication
* if the result cannot be represented, the result is `Infinity` or `–Infinity`
* if either operand is `NaN`, the result is `NaN`
* if `Infinity` is multiplied by zero, the result is `NaN`
* if `Infinity` is multiplied by a nonzero finite number, the result is `Infinity` or `-Infinity`,  
  depending on the sign of the number
* if `Infinity` is multiplied by `Infinity`, the result is `Infinity`
* if either operand isn’t a number, it is converted to a number using Number()  
and then the other rules are applied

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

#### Divide
is represented by a slash `/` and divides the first operand by the second operand:

* if the operands are numbers, regular arithmetic division is performed
* if the result can’t be represented, the result is `Infinity` or `–Infinity`
* if either operand is `NaN`, the result is `NaN`
* if `Infinity` is divided by `Infinity`, the result is `NaN`
* if zero is divided by zero, the result is `NaN`
* if a nonzero finite number is divided by zero, the result is `Infinity` or `–Infinity`,  
depending on the sign of the first operand
* if `Infinity` is divided by any number, the result is `Infinity` or `–Infinity`,  
depending on the sign of the second operand
* if either operand isn’t a number, it is converted to a number using Number()  
and then the other rules are applied

```js
25 * 2;              //12.5
NaN / 3;             //NaN
0 / 0;               //NaN
1 / 0;               //Infinity
Infinity / 0;        //Infinity
Infinity / 1;        //Infinity
Infinity / -2;       //-Infinity
Infinity / Infinity; //NaN
"3" / true;          //3
```

#### Modulus
is represented by a percent sign `%` and return the remainder of the division:

* if the operands are numbers, regular arithmetic division is performed,  
and the remainder of that division is returned.
* if the dividend is an infinite number and the divisor is a finite number, the result is `NaN`
* if the dividend is a finite number and the divisor is `0`, the result is `NaN`
* if `Infinity` is divided by `Infinity`, the result is `NaN`
* if the dividend is a finite number and the divisor is an infinite number, the result is the dividend
* if the dividend is zero and the divisor is nonzero, the result is zero
* if either operand isn’t a number, it is converted to a number using Number()  
and then the other rules are applied

## Additive Operators

### Add
is represented by `+` and is used just as one would expect:

* if either operand is `NaN`, the result is `NaN`
* if `Infinity` is added to `Infinity`, the result is `Infinity`
* if `–Infinity` is added to `–Infinity`, the result is `–Infinity`
* if `Infinity` is added to `–Infinity`, the result is `NaN`
* if `+0` is added to `+0`, the result is `+0`
* if `–0` is added to `+0`, the result is `+0`
* if `–0` is added to `–0`, the result is `–0`
* if one of the operands is a string
 * if both operands are strings, the second string is concatenated to the first
 * if only one operand is a string, the other operand is converted to a string  
   and the result is the concatenation of the two strings
 * if either operand is an object, number, or boolean, it is converted to a string calling its `toString()` method  
   and then the other rules regarding strings are applied
 * if either operand is `undefined` or `null`, it is converted to `"undefined"` or `"null"`  
   and then the other rules regarding strings are applied

```js
Infinity + Infinity;   //Infinity
-Infinity + -Infinity; //-Infinity
Infinity + -Infinity;  //NaN
0 + 0;                 //0
-0 + 0;                //0
-0 + -0;               //-0
1 / (-0 + -0);         //-Infinity
5 + 5;                 //10
5 + "5";               //"55"
true + "5";            //"true5"
```

#### Subtract
is represented by `-` and is used just as one would expect:

* if the two operands are numbers, perform arithmetic subtract and return the result
* if either operand is `NaN`, the result is `NaN`
* if `Infinity` is subtracted from `Infinity`, the result is `NaN`
* if `–Infinity` is subtracted from `–Infinity`, the result is `NaN`
* if `–Infinity` is subtracted from `Infinity`, the result is `Infinity`
* if `Infinity` is subtracted from `–Infinity`, the result is `–Infinity`
* if `+0` is subtracted from `+0`, the result is `+0`
* if `–0` is subtracted from `+0`, the result is `–0`
* if `–0` is subtracted from `–0`, the result is `+0`
* if either operand is a string, a boolean, `null`, or `undefined`,  
it is converted to a number using `Number()` and the arithmetic subtract is performed
* if either operand is an object, its valueOf() method is called to retrieve a numeric value to represent it  
and the arithmetic subtract is performed
* if the object doesn’t have `valueOf()` defined, then `toString()` is called 
and the resulting string is converted into a number

```js
5 - true;  //4 because true is converted to 1
NaN - 1;   //NaN
5 - 3;     //2
5 - "";    //5 because "" is converted to 0 
5 - "2";   //3 because "2" is converted to 2
5 - null;  //5 because null is converted to 0
```

## Relational Operators

The relational operators perform comparisons between values:

* less-than `<`
* greater-than `>`
* less-than-or-equal-to `<=`
* greater-than-or-equal-to `>=` 

When using different data types:

* if the operands are numbers, perform a numeric comparison
* if the operands are strings, compare the character codes of each corresponding character in the string
* if one operand is a number, convert the other operand to a number and perform a numeric comparison
* if an operand is an object, call `valueOf()` and use its result to perform the comparison,  
if `valueOf()` is not available, call `toString()` and use its result to perform the comparison
* if an operand is a boolean, convert it to a number and perform the comparison

## Equality operators

#### Equal and Not Equal

The equal operator is represented by `==`, and returns `true` if the operands are equal.  
The not-equal operator is represented by `!=`, and returns `true` if two operands are not equal. 

Both operators do conversions to determine if two operands are equal:

* if an operand is a boolean, convert to a number (`false` in `0`, `true` in `1`) and check for equality
* if one operand is a string and the other is a number, convert the string to a number and check for equality
* if either one of the operands is an object and the other is not,  
call `valueOf()` on the object and use its result to check for equality
* `null` and `undefined` are equal
* `null` and `undefined` cannot be converted into any other values for equality checking
* if either operand is `NaN`, the equal operator returns `false`  
and the not-equal operator returns `true`
* if both operands are `NaN`, the equal operator returns `false`  
because, by rule, `NaN` is not equal to `NaN`
* if both operands are objects, then they are compared to see if they are the same object,  
if both operands point to the same object, then the equal operator returns `true`, otherwise `false`

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

#### Identically Equal and Not Identically Equal

The identically equal and not identically equal operators do the same thing as equal and not equal,  
except that they do not convert operands before testing for equality. 

The identically equal operator is represented by `===`  
and returns `true` only if the operands are equal without conversion.

The not identically equal operator is represented `!==`  
and returns `true` only if the operands are not equal without conversion

```js
"55" == 55;  //true - equal because of conversion
"55" === 55; //false - not equal because different data types
```
```js
"55" != 55; //false - equal because of conversion
"55" !== 55; //true - not equal because different data types
```

> #### Note
> `null == undefined` is `true` because they are similar values,  
> `null === undefined` is `false` because they are not the same type.

> #### Tip
> Because of the type conversion issues with the equal and not-equal operators,  
> use identically equal and not identically equal instead,  
> in order to maintain data type integrity throughout your code.

## Conditional Operator

The *conditional operator* (also called *ternary operator*) is represented by `?` and `:`  
and return one of two values depending on the evaluation of a boolean expression:  

* if the boolean expression is `true`, return value defined after `?` 
* if the boolean expression is `false`, return value defined after `:`

```js
boolean_expression ? true_value : false_value;
```

> #### Example
> ```js
> var max = (num1 > num2) ? num1 : num2;
> ```

## Assignment Operators

#### Simple assignment
is represented by `=` and simply assigns the value on the right to the variable on the left.

```js
var variable = value;
```

#### Compound assignment
exist for each of the major mathematical operations and a few others as well:

* multiply/assign `*=`
* divide/assign `/=`
* modulus/assign `%=`
* add/assign `+=`
* subtract/assign `-=`
* left shift/assign `<<=`
* signed right shift/assign `>>=`
* unsigned right shift/assign `>>>=`

> #### Note
> Compound-assignment operators are designed specifically as shorthand ways of achieving operations,  
> they do not represent any performance improvement.

### Comma Operator
#### comma operator 
allows execution of more than one operation in a single statement.

> #### Tip
> Comma operator can be used in the declaration of variables
> 
> ```js
> var a, b = 1, c = 2;
> a; //undefined
> b; //1
> c; //2
> ```
>
> Comma operator can be used to assign value to a variable,  
> it returns the last item in the expression.
>
> ```js 
> var n = (0, 1, 2, 3, 4, 5);
> n; //5
> ```