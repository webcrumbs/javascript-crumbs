# Functions

- - -
## definition

    !js
    function name (comma_separated_params) {
      // code block 
    }

- - -
## definition

    !js
    function sum (a, b) {
      var result = a + b;
      return result;
    }

- - -
## definition

    !js
    function greets (name) {
      alert('Hello ' + name + '!');
      // implicitly return undefined;
    }

- - -
## definition

    !js
    var square = function (x) {
      return x*x;
    };

- - -

## invoking functions

    !js
    var result = square(3);
    result; // ?

- - -

# Function arguments and parameters

- - -
# optional parameters

When a function is invoked with fewer arguments than declared parameters,  
the additional parameters are set to `undefined`.


    !js
    function sum (a, b) { return a + b; }

    sum(3);        // NaN
    sum('Hello '); // "Hello undefined"

- - -
## arguments list

When a function is invoked with more argument values than declared parameters,  
you can refer to the unnamed values using the `arguments` object of the function.

    !js
    function args () {
        return arguments;
    }

    args(1, 'hello', Math.PI); //[1, "hello", 3.141592653589793]

- - -
## arguments list

    !js
    function sumAll () {
      var result = 0;
      for (var i = 0; i < arguments.length; i++) {
        result += arguments[i];
      }
      return result;
    }
    
    sum_all(1, 2, 3, 4, 5); //15

- - - 
## arguments list

    !js
    function max () {
      var max = Number.NEGATIVE_INFINITY;
      for (var i = 0; i < arguments.length; i++) {
        max = arguments[i] > max ? arguments[i] : max;
      }
      return max;
    }
    
    max(1, 10, 100, 42, Math.PI, 1.4142135); //100

- - - 
# Functions as values

- - -
## functions as values

JavaScript functions are a special kind of object with two important features:

* they contain code  
* they are executable (can be invoked)  

Because they are objects:

* they can be assigned to variables or object properties
* they can be passed to functions  
* they can have properties
* they can be returned by functions

- - - 
## assign functions to variables

JavaScript function can be assigned to variables or object properties.

    !js
    var greets = function () { return 'Hello!'; };
    var person = { say: greets };

- - -
## copy functions to variables

JavaScript functions can be copied to different variables.

    !js
    var sum = function (a, b) { return a + b; }
    var add = sum;
    var result = add(1, 2);
    result; //3

- - -
## pass functions to functions

JavaScript functions can be passed to other function.

    !js
    function add (x,y) { return x + y; }
    function sub (x,y) { return x - y; }
    function mul (x,y) { return x * y; }
    function div (x,y) { return x / y; }
    
    function calc (operator, x, y) {
      return operator(x, y);
    }
    
    // Calculate ((2+3) + (4*5))
    calc(add, calc(add, 2, 3), calc(mul, 4, 5));

- - -
## assign properties to functions

    !js
    // Compute factorials and cache results as properties of the function itself.
    function factorial (n) {
      if (!(n in factorial)) {
        factorial[n] = n * factorial(n-1); 
      }
      return factorial[n];
    }
    factorial[1] = 1; // Initialize the cache to hold this base case.

- - -
## return functions

JavaScript functions can be returned by functions.

    !js
    function greets () {
      console.log('Hello!');
      return function () {
        console.log('Bye!');
      };
    }
    

    var f = greets(); //"Hello!"
    f(); //"Bye!"
    f(); //"Bye!"
    //...
    

    greets()();
    //"Hello!"
    //"Bye!"
    

    greets()()();
    //"Hello!"
    //"Bye!"
    // TypeError: object is not a function

- - -
## self-invoking functions

JavaScript functions can be called right after they were defined.

    !js
    (function () { alert('boo'); }());
    

    var message = (function (name) { return 'Hello ' + name + '!'; }('dude'));
    message; //"Hello dude!"

- - -
# Inner (private) functions

- - -
## define functions inside functions

JavaScript functions can be defined inside another function.

    !js
    function f1 (a) {
      function f2 (b) {
        return b * 2;
      }
      return f2(a);
    };
    var result = f1(2); 
    result; //4
    
## Note
When you call the global function `f1`, it will internally call the local function `f2`.  
Since `f2` is local, it's not accessible outside `f1`, so we can say it's a private function.
    
    !js
    f1(2);
    f2(2); //ReferenceError: f2 is not defined

- - -
## rewrite functions from inside

JavaScript functions can actually rewrite themselves from the inside.

    !js
    function greets () {
      console.log('Hello!');
      greets = function () {
        console.log('Bye!');
      };
    }
    

    greets()();
    //"Hello!"
    //"Bye!"
    
    
    greets()()();
    //"Hello!"
    //"Bye!"
    //"Bye!"
