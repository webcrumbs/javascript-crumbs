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
> 
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
> 
> sum(3);       // NaN
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
> 
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
> 
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
> 
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
> var greets = function () { return 'Hello!'; };
> var person = { say: greets };
> ```

JavaScript functions can be copied to different variables.

> #### Example
> ```js
> var sum = function (a, b) { return a + b; }
> var add = sum;
> var result = add(1, 2);
> result; //3
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
> 
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
> var result = f1(2); 
> result; //4
> ```
> 
> #### Note
> When you call the global function `f1`, it will internally call the local function `f2`.  
> Since `f2` is local, it's not accessible outside `f1`, so we can say it's a private function.
> 
> ```js
> f1(2);
> f2(2); //ReferenceError: f2 is not defined
> ```

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
>   };
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

## Lexical scope

JavaScript functions have **lexical scope**:  
they create their environment (scope) when they are defined, not when they are executed.

> #### Example
> ```js
> function f1 () { 
>   var a = 1; 
>   f2(); 
> }
> 
> function f2 () { 
>   return a; 
> }
> 
> f1(); //a is not defined
> ```

## Function Scope

JavaScript uses **function scope**:
variables are visible within the function in which they are defined  
and within any functions that are nested within that function.

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

Each function has its own local scope.  
Since functions can be nested, it is possible to have several nested layers of local scope.

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
>
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
