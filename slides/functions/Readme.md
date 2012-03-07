# Functions

- - -

# Functions

## Definition

```js
function name (comma_separated_params) {
  // code block 
}
```

- - -

# Functions

## Definition

```js
function sum (a, b) {
  var result = a + b;
  return result;
}
```

- - -

# Functions

## Definition

```js
function greets (name) {
  alert('Hello ' + name + '!');
  // implicitly return undefined;
}
```

```js
var square = function (x) {
  return x*x;
};
```

- - -

# Functions

## Invocation

```js
var result = square(3);
result; // ?
```

- - -

# Functions

## Invocation

### Arguments and parameters

#### Optional parameters

If arguments are fewer than declared parameters  
the additional parameters are set to `undefined`

```js
function sum (a, b) { return a + b; }

sum(3);       // NaN
sum('Hello '); // "Hello undefined"
```

- - -

# Functions

## Invocation

### Arguments and parameters

#### Arguments list

If arguments are more than declared parameters  
you can access them by the `arguments` object

```js
function args () {
  return arguments;
}

args(1, 'hello', Math.PI); //[1, "hello", 3.141592653589793]
```

- - -

# Functions

## Invocation

### Arguments list

```js
function sumAll () {
  var result = 0;
  for (var i = 0; i < arguments.length; i++) {
    result += arguments[i];
  }
  return result;
}
```
```js
sumAll(1, 2, 3, 4, 5); //15
```

- - - 

# Functions

## Invocation

### Arguments list

```js
function max () {
  var max = Number.NEGATIVE_INFINITY;
  for (var i = 0; i < arguments.length; i++) {
    max = arguments[i] max ? arguments[i] : max;
  }
  return max;
}
```
```js
max(1, 10, 100, 42, Math.PI, 1.4142135); //100
```

- - - 

# Functions

## Function as values

### Functions are objects

JavaScript functions are a special kind of object with two important features:

* they contain code  
* they are executable (can be invoked)  

and because they are objects:

* they can be assigned to variables or object properties
* they can be passed to functions  
* they can have properties
* they can be returned by functions

- - - 

# Functions

## Function as values

### Assign function to variables

JavaScript function can be assigned to variables or object properties.

```js
function f () { return 'Hello!'; };
var greets = f;
var person = { say: greets };
```

- - -

# Functions

## Function as values

### Copy function to variables

JavaScript functions can be copied to different variables.

```js
var sum = function (a, b) { return a + b; }
var add = sum;
```
```js
var result = add(1, 2);
result; //3
```

- - -

# Functions

## Function as values

### Pass function to functions

JavaScript functions can be passed to other function.

```js
function add (x,y) { return x + y; }
function sub (x,y) { return x - y; }
function mul (x,y) { return x * y; }
function div (x,y) { return x / y; }

function calc (operator, x, y) {
  return operator(x, y);
}
```
```js
// Calculate ((2+3) + (4*5))
calc(add, calc(add, 2, 3), calc(mul, 4, 5));
```

- - -

# Functions

## Function as values

### Assign properties to functions

```js
// Compute factorials and cache results as properties of the function itself.
function factorial (n) {
  if (!(n in factorial)) {
    factorial[n] = n * factorial(n-1); 
  }
  return factorial[n];
}

factorial[1] = 1; // Initialize the cache to hold this base case.
```
```js
factorial(5); //120
```

- - -

# Functions

## Function as values

### Return function

JavaScript functions can be returned by functions.

```js
function greets () {
  console.log('Hello!');
  return function () {
    console.log('Bye!');
  };
}
```

```js
var f = greets(); //"Hello!"
f(); //"Bye!"
f(); //"Bye!"
//...
```

- - -

# Functions

## Function as values

### Return function

JavaScript functions can be returned by functions.

```js
function greets () {
  console.log('Hello!');
  return function () {
    console.log('Bye!');
  };
}
```

```js 
greets()();
//"Hello!"
//"Bye!"
```

```js
greets()()();
//"Hello!"
//"Bye!"
// TypeError: object is not a function
```

- - -

# Functions

## Self-invoking functions

JavaScript functions can be called right after they were defined.

```js
(function () { alert('boo'); }());
```

```js
var message = (function (name) { return 'Hello ' + name + '!'; }('dude'));
message; //"Hello dude!"
```

- - -

# Function

## Inner (private) functions

### Define functions inside functions

JavaScript functions can be defined inside another function.

```js
function f1 (a) {
  function f2 (b) {
    return b * 2;
  }
  return f2(a);
};
```
```js
f1(2); //4
```
```js
f2(2); //ReferenceError: f2 is not defined
```

