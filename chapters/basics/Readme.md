# Language Basics

### Variables

ECMAScript variables are loosely typed, meaning that a variable can hold any type of data.

Every variable is simply a named placeholder for a value.

To define a variable, use the `var` operator (`var` is a keyword) followed by the variable name (an identifier).

    var message;

This code defines a variable named `message` that can be used to hold any value.

Without initialization, a variable holds the special value `undefined`.
It’s possible to define the variable and set its value at the same time.

    var message = "hello!";

It's still possible to not only change the value stored in the variable but also change the type of value.

    var message = “hi”;
    message = 100;      //legal, but not recommended

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
Having only six data types may seem like too few to fully represent data;
however, these data types have dynamic aspects that make each single data type behave like several.

### The typeof Operator

Because ECMAScript is loosely typed, there needs to be a way to determine the data type of a given variable.
The typeof operator provides a way to determine the data type of a given variable.
Using the typeof operator on a value returns one of the following strings:

* "undefined" if the value is undefined
* "boolean" if the value is a boolean
* "string" if the value is a string
* "number" if the value is a number
* "object" if the value is an object or null
* "function” if the value is a function

for example:

    typeof undefined; // "undefined"
    typeof null; // "object"
    typeof true; // "boolean"
    typeof "false"; // "string"
    typeof "hello"; // "string"
    typeof 42; // "number"
    typeof 1.4142135; // "number"
    typeof { "key": "value" }; // "object"
    typeof Math.sin; // "function"
    typeof function () {}; // "function"

Note that because `typeof` is an operator and not a function, no parentheses are required (although they can be used).
Note that `typeof null` returns `"object"`, as the special value `null` is considered to be an empty object reference.

Technically, functions are considered objects in ECMAScript and don’t represent another data type.
However, they do have some special properties, which differentiate them from other objects.

### Numbers

#### Integer

The simplest number is an integer.

    var intNum1 = 1;
    var intNum2 = 2;
    var intNum3 = 3;

#### Octal and Hexadecimal numbers

Integers can also be represented as either octal (base 8) or hexadecimal (base 16) literals.
Numbers created using octal or hexadecimal format are treated as decimal numbers in all arithmetic operations.

Octal literal starts with digit zero (0) followed by a sequence of octal digits (0 through 7).
If a number out of this range is detected in the literal,
then the leading zero is ignored and the number is treated as a decimal.

    var octalNum1 = 070; //octal for 56
    var octalNum2 = 079; //invalid octal - interpreted as 79
    var octalNum3 = 008; //invalid octal - interpreted as 8

Hexadecimal literal starts with two characters 0x (case insensitive),
followed by any number of hexadecimal digits (0 through 9, and A through F).
Letters may be in uppercase or lowercase.

    var hexNum1 = 0xA; //hexadecimal for 10
    var hexNum2 = 0x1f; //hexedecimal for 31

#### Floating-Point Values

Floating-point value must include a decimal point and at least one number after the decimal point.
Although an integer is not necessary before a decimal point, it is recommended.

    var floatNum1 = 1.1;
    var floatNum2 = 0.1;
    var floatNum3 = .1; //valid, but not recommended

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

    1e1; //10
    1e+1; //10
    2e+3; //2000
    2e-3; //0.002
    123.456E-3; //0.123456

#### Range of Values

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

#### NaN

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

### Strings

A string is a sequence of characters used to represent text.
In JavaScript, any value placed between single or double quotes is considered a string.

    var s = "some characters";
    var s = 'some characters and numbers 123 5.87';
    var s = '1';
    var s = "";
    var s = "'hello'";
    var s = '"hello"';
    var s = 'hello"; //syntax error - quotes must match

#### Character Literals

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
    s = "\u03a3"; //"Σ"
    s = "\x41"; //"A"

### Booleans

There are only two values that belong to the boolean data type: the values true and false, used without quotes.

    var b = true;
    typeof b; //"boolean"

    var b = false;
    typeof b; //"boolean"

## Operators

ECMA-262 describes a set of operators that can be used to manipulate data values.
The operators range from mathematical operations (such as addition and subtraction) and bitwise operators to relational operators and equality operators.
Operators are unique in ECMAScript in that they can be used on a wide range of values, including strings, numbers, booleans, and even objects.
When used on objects, operators typically call the valueOf() and/or toString() method to retrieve a value they can work with.

### Unary Operators

Operators that work on only one value are called unary operators.
They are the simplest operators in ECMAScript.

