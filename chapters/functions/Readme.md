# Functions

A function is a block of JavaScript code that is defined once but may be executed, or invoked, any number of times.  
Functions allow you group together some code, give this code a name, and reuse it later, addressing it by name.

## Defining functions

```js
function function_name (comma_separated_parameters) {
  // code block
  return returned_value;
}
```

Function definition is composed by:

* the `function` statement
* the name of the function
* a list of zero or more parameter names grouped within `(` and `)`and separated by comma `,`
* a code block, the body of the function
* the `return` statement

> #### Example
> 
> ```js
> function sum (a, b) {
>   var result = a + b;
>   return result;
> }
> ```
> 
> ```js
> var square = function (x) {
>   return x * x;
> };
> ```

> #### Note
> A function always returns a value.  
> If it doesn't return value explicitly, it implicitly returns the value `undefined`.
> 
> ```js
> function greets (name) {
>   console.log('Hello ' + name + '!');
> } // implicitly return undefined
> ```
> 
> #### Note
> A function can only return a single value.  
> If you need to return more values, then simply return an object.

## Invoking functions

In order to make use of a function, you need to call it (invoke it).  
You call a function simply by using its name followed by parameters list in parentheses.

```js
function_name(comma_separated_arguments);
```

> #### Example
> ```js
> function sum (a, b) { return a + b; }
> ```
> ```js
> sum(3, 2); // 5
> ```

## Function arguments and parameters

Function definitions do not specify an expected type for the function parameters.  
Function invocations do not do any type checking on the argument values you pass.  
Function invocations do not even check the number of arguments being passed.  

### Optional parameters

When a function is invoked with fewer arguments than declared parameters,  
the additional parameters are set to `undefined`.

> #### Example
> ```js
> function sum (a, b) { return a + b; }
> ```
> ```js
> sum(3);        // NaN
> ```
> ```js
> sum('Hello '); // "Hello undefined"
> ```

### Arguments list

When a function is invoked with more argument values than declared parameters,  
there is no way to directly refer to the unnamed values.

The `arguments` object, defined within the body of a function, is an array-like object  
that allows the argument values passed to the function to be retrieved by number:  
the first argument value is in `arguments[0]`, the second in `arguments[1]`, ...

> #### Example
> ```js
> function args () {
>   return arguments;
> }
> ```
> ```js
> args(1, 'hello', Math.PI); //[1, "hello", 3.141592653589793]
> ```
> 
> #### Example
> ```js
> function sumAll () {
>   var result = 0;
>   for (var i = 0; i < arguments.length; i++) {
>     result += arguments[i];
>   }
>   return result;
> }
> ```
> ```js
> sum_all(1, 2, 3, 4, 5); //15
> ```
> 
> #### Example
> 
> ```js
> function max () {
>   var max = Number.NEGATIVE_INFINITY;
>   for (var i = 0; i < arguments.length; i++) {
>     max = arguments[i] > max ? arguments[i] : max;
>   }
>   return max;
> }
> ```
> ```js
> max(1, 10, 100, 42, Math.PI, 1.4142135); //100
> ```

## Function as values

JavaScript functions are a special kind of object with two important features:

* they contain code  
* they are executable (can be invoked)  

Because they are objects:

* they can be assigned to variables or object properties
* they can be passed to functions  
* they can have properties
* they can be returned by functions

> #### Note
> although functions are considered objects and don’t represent another data type  
> they do have some special properties, which differentiate them from other objects:  
> operator `typeof` applied to a function returns `"function"` not `"object"`
> 
> ```js
> typeof function () {}; //"function"
> ```

JavaScript function can be assigned to variables or object properties.

> #### Example
> ```js
> function f () { return 'Hello!'; }
> ```
> ```js
> var greets = f;
> var person = { say: greets };
> ```

JavaScript functions can be copied to different variables.

> #### Example
> ```js
> var sum = function (a, b) { return a + b; }
> var add = sum;
> ```
> ```js
> add(1, 2); //3
> ```

JavaScript functions can be passed to other function.

> #### Example
> ```js
> function add (x,y) { return x + y; }
> function sub (x,y) { return x - y; }
> function mul (x,y) { return x * y; }
> function div (x,y) { return x / y; }
> 
> function calc (operator, x, y) {
>   return operator(x, y);
> }
> ```
> ```js
> // Calculate ((2+3) + (4*5))
> calc(add, calc(add, 2, 3), calc(mul, 4, 5));
> ```

JavaScript functions can have properties.

