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

### Arguments list

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

In JavaScript, functions are objects:  

* they can be assigned to variables  
* they can be passed to other functions  
* they have properties

but a special kind of object with two important features:

* they contain code  
* they are executable (can be invoked)  

> #### Note
> although functions are considered objects and don’t represent another data type
> they do have some special properties, which differentiate them from other objects:
> operator typeof applied to a function returns "function" not "object"
> 
> ```js
> typeof function () {}; //"function"
> ```

JavaScript function can be assigned to variable or object properties.

```js
var greetings = function () { return 'hello'; };
var person = { say: greetings };
```

JavaScript functions can be copied to a different variable.

```js
var sum = function (a, b) { return a + b; }
var add = sum;
var result = add(1, 2);
result; //3
```

JavaScript functions can have properties.

```js
function add (x,y) { return x + y; }
function sub (x,y) { return x - y; }
function mul (x,y) { return x * y; }
function div (x,y) { return x / y; }

function calc (operator, x, y) {
  return operator(x, y);
}

// Calculate ((2+3) + (4*5))
calc(add, calc(add, 2, 3), calc(mul, 4, 5));
```

```js
var operators = {
    add: function (x,y) { return x + y; }
  , sub: function (x,y) { return x - y; }
  , mul: function (x,y) { return x * y; }
  , div: function (x,y) { return x / y; }
  , pow: Math.pow
};

function calc (operation, x, y) {
  if (typeof operators[operation] === 'function') {
    return operators[operation](x, y);
  } else {
    throw "unknown operator";
  }
}

calc('add', 'hello ', 'world'); //"hello world"
calc('pow', 10, 2); //100
```

## Self-invoking functions

JavaScript functions can be called right after it was defined.

```js
(function () { alert('boo'); }());
var message = function (name) { return 'hello ' + name + '!'; }('dude');
message; //"hello dude!"
```

> #### Note 
> You cannot execute the same anonimous function twice (unless you put it inside a loop or another function).

> #### Tip
> Use self-invoking anonymous functions to have some work done without creating global variables,  
> for one-off or initialization tasks.

## Inner (private) functions

JavaScript functions can be defined inside another function.

```js
function a (param) {
  function b (input) {
    return input * 2;
  }
  return b(param);
};
var result = a(2); 
result; //4
```

```js
var a = function (param) {
  var b = function (input) {
    return input * 2;
  };
  return b(param);
};
var result = a(2); 
result; //4
```

> ####Note
> When you call the global function `a`, it will internally call the local function `b`.  
> Since `b` is local, it's not accessible outside `a`, so we can say it's a private function.
> 
> ```js
> a(2);
> b(2); //ReferenceError: b is not defined
> ```

The benefit of using private functions are as follows:
* you keep the global namespace clean (smaller chance of naming collisions)
* you expose only the functions you decide to the "outside world"

## Functions that return functions

A function can return only one value and this value could just as easily be another function.

```js
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
```

Because a function can return a function, you can use the new function to replace the old one.  
The function can actually rewrite itself from the inside.

```js
function a () {
  console.log('A!');
  a = function () {
    console.log('B!');
  };
}

a(); //"A!"
a(); //"B!"
a(); //"B!"
```

## Lexical scope

In JavaScript, functions have **lexical scope**:
functions create their environment (scope) when they are defined, not when they are executed.

```js
function f1 () { 
  var a = 1; 
  f2(); 
}
    
function f2 () { 
  return a; 
}
    
f1(); //a is not defined
```

## Closure

## Variable Scope
The scope of a variable is the region of the source code in which it is defined.

In some C-like programming languages, each block of code within curly braces has its own scope, 
and variables are not visible outside of the block in which they are declared.
This is called block scope, and JavaScript does not have it.

JavaScript uses **function scope**:
variables are visible within the function in which they are defined  
and within any functions that are nested within that function;  
a global variable has global scope, it is defined everywhere in the code;  
a variable declared within a function has a local scope, it is defined only within the body of the function.

Function parameters count as local variables and are defined only within the body of the function.  
A local variable, declared within a function, takes precedence over a global variable with the same name.

```js
var scope = 'global';

function checkscope () {
  var scope = 'local';
  return scope;
}

checkscope(); //"local"
scope;        //"global"
```

Although you can get away with not using the var statement when you write code in the global scope,  
you must always use var to declare local variables.

```js
var scope = 'global';

function checkscope () {
  scope = 'local';
  return scope;
}

checkscope(); //"local"
scope;        //"local"
```

Each function has its own local scope.  
Since functions can be nested, it is possible to have several nested layers of local scope.

```js
var scope = 'global';

function checkscope () {
  var scope = 'local';

  function nested () {
    var scope = 'nested';
    return scope;
  }

  return nested();
}

checkscope(); //"nested"
scope;        //"global"
```

### Hoisting

JavaScript’s function scope means that all variables declared within a function are visible throughout the body of the function.
Curiously, this means that variables are even visible before they are declared.  
This feature of JavaScript is informally known as **hoisting**:
JavaScript code behaves as if all variable declarations in a function  
(but not any associated assignments) are "hoisted" to the top of the function.

```js
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
```

> #### Note
> The variables `i`, `j`, and `k` are declared in different spots,  
> but all have the same scope, all three are defined throughout the body of the function.

```js
var scope = "global";

function f () {
  console.log(scope);  //prints "undefined", not "local" nor "global"
  var scope = "local"; //variable scope initialized here, but defined everywhere in f
  console.log(scope);  //prints "local"
}
```

> #### Note
> You might think that the first line of the function would print “global”,  
> because the var statement declaring the local variable has not yet been executed.  
> Because of the rules of function scope, however, this is not what happens.  
> The local variable is defined throughout the body of the function,  
> which means the global variable by the same name is hidden throughout the function.  
> Although the local variable is defined throughout,  
> it is not actually initialized until the var statement is executed.

The function above is equivalent to the following,  
in which the variable declaration is “hoisted” to the top  
and the variable initialization is left where it is:

```js
function f () {
  var scope;          // local variable is declared at the top of the function
  console.log(scope); // local variable exists here, but still has "undefined" value
  scope = 'local';    // local variable is initialized
  console.log(scope); // local variable has the value we expect
}
```

> ### Tip
> In programming languages with block scope,
> it is generally good programming practice to declare variables
> as close as possible to where they are used and with the narrowest possible scope.
> Since JavaScript does not have block scope,
> some programmers make a point of declaring all their variables at the top of the function,
> rather than trying to declare them closer to the point at which they are used.
> This technique makes their source code accurately reflect the true scope of the variables.