#### increment/decrement

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

#### Unary plus and minus

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

### Bitwise operators

#### Bitwise NOT

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

### Logical Operators

There are three operators, called logical operators, that work with boolean values:

* `!` logical NOT (negation)
* `&&` logical AND
* `||` logical OR

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

When you use AND, the result is true only if all of the operands are true.

    true && true; //true
    true && false; //false
    false && true; //false
    false && false; //false

When using OR, the result is true if at least one of the operands is true.

    true || true; //true
    true || false; //true
    false || true; //true
    false || false; //false

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

## Statements

### Code Blocks

A block of code consists of zero or more expressions enclosed in curly brackets.

    {
      var a = 1;
      var b = 3;
    }

You can nest blocks within each other indefinitely:

    {
      var a = 1;
      var b = 3;
      var c, d;
      {
        c = a + b;
        {
          d = a - b;
        }
      }
    }

#### Best Practice Tips

* Use end-of-line semicolons.
Although the semicolon is optional when you have one expression per line, it's good to develop the habit of using them.
For best readability, the individual expressions inside a block should be placed one per line and separated by semi-colons.
* Indent any code placed within curly brackets.
Some people use one tab indentation, some use four spaces, and some use two spaces.
It really doesn't matter, as long as you're consistent.
* Use curly brackets.
When a block consists of only one expression, the curly brackets are optional,
but for readability and maintainability, you should get into the habit of always using them, even when they're optional.


### The if Statement

 The if statement has the following syntax:

    if (condition) statement1 else statement2

    if (i > 25)
      console.log("Greater than 25."); //one-line statement
    else {
      console.log("Less than or equal to 25."); //block statement
    }

It’s considered best coding practice to always use block statements,
even if only one line of code is to be executed.
Doing so can avoid confusion about what should be executed for each condition.
You can also chain if statements together like so:

    if (condition1) statement1 else if (condition2) statement2 else statement3

    if (i > 25) {
      console.log("Greater than 25.");
    } else if (i < 0) {
      console.log("Less than 0.");
    } else {
      console.log("Between 0 and 25, inclusive.");
    }

### The switch Statement

If you find yourself using an if condition and having too many else if parts, you could consider changing the if to a switch.

    switch (expression) {
      case value: statement
        break;
      case value: statement
        break;
      case value: statement
        break;
      case value: statement
        break;
      default: statement
    }

Each case in a switch statement says, "If the expression is equal to the value, execute the statement."
The break keyword causes code execution to jump out of the switch statement.
Without the break keyword, code execution falls through the original case into the following one.
The default keyword indicates what is to be done if the expression does not evaluate to one of the cases.
(In effect, it is an else statement.)

In other words, the step-by-step procedure for executing a switch statement is as follows:

1. Evaluate the switch expression found in parentheses, remember it.
2. Move to the first case, compare its value with the one from step 1.
3. If the comparison in step 2 returns true, execute the code in the case block.
4. After the case block is executed, if there's a break statement at the end of it, exit the switch.
5. If there's no break or step 2 returned false, move on to the next case block. Repeat steps 2 to 5.
6. If we're still here (we didn't exit in step 4), execute the code following the default statement.

Essentially, the switch statement prevents a developer from having to write something like this:

  if (i == 25) {
    console.log("25");
  } else if (i == 35) {
    console.log("35");
  } else if (i == 45) {
    console.log("45");
  } else {
    console.log("other");
  }

The equivalent switch statement is as follows:

  switch (i) {
    case 25:
      console.log("25");
      break;
    case 35:
      console.log(“35”);
      break;
    case 45:
      console.log("45");
      break;
    default:
      console.log("other");
  }

It’s best to always put a break statement after each case to avoid having cases fall through into the next one.
If you need a case statement to fall through, include a comment indicating that the omission of the break statement is intentional, such as this:

  switch (i) {
    case 25: // falls through
    case 35:
      console.log("25 or 35");
      break;
    case 45:
      console.log("45");
      break;
    default:
      console.log("other");
  }

Although the switch statement was borrowed from other languages, it has some unique characteristics in ECMAScript.

* the switch statement works with all data types (in many languages it works only with numbers), so it can be used with strings and even with objects.
* the case values need not be constants; they can be variables and even expressions.

The switch statement compares values using the identically equal operator, so no type coercion occurs
(for example, the string "10" is not equal to the number 10).

### The do-while Statement