> #### Example
> ```js
> guid.counter = 0;
>
> // This function returns a different integer each time it is called.
> // It uses a property of itself to remember the next value to be returned.
> function guid() {
>   return guid.counter++; // Increment and return counter property 
> }
> ```

> #### Example
> ```js
> // Compute factorials and cache results as properties of the function itself.
> function factorial (n) {
>   if (!(n in factorial)) {
>     factorial[n] = n * factorial(n-1); 
>   }
>   return factorial[n];
> }
> factorial[1] = 1; // Initialize the cache to hold this base case.
> ```

JavaScript functions can be returned by functions.

> #### Example
> ```js
> function greets () {
>   console.log('Hello!');
>   return function () {
>     console.log('Bye!');
>   };
> }
> ```
>
> ```js
> var f = greets(); //"Hello!"
> f(); //"Bye!"
> f(); //"Bye!"
> //...
> ```
>
> ```js 
> greets()();
> //"Hello!"
> //"Bye!"
> ```
>
> ```js
> greets()()();
> //"Hello!"
> //"Bye!"
> // TypeError: object is not a function
> ```

## Self-invoking functions

JavaScript functions can be called right after they were defined.

> #### Example
> ```js
> (function () { alert('boo'); }());
> ```

> #### Example
> ```js
> var message = (function (name) { return 'Hello ' + name + '!'; }('dude'));
> message; //"Hello dude!"
> ```

> #### Tip
> Use self-invoking anonymous functions to have some work done,  
> without creating global variables, for initialization tasks.

## Inner (private) functions

JavaScript functions can be defined inside another function.

> #### Example
> ```js
> function f1 (a) {
>   function f2 (b) {
>     return b * 2;
>   }
>   return f2(a);
> };
> ```
> 
> ```js
> f1(2); //4
> ```
> 
> ```js
> f2(2); //ReferenceError: f2 is not defined
> ```
>
> #### Note
> When you call the global function `f1`, it will internally call the local function `f2`.  
> Since `f2` is local, it's not accessible outside `f1`, so we can say it's a private function. 

The benefit of using private functions are as follows:

* you keep the global namespace clean (smaller chance of naming collisions)
* you expose only the functions you decide to the "outside world"

> #### Note
> JavaScript functions can actually rewrite themselves from the inside.
> 
> ```js
> function greets () {
>   console.log('Hello!');
>   greets = function () {
>     console.log('Bye!');
>     return greets;
>   };
>   return greets;
> }
> ```
>
> ```js 
> greets()();
> //"Hello!"
> //"Bye!"
> ```
>
> ```js
> greets()()();
> //"Hello!"
> //"Bye!"
> //"Bye!"
> ```

## Function Scope

JavaScript uses **function scope**:
variables are visible within the function in which they are defined  
and within any functions that are nested within that function.

A variable defined in a function is not visible outside the function, 
but a variable defined in a code block (an if or a for loop) is visible outside the block.

> #### Example
> ```js
> var a = 1; 
> function f () { var b = 1; return a; }
> ```
> ```js
> f();
> ```
> ```js
> b; //b is not defined
> ```
> #### Note 
> - variable `a` is in the global space  
> - variable `b` is in the scope of the function `f()`  
> - inside `f()`, both `a` and `b` are visible  
> - outside `f()`, `a` is visible, but `b` is not

### Local and global scope
A variable declared within a function has a **local scope**,  
it is defined only within the body of the function.  

A variable not declared within a function has a **global scope**,  
it is defined everywhere in the code.

A local variable, a variable declared within a function,  
takes precedence over a global variable with the same name.

> #### Example
> ```js
> var scope = 'global';
> 
> function checkScope () {
>   var scope = 'local';
>   return scope;
> }
> 
> checkScope(); //"local"
> scope;        //"global"
> ```

> #### Attention!
> You must always use `var` to declare local variables.
>
> ```js
> var scope = 'global';
> 
> function checkScope () {
>   scope = 'local';        // if var is omitted, it refers to global variable
>   return scope;
> }
> 
> checkScope(); //"local"
> scope;        //"local"
> ```

### Local variables
Function parameters count as local variables and are defined only within the body of the function.

> #### Example
> ```js
> function checkParamScope (a) {
>   a += 1;
>   console.log(a);
> }
> 
> console.log(a);     //"undefined"
> checkParamScope(1); //2
> ```

### Scope chain
Each function has its own local scope.  
Since functions can be nested, it is possible to have several nested layers of local scope.

