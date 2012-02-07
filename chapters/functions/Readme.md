# Functions

A function is a block of JavaScript code that is defined once but may be executed, or invoked, any number of times.  
Functions allow you group together some code, give this code a name, and reuse it later, addressing it by name.

## Defining functions

Function definition is composed by:

* the `function` statement
* the name of the function
* a list of zero or more parameter names grouped within `(` and `)`and separated by comma `,`
* a code block, the body of the function
* the `return` statement

```js
function sum (a, b) {
  var result = a + b;
  return result;
}
```

> #### Note
> A function always returns a value.  
> If it doesn't return value explicitly, it implicitly returns the value `undefined`.
> 
> A function can only return a single value.  
> If you need to return more values, then simply return an object.

```js
function distance (x1, y1, x2, y2) {
  var dx = x2 - x1;
  var dy = y2 - y1;
  return Math.sqrt(dx*dx + dy*dy);
}

var square = function (x) {
  return x*x;
};
```

In JavaScript, functions are objects:  
they can be assigned to variables and passed to other functions;  
they have properties and methods.

## Invoking functions

In order to make use of a function, you need to call it (invoke it).
You call a function simply by using its name followed by parameters list in parentheses.

```js
var result = sum(1, 2);
result; // 3
```

## Function arguments and parameters

Function definitions do not specify an expected type for the function parameters.  
Function invocations do not do any type checking on the argument values you pass.  
Function invocations do not even check the number of arguments being passed.  

### Optional parameters

When a function is invoked with fewer arguments than declared parameters,  
the additional parameters are set to `undefined`.

```js
var result = sum(1);
result; // NaN
```

### Argument lists

When a function is invoked with more argument values than declared parameters,  
there is no way to directly refer to the unnamed values.

The `arguments` object, within the body of a function, is an array-like object  
that allows the argument values passed to the function to be retrieved by number, rather than by name.

```js
function sum (a, b) {
  return a + b;
}

var result = sum(1, 2, 3, 4, 5); 
result; //3
```

```js
function sumAll () {
  var result = 0;
  for (var i = 0; i < arguments.length; i++) {
    result += arguments[i];
  }
  return result;
}

var result = sum_all(1, 2, 3, 4, 5);
result; //15
```

```js
function max () {
  var max = Number.NEGATIVE_INFINITY;
  for (var i = 0; i < arguments.length; i++) {
    max = arguments[i] > max ? arguments[i] : max;
  }
  return max;
}

maximum = max(1, 10, 100, 42, 3.14, 1.4142135);
maximum; //100
```

## Function as values

JavaScript functions are actually data:  
they can be assigned to variables or object properties.

```js
var greetings = function () { return 'hello'; };
var person = { say: greetings };
```

When you use the `typeof` operator on a variable that holds a function value, it returns `"function"`.

```js
var greetings = function () { return 'hello'; };
typeof greetings; //"function"
```

JavaScript functions are data, but a special kind of data with two important features:

* they contain code
* they are executable (can be invoked)

JavaScript functions can be copied to a different variable.

```js
var sum = function (a, b) { return a + b; }
var add = sum;
var result = add(1, 2);
result; //3
```

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