The do-while statement is a post-test loop:
the escape condition is evaluated only after the code inside the loop has been executed.
The body of the loop is always executed at least once before the expression is evaluated.

    do {
      statement
    } while (expression);

for example:

    var i = 0;
    do {
      i += 2;
    } while (i < 10);

In this example, the loop continues as long as i is less than 10.
The variable starts at 0 and is incremented by two each time through the loop.

### The while Statement

The while statement is a pretest loop.
This means the escape condition is evaluated before the code inside the loop has been executed.
Because of this, it is possible that the body of the loop is never executed.

    while (expression) statement

for example:

    var i = 0;
    while (i < 10) {
      i += 2;
    }

In this example, the variable i starts out equal to 0 and is incremented by two each time through the loop.
As long as the variable is less than 10, the loop will continue.

### The for Statement

The for statement is also a pretest loop with the added capabilities of variable initialization before entering the loop and defining postloop code to be executed.

    for (initialization; expression; post-loop-expression) statement

for loops can be nested within each other.

Here's an example of a loop that is nested inside another loop and assembles a string containing 10 rows and 10 columns of asterisks.
Think of i being the row and j being the column of an "image".

    var res = '\n';
    for(var i = 0; i < 10; i++) {
      for(var j = 0; j < 10; j++) {
        res += '* ';
      }
      res += '\n';
    }

    The result is a string like:

    "
    * * * * * * * * * *
    * * * * * * * * * *
    * * * * * * * * * *
    * * * * * * * * * *
    * * * * * * * * * *
    * * * * * * * * * *
    * * * * * * * * * *
    * * * * * * * * * *
    * * * * * * * * * *
    * * * * * * * * * *
    "

The initialization, control expression, and postloop expression are all optional.
You can create an infinite loop by omitting all three, like this:

    for (;;) { //infinite loop
      doSomething();
    }

Including only the control expression effectively turns a for loop into a while loop, as shown here:

￼￼￼￼var count = 10;
    var i = 0;
    for (; i < count; ) {
      console.log(i);
      i++;
    }

This versatility makes the for statement one of the most used in the language.

### The for-in Statement

The for-in statement is a strict iterative statement.
It is used to enumerate the properties of an object.

    for (property in expression) statement

For example:

  var obj = {a: 1, b: 2, c: 3};
  for (var key in obj) {
    console.log(key);
  }

# Functions

A function is a block of JavaScript code that is defined once but may be executed, or invoked, any number of times.
Functions allow you group together some code, give this code a name, and reuse it later, addressing it by name.

    function sum (a, b) {
      var result = a + b;
      return result;
    }

JavaScript functions are parameterized: a function definition may include a list of identifiers, known as parameters, that work as local variables for the body of the function.
Function invocations provide values, or arguments, for the function’s parameters.
Functions often use their argument values to compute a return value that becomes the value of the function invocation expression.
In addition to the arguments, each invocation has another value, the invocation context, that is the value of the this keyword.

A function can only return a single value.
If you need to return more values, then simply return an array that contains all of the values as elements of this array.

If a function is assigned to the property of an object, it is known as a method of that object.
When a function is invoked on or through an object, that object is the invocation context or this value for the function.
Functions designed to initialize a newly created object are called constructors.

In JavaScript, functions are objects, and they can be manipulated by programs.
JavaScript can assign functions to variables and pass them to other functions.
Since functions are objects, you can set properties on them, and even invoke methods on them.
JavaScript function definitions can be nested within other functions,
and they have access to any variables that are in scope where they are defined.
This means that JavaScript functions are closures, and it enables important and powerful programming techniques.

## Defining functions

Function definition is composed by:

* The function statement.
* The name of the function.
* A list of zero or more parameter names grouped within parenthesis and separated by comma.
Parameters behave like local variables within the body of the function.
* A code block, also called the body of the function.
The statements in the body are executed whenever the function is invoked.
* The return statement.
A function always returns a value.
If it doesn't return value explicitly, it implicitly returns the value undefined.

For example:

    function sum (a, b) {
      return a + b;
    }

    function distance (x1, y1, x2, y2) {
      var dx = x2 - x1;
      var dy = y2 - y1;
      return Math.sqrt(dx*dx + dy*dy);
    }

    var square = function (x) {
      return x*x;
    };

## Invoking functions

In order to make use of a function, you need to call it (invoke it).
You call a function simply by using its name followed by any parameters in parentheses.

  var result = sum(1, 2);
  console.log(result); //3

## Function arguments and parameters
Function definitions do not specify an expected type for the function parameters.
Function invocations do not do any type checking on the argument values you pass.
Function invocations do not even check the number of arguments being passed.