If you define a function `n()` nested inside a function `f()`, 
the function `n()` will have access to variables in its own scope, plus the scope of its "parents".  
This is known as **scope chain**, and the chain can be as long (deep) as you need it to be.

```js
var a = 1;
// code here can see variable a and function f

function f (){
  var b = 1;
  // code here can see variables a and b and function n

  function n () {
    var c = 3; 
    // code here can see variables a, b and c
  }
}
```

> #### Example
> ```js
> var scope = 'global';
> 
> function localScope () {
>   var scope = 'local';
> 
>   function nestedScope () {
>     var scope = 'nested';
>     return scope;
>   }
> 
>   return nestedScope();
> }
> ```
> ```js
> localScope(); //"nested"
> scope;        //"global"
> ```

### Variable hoisting

Since variables are visible within the function in which they are defined  
variables are even visible before they are declared.  
All variable declarations in a function (but not any associated assignments)  
are "hoisted" to the top of the function.

> #### Example
> ```js
> function test (o) {
>   var i = 0;                      //i is defined throughout function
>   if (typeof o == 'object') {
>     var j = 0;                    //j is defined everywhere, not just block
>     for (var k=0; k < 10; k++) {  //k is defined everywhere, not just loop
>       console.log(k);             //print numbers 0 through 9
>     }
>     console.log(k);               //k is still defined: prints 10
>   }
>   console.log(j);                 //j is defined, but may not be initialized
> }
> ```
> 
> #### Note
> The variables `i`, `j`, and `k` are declared in different spots,  
> but all have the same scope, all three are defined throughout the body of the function.
> 

> #### Example
> ```js
> var scope = 'global';
> 
> function f () {
>   console.log(scope);  //prints "undefined", not "local" nor "global"
>   var scope = 'local'; //variable scope initialized here, but defined everywhere in f
>   console.log(scope);  //prints "local"
> }
> ```
> 
> #### Note
> The function above is equivalent to the following,  
> in which the variable declaration is “hoisted” to the top  
> and the variable initialization is left where it is:
> 
> ```js
> function f () {
>   var scope;          // local variable is declared at the top of the function
>   console.log(scope); // local variable exists here, but still has "undefined" value
>   scope = 'local';    // local variable is initialized
>   console.log(scope); // local variable has the value we expect
> }
> ```
> 
> ### Tip
> Declare all the variables defined within a function at the top of the function,  
> rather than trying to declare them closer to the point at which they are used,  
> to make the source code accurately reflect the true scope of the variables,  
> and to avoid inaspectated results.

## Closures

#### Example
```js
function f () {
  var b = 'b';
}
```
```js
b; //b is not defined
```

#### Example \#1
```js
function f () {
  var b = 'b';
  return b;
}
```
```js
b; //b is not defined
```
```js
b = f();
b; //"b"
```

#### Example \#2
```js
function f () {
  var b = 'b';
  return function () {
    return b;
  };
}
```
```js
getB = f();
b = getB();
b; //"b"
```

#### Example \#3
```js
var getB;
function f () {
  var b = 'b';
  getB = function () {
    return b;
  };
}
```
```js
b = getB();
b; //"b"
```

#### Example \#4
```js
function f (arg) {
  return function () {
    return arg;
  };
}
```
```js
var getArg = f('Hello');
getArg(); //"Hello"
```

#### Example \#5
```js
function countdown (from) {
  return function () {
    if (from > 0) {
      return from--;
    } 
    return 'Finish!';
  };
}
```
```js
var c = countdown(3);
c(); //3
c(); //2
c(); //1
c(); //"Finish!"
c(); //"Finish!"
```

#### Example \#6
Let's loop three times, each time creating a new function that returns the loop sequence number.  
The new functions will be added to an array and we'll return the array at the end. 

```js
function f () {
  var a = [];
  var i;
  
  for (i = 0; i < 3; i++) {
    a[i] = function () {
      return i;
    }
  }

  return a; 
}
```
```js
var a = f();
```
```js
a[0](); //3
a[1](); //3
a[2](); //3
```

```js
function f () {
  function getArg (x) {
    return function () {
      return x;
    } 
  }
  
  var a = [];
  var i;
  
  for (i = 0; i < 3; i++) {
   a[i] = getArg(i);
  }
  
  return a; 
}
```

#### Example \#7

```js
var getValue, setValue;
(function () {
  var secret = 0;
  getValue = function () {
    return secret;
  };
  setValue = function (v) {
    secret = v;
  }; 
})();
```
```js
getValue();    //0
```
```js
setValue(123);
getValue();    //123
```

