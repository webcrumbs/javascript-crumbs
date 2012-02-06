# Operators

ECMA-262 describes a set of operators that can be used to manipulate data values.
The operators range from mathematical operations (such as addition and subtraction) and bitwise operators to relational operators and equality operators.
Operators are unique in ECMAScript in that they can be used on a wide range of values, including strings, numbers, booleans, and even objects.
When used on objects, operators typically call the valueOf() and/or toString() method to retrieve a value they can work with.

## Unary Operators

Operators that work on only one value are called unary operators.
They are the simplest operators in ECMAScript.

### increment/decrement

The increment and decrement operators are taken directly from C and come in two versions: prefix and postfix.
The prefix versions of the operators are placed before the variable they work on;
the postfix versions of the operators are placed after the variable.

When using the prefix versions of the operators,
the variable’s value is changed before the statement is evaluated.

When using the postfix versions of the operators,
the variable’s value is changed after the statement is evaluated.

pre-increment is when the input value is first incremented by 1 and then returned.

    var a = 123;
    var b = ++a;
    b; //124
    a; //124

post-increment is when the input value is incremented by 1 after it's returned.

    var a = 123;
    var b = a++;
    b; //123
    a; //124

pre-decrement is when the input value is first decremented by 1 and then returned.

    var a = 123;
    var b = ++a;
    b; //124
    a; //124

post-decrement is when the input value is decremented by 1 after it's returned.

    var a = 123;
    var b = a--;
    b; //123
    a; //122

All four of these operators work on any values, meaning not just integers but strings, booleans, floating-point values, and objects.
The increment and decrement operators follow these rules regarding values:

* When used on a string that is a valid representation of a number, convert to a number and apply the change.
The variable is changed from a string to a number.
* When used on a string that is not a valid number, the variable’s value is set to NaN.
The variable is changed from a string to a number.
* When used on a boolean value that is false (or true), convert to 0 (or 1) and apply the change.
The variable is changed from a Boolean to a number.
* When used on a floating-point value, apply the change by adding or subtracting 1.
* When used on an object, call its valueOf() method to get a value to work with and apply the change.
If the result is NaN, then call toString() and apply the change.
The variable is changed from an object to a number.

### Unary plus and minus

The unary plus is represented by a single plus sign (+) placed before a variable;
when it is applied to a numeric values, it does nothing to a numeric value.

When it is applied to a nonnumeric value, it converts the value to a number and return the result.
* When used on a string that is a valid representation of a number, convert to a number and return the result.
* When used on a boolean value that is false (or true), convert to 0 (or 1) and return the result.
* When used on an object, call its valueOf() method to get a value to work with and return the result.
If the result is NaN, then call toString() and return the result.

    var num = 25;
    var s1 = “01”;
    var s2 = “1.1”;
    var s3 = “z”;
    var b = false;
    var f = 1.1;
    var o = {
      valueOf: function () {
        return -1;
      }
    };

    num = +num; //still 25
    s1 = +s1; //value becomes numeric 1
    s2 = +s2; //value becomes numeric 1.1
    s3 = +s3; //value becomes NaN
    b = +b; //value becomes numeric 0
    f = +f; //no change, still 1.1
    o = +o; //value becomes numeric -1

The unary minus operator’s primary use is to negate a numeric value.
When used on a numeric value, it simply negates the value.
When used on nonnumeric values, it applies all of the same rules as unary plus and then negates the result:

￼￼￼￼var num = 25;
    var s1 = “01”;
    var s2 = “1.1”;
    var s3 = “z”;
    var b = false;
    var f = 1.1;
    var o = {
      valueOf: function() {
        return -1;
￼￼￼￼  }
    };

    num = -num; //becomes -25
    s1 = -s1; //value becomes numeric -1
    s2 = -s2; //value becomes numeric -1.1
    s3 = -s3; //value becomes NaN
    b = -b; //value becomes numeric 0
    f = -f; //change to -1.1
    o = -o; //value becomes numeric 1

## Bitwise operators

### Bitwise NOT

The bitwise NOT is represented by a tilde (~) and simply returns the one’s complement of the number.
Bitwise NOT is one of just a few ECMAScript operators related to binary mathematics.

    var num1 = 25;     //binary 0000 0000 0000 0000 0000 0000 0001 1001
    var num2 = ~num1;  //binary 1111 1111 1111 1111 1111 1111 1110 0110
    console.log(num2); //-26

### Bitwise AND

The bitwise AND is represented by the ampersand character (&) and works on two values;
it lines up the bits in each number and then performs an AND operation between the bits in the same position.
A bitwise AND returns 1 only if both bits are 1.

For example:

    var a = 25;        //binary 0000 0000 0000 0000 0000 0000 0001 1001
    var b = 11;        //binary 0000 0000 0000 0000 0000 0000 0000 1011
    var c = a & b;     //binary 0000 0000 0000 0000 0000 0000 0000 1001
    console.log(c);    //9

### Bitwise OR

The bitwise OR is represented by the pipe character (|) and works on two values;
it lines up the bits in each number and then performs an OR operation between the bits in the same position.
Bitwise OR operation returns 1 if at least one bit is 1 (returns 0 only if both bits are 0).

For example:

    var a = 25;        //binary 0000 0000 0000 0000 0000 0000 0001 1001
    var b = 11;        //binary 0000 0000 0000 0000 0000 0000 0000 1011
    var c = a | b;     //binary 0000 0000 0000 0000 0000 0000 0001 1011
    console.log(c);    //27

### Bitwise XOR

The bitwise XOR is represented by the pipe character (|) and works on two values;
it lines up the bits in each number and then performs an OR operation between the bits in the same position.
Bitwise XOR returns 1 only when exactly one bit has a value of 1 (returns 0 if both bits contain 1).

## Logical Operators

There are three operators, called logical operators, that work with boolean values:

* `!` logical NOT (negation)
* `&&` logical AND
* `||` logical OR

### Logical NOT

In everyday meaning, if something is not true, it is false.

    !true; //false

If you use the logical NOT twice, you get the original value.

    !!true; //true

Using double negation is an easy way to convert any value to its boolean equivalent.
This is rarely useful, but on the other hand understanding how any value converts to a boolean is important.
Most values convert to true with the exception of the following (which convert to false):

* the empty string ""
* null
* undefined
* the number 0
* the number NaN
* the boolean false

If you use a logical operator on a non-boolean value, the value is converted to boolean behind the scenes.

    !"one"; //false

These six values are sometimes referred to as being falsy, while all others are truthy
(including, for example, the strings "0", " ", and "false").

### Logical AND

When you use AND, the result is true only if all of the operands are true.

    true && true; //true
    true && false; //false
    false && true; //false
    false && false; //false

### Logical OR

When using OR, the result is true if at least one of the operands is true.

    true || true; //true
    true || false; //true
    false || true; //true
    false || false; //false

### Logical operator precedence

You can also mix && and || in the same expression.
In this case, you should use parentheses to clarify how you intend the operation to work.

    false && false || true && true; //true
    false && (false || true) && true; //false

Similarly for logical operations, assuming there are no parentheses that demand otherwise,
`!` has the highest precedence and is executed first, then comes `&&` and finally `||`.

    false && false || true && true; // true
    (false && false) || (true && true); //true

Use parentheses instead of relying on operator precedence.
This makes your code easier to read and understand.