### Optional parameters
When a function is invoked with fewer arguments than declared parameters,
the additional parameters are set to the undefined value.

  sum(1); // NaN

### Variable-Length Argument Lists: The Arguments Object

When a function is invoked with more argument values than there are parameter names,
there is no way to directly refer to the unnamed values.
The Arguments object provides a solution to this problem.
Within the body of a function, the identifier arguments refers to the Arguments object for that invocation.
The Arguments object is an array-like object that allows the argument values passed to the function to be retrieved by number, rather than by name.

  function sum (a, b) {
    var result = a + b;
    return result;
  }

  function sum_all () {
    var result = 0;
    for (var i = 0; i < arguments.length; i++) {
      result += arguments[i];
    }
    return result;
  }

  sum(1, 2, 3, 4, 5); //3
  sum_all(1, 2, 3, 4, 5); //15

  function max () {
    var max = Number.NEGATIVE_INFINITY;
    for (var i = 0; i < arguments.length; i++) {
      max = arguments[i] > max ? arguments[i] : max;
    }
    return max;
  }

  var maximum = max(1, 10, 100, 42, 3.14, 1.4142135);
  console.log(maximum); //100

## Function as values

Functions in JavaScript are actually data.
This means that the following two ways to define a function are exactly the same:

    function f () { return 1; }
    var f = function () { return 1; }

The second way of defining a function is known as function literal notation.
When you use the typeof operator on a variable that holds a function value, it returns the string "function".

    function f () { return 1; }
    typeof f; //"function"

So JavaScript functions are data, but a special kind of data with two important features:

* They contain code
* They are executable (can be invoked)

Function can be copied to a different variable and even deleted.

    var sum = function (a, b) { return a + b; }
    var add = sum;
    delete sum;
    true

Functions are not primitive values in JavaScript,
but a specialized kind of object, which means that functions can have properties.

    function add (x,y) { return x + y; }
    function sub (x,y) { return x - y; }
    function mul (x,y) { return x * y; }
    function div (x,y) { return x / y; }

    function calc (operator, x, y) {
        return operator(x, y);
    }

    // Compute the value (2+3) + (4*5)
    calc(add, calc(add, 2, 3), calc(mul, 4, 5));

    var operators = {
        add: function (x,y) { return x + y; }
      , sub: function (x,y) { return x - y; }
      , mul: function (x,y) { return x * y; }
      , div: function (x,y) { return x / y; }
      , pow: Math.pow
    };

    function calc2 (operation, x, y) {
        if (typeof operators[operation] === 'function') {
            return operators[operation](x, y);
        } else {
            throw "unknown operator";
        }
    }

    calc2('add', 'hello ', 'world');
    calc2('pow', 10, 2);

## Self-invoking functions

Functions can be called right after it was defined.

    (function () { alert('boo'); }());
    var a = function (name) { return 'hello ' + name + '!'; }('dude');
    console.log(a); //"hello dude!"

One good reason for using self-invoking anonymous functions is to have some work done without creating global variables.
A drawback, of course, is that you cannot execute the same function twice (unless you put it inside a loop or another function).
This makes the anonymous self-invoking functions best suited for one-off or initialization tasks.

## Inner (private) functions

Bearing in mind that a function is just like any other value,
there's nothing that stops you from defining a function inside another function.

    function a (param) {
      function b (input) {
          return input * 2;
      }
      return 'The result is ' + b(param);
    };

Using the function literal notation, this can also be written as:

    var a = function (param) {
      var b = function (input) {
        return input * 2;
      };
      return 'The result is ' + b(param);
    };

When you call the global function a(), it will internally call the local function b().
Since b() is local, it's not accessible outside a(), so we can say it's a private function.

    a(2); //"The result is 4"
    a(8); //"The result is 16"
    b(2); //ReferenceError: b is not defined

The benefit of using private functions are as follows:
* You keep the global namespace clean (smaller chance of naming collisions).
* Privacy—you expose only the functions you decide to the "outside world",
keeping to yourself functionality that is not meant to be consumed by the rest of the application.

## Functions that return Functions
A function can return only one value and this value could just as easily be another function.

    function a () {
      console.log('A!');
      return function () {
        console.log('B!');
      };
    }

    var f = a(); //"A!"
    f(); //"B!"
    f(); //"B!"

    a()();
    //"A!"
    //"B!"

## Function, Rewrite Thyself!

