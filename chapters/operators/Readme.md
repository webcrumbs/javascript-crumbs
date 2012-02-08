# Operators

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

```js
var a = 123;
var b = ++a;
a; //124
b; //124
```

#### post-increment 
increments the input value by 1 after the statement is evaluated.

```js
var a = 123;
var b = a++;
a; //124
b; //123
```

#### pre-decrement 
decremented the input value by 1 before the statement is evaluated.

```js
var a = 123;
var b = ++a;
b; //124
a; //124
```

#### post-decrement 
decremented the input value by 1 after the statement is evaluated.

```js
var a = 123;
var b = a--;
b; //123
a; //122
```

> #### Note
> The increment and decrement operators follow these rules regarding values:
>
> * when used on a string that is a valid number, convert to a number and apply the change;  
> the variable is changed from a string to a number
> * when used on a string that is not a valid number, convert to `NaN`;  
> the variable is changed from a string to a number  
> * when used on a boolean, convert to a number (`false` in `0`, `true` in `1`) and apply the change;  
> the variable is changed from a boolean to a number
> * when used on a floating-point value, apply the change;  
> the variable is just a number
> * when used on an object, call its `valueOf()` method to get a value to work with and apply the change;  
> the variable is changed from an object to a number
> 
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

> #### Tip
> If you use the logical NOT twice, you get the original value.
>  
> ```js
> !!true; //true
> ```
>
> Using double negation is an easy way to convert any value to its boolean equivalent.
> This is rarely useful, but on the other hand understanding how any value converts to a boolean is important.
> Most values convert to true with the exception of the following (which convert to false):
>
> * the empty string ""
> * null
> * undefined
> * the number 0
> * the number NaN
> * the boolean false
> 
> If you use a logical operator on a non-boolean value, the value is converted to boolean behind the scenes.
> 
> ```js
> !"one"; //false
> ```
> 
> These six values are sometimes referred to as being falsy, while all others are truthy
> (including, for example, the strings "0", " ", and "false").

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
