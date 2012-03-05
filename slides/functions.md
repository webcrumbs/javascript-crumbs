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

#### Example

```js
function sum (a, b) {
  var result = a + b;
  return result;
}
```

- - -

# Functions

## Definition

#### Example

```js
function greets (name) {
  alert('Hello ' + name + '!');
  // implicitly return undefined;
}
```

- - -

# Functions

## Definition

#### Example

```js
var square = function (x) {
  return x*x;
};
```

- - -

# Functions

## Invoking functions

```js
var result = square(3);
result; // ?
```

- - -

# Functions

## Function arguments and parameters

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

- - -

# Functions

## Function arguments and parameters

### Arguments list

When a function is invoked with more argument values than declared parameters,  
you can refer to the unnamed values using the `arguments` object of the function.

> #### Example
> ```js
> function args () {
>   return arguments;
> }
> 
> args(1, 'hello', Math.PI); //[1, "hello", 3.141592653589793]
> ```

- - -

# Functions

## Function arguments and parameters

### Arguments list

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

- - - 

# Functions

## Function arguments and parameters

### Arguments list

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

- - - 

# Functions

## Function as values

JavaScript functions are a special kind of object with two important features:

* they contain code  
* they are executable (can be invoked)  

Because they are objects:

* they can be assigned to variables or object properties
* they can be passed to functions  
* they can have properties
* they can be returned by functions

- - - 

# Functions

## Function as values

### Assign function to variables

JavaScript function can be assigned to variables or object properties.

> #### Example
> ```js
> var greets = function () { return 'Hello!'; };
> var person = { say: greets };
> ```

- - -

# Functions

## Function as values

### Copy function to variables

JavaScript functions can be copied to different variables.

> #### Example
> ```js
> var sum = function (a, b) { return a + b; }
> var add = sum;
> var result = add(1, 2);
> result; //3
> ```

- - -

# Functions

## Function as values

### Pass function to functions

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

- - -

# Functions

## Function as values

### Assign properties to functions

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

- - -

# Functions

## Function as values

### Return function

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

- - -

# Functions

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

- - -

# Functions

## Inner (private) functions

### Define functions inside functions

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

- - -

# Functions

## Inner (private) functions

### Rewrite functions from inside

JavaScript functions can actually rewrite themselves from the inside.

> #### Example 
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