Because a function can return a function, you can use the new function to replace the old one.
A function can overwrite itself after the first call in order to avoid doing unnecessary repetitive work every time it's called.
The function can actually rewrite itself from the inside.

    function a () {
      console.log('A!');
      a = function () {
        console.log('B!');
      };
    }

    a(); //"A!"
    a(); //"B!"
    a(); //"B!"

## Lexical scope

In JavaScript, functions have lexical scope.
This means that functions create their environment (scope) when they are defined, not when they are executed.

    function f1 () { var a = 1; f2(); }
    function f2 () { return a; }
    f1(); //a is not defined

Inside the function f1() we call the function f2().
Because the local variable a is also inside f1(), one might expect that f2() will have access to a, but that's not the case.
At the time when f2() was defined (as opposed to executed), there was no a in sight.
f2(), just like f1(), only has access to its own scope and the global scope.
f1() and f2() don't share their local scopes.

## Closure

## Variable Scope

The scope of a variable is the region of the source code in which it is defined.
A global variable has global scope; it is defined everywhere in the code.
On the other hand, variables declared within a function are defined only within the body of the function.
They are local variables and have local scope.
Function parameters also count as local variables and are defined only within the body of the function.
Within the body of a function, a local variable takes precedence over a global variable with the same name.
If you declare a local variable or function parameter with the same name as a global variable, you effectively hide the global variable:

    var scope = 'global';

    function checkscope() {
      var scope = 'local';
      return scope;
    }

    console.log(scope); //"global"
    checkscope();       //"local"

Although you can get away with not using the var statement when you write code in the global scope,
you must always use var to declare local variables.

    var scope = "global";

    function checkscope2() {
      scope = "local";
      return scope;
    }

    console.log(scope); //"local"
    checkscope2();      //"local"

Function definitions can be nested.
Each function has its own local scope, so it is possible to have several nested layers of local scope.
For example:

    var scope = "global scope";

    function checkscope() {
      var scope = "local scope";

      function nested() {
        var scope = "nested scope";
        return scope;
      }

      return nested();
    }

    checkscope(); //"nested scoper"

### Function Scope and Hoisting

In some C-like programming languages, each block of code within curly braces has its own scope, and variables are not visible outside of the block in which they are declared.
This is called block scope, and JavaScript does not have it.

Instead, JavaScript uses function scope:
variables are visible within the function in which they are defined and within any functions that are nested within that function.

In the following code, the variables i, j, and k are declared in different spots,
but all have the same scope, all three are defined throughout the body of the function:

    function test (o) {
      var i = 0;                      //i is defined throughout function
      if (typeof o == 'object') {
        var j = 0;                    //j is defined everywhere, not just block
        for (var k=0; k < 10; k++) {  //k is defined everywhere, not just loop
          console.log(k);             //print numbers 0 through 9
        }
        console.log(k);               //k is still defined: prints 10
      }
      console.log(j);                 //j is defined, but may not be initialized
    }

JavaScript’s function scope means that all variables declared within a function are visible throughout the body of the function.
Curiously, this means that variables are even visible before they are declared.
This feature of JavaScript is informally known as hoisting:
JavaScript code behaves as if all variable declarations in a function (but not any associated assignments) are "hoisted" to the top of the function.

    var scope = "global";

    function f () {
      console.log(scope);  //prints "undefined", not "global"
      var scope = "local"; //variable scope initialized here, but defined everywhere in f
      console.log(scope);  //prints "local"
    }

You might think that the first line of the function would print “global”,
because the var statement declaring the local variable has not yet been executed.
Because of the rules of function scope, however, this is not what happens.
The local variable is defined throughout the body of the function,
which means the global variable by the same name is hidden throughout the function.
Although the local variable is defined throughout,
it is not actually initialized until the var statement is executed.
Thus, the function above is equivalent to the following,
in which the variable declaration is “hoisted” to the top and the variable initialization is left where it is:

    function f () {
      var scope;          // local variable is declared at the top of the function
      console.log(scope); // local variable exists here, but still has "undefined" value
      scope = 'local';    // local variable is initialized
      console.log(scope); // local variable has the value we expect
    }

In programming languages with block scope,
it is generally good programming practice to declare variables
as close as possible to where they are used and with the narrowest possible scope.

Since JavaScript does not have block scope,
some programmers make a point of declaring all their variables at the top of the function,
rather than trying to declare them closer to the point at which they are used.
This technique makes their source code accurately reflect the true scope of the variables.