#### Note
`f2` is defined inside `f1` and it is not visible outside `f1`;
`f1` internally call the local function `f2`.

- - -

# Function
## Inner (private) functions

```js
function greets () {
  console.log('Hello!');
  greets = function () {
    console.log('Bye!');
    return greets;
  };
  return greets;
}
```

```js 
greets()();
//"Hello!"
//"Bye!"
```

```js
greets()()();
//"Hello!"
//"Bye!"
//"Bye!"
```

- - -

# Function

## Function Scope

JavaScript uses **function scope**:  
variables are visible within the function in which they are defined  
and within any functions that are nested within that function.

A variable defined in a function is not visible outside the function, 
but a variable defined in a code block is visible outside the block.

- - - 

# Function

### Function Scope

```js
var a = 1; 
function f () { var b = 1; return a; }
```
```js
f();
```
```js
b; //b is not defined
```

- variable `a` is in the global space  
- variable `b` is in the scope of the function `f()`  
- inside `f()`, both `a` and `b` are visible  
- outside `f()`, `a` is visible, but `b` is not

- - - 

# Function

## Function Scope

### Local and Global Scope

A variable declared within a function has a **local scope**,  
it is defined only within the body of the function.  

A variable not declared within a function has a **global scope**,  
it is defined everywhere in the code.

A local variable, a variable declared within a function,  
takes precedence over a global variable with the same name.

- - -

# Function

## Function Scope

### Local and Global Scope

```js
var scope = 'global';

function checkScope () {
  var scope = 'local';
  return scope;
}

checkScope(); //"local"
scope;        //"global"
```

- - - 

# Function

## Function Scope

### Local and Global Scope

#### Attention!
You must always use `var` to declare local variables.

```js
var scope = 'global';

function checkScope () {
  scope = 'local';        // if var is omitted, it refers to global variable
  return scope;
}

checkScope(); //"local"
scope;        //"local"
```

- - - 

# Function

## Function Scope

### Local variables

Function parameters count as local variables  
and are defined only within the body of the function.

```js
function checkParamScope (a) {
  a += 1;
  console.log(a);
}

console.log(a);     //"undefined"
checkParamScope(1); //2
```

- - - 

# Function

## Function Scope

### Scope Chain

Each function has its own local scope.  
It is possible to have several nested layers of local scope.

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

- - -

# Function

## Function Scope

### Scope Chain

```js
var scope = 'global';

function localScope () {
  var scope = 'local';

  function nestedScope () {
    var scope = 'nested';
    return scope;
  }

  return nestedScope();
}
```
```js
localScope(); //"nested"
scope;        //"global"
```

- - - 

# Function

## Function Scope

### Variable hoisting

Since variables are visible within the function in which they are defined  
variables are even visible before they are declared.  
All variable declarations in a function (but not any associated assignments)  
are "hoisted" to the top of the function.

- - -

### Variable hoisting

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

The variables `i`, `j`, and `k` are declared in different spots,  
but all have the same scope, all three are defined throughout the body of the function.

- - -

# Function

## Function Scope

### Variable hoisting

```js
var scope = 'global';

function f () {
  console.log(scope);  //prints "undefined", not "local" nor "global"
  var scope = 'local'; //variable scope initialized here, but defined everywhere in f
  console.log(scope);  //prints "local"
}
```

The function above is equivalent to the following:

```js
function f () {
  var scope;          // local variable is declared at the top of the function
  console.log(scope); // local variable exists here, but still has "undefined" value
  scope = 'local';    // local variable is initialized
  console.log(scope); // local variable has the value we expect
}
```

- - -

# Function

## Function Scope

### Variable hoisting

#### Tip
Declare all the variables defined within a function at the top of the function.

- - - 

# Function

## Closures

### Example \#0

```js
function f () {
  var b = 'b';
}
```

```js
b; //b is not defined
```

- - -

# Function

## Closure

### Example \#1

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

- - -

# Function

## Closure

### Example \#2

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

- - -

# Function

## Closure

### Example \#3

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

- - -

# Function

## Closure

### Example \#4

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

- - -

# Function

## Closure

### Example \#5

```js
function countdown (from) {
  return function () {
    if (from 0) {
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

- - -

# Function

## Closure

### Example \#6

Let's loop three times, each time creating a new function that returns the loop sequence number.  
The new functions will be added to an array and we'll return the array at the end. 

- - -

# Function

## Closure

### Example \#6

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

- - -

# Function

## Closure

### Example \#6 (that works!)

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

- - - 

# Function

## Closure

### Example \#7

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

