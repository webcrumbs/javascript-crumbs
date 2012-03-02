## Statements

#### Code Blocks
consists of zero or more expressions enclosed in curly brackets `{` and `}`;  
they can be nested within each other indefinitely.

> #### Example
> ```js
> {
>   var a = 1;
>   var b = 3;
>   var c, d;
>   {
>     c = a + b;
>     {
>       d = a - b;
>     }
>   }
> }
> ```

> #### Convention
> * Use end-of-line semicolons, although it is optional when you have one expression per line
> * Indent any code placed within curly brackets
> * Use curly brackets, although they are optional when you have a block of only one expression

### The if Statement

```js
if (condition) statement1 else statement2
```
```js
if (condition1) statement1 else if (condition2) statement2 else statement3
```

> #### Convention 
> Use code blocks for control statements, even when it is only one expression.
>
> ```js
> if (test)
>   console.log('hello!'); //valid, but error-prone and should be avoided
> 
> if (test) { //preferred
>   alert(test);
> }
> ```

### The switch Statement

```js
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
```

The step-by-step procedure for executing a **switch** statement is as follows:

1. evaluate the switch `expression` found in parentheses, remember it
2. move to the first case, compare its value with the one from step **1**
3. if the comparison in step **2** returns `true`, execute the code in the `case` block
4. after the `case` block is executed, if there's a `break` statement at the end of it, exit the `switch`
5. if there's no `break` or step **2** returned `false`,  
move on to the next `case` block, repeat steps **2** to **5**
6. if we're still here (we didn't exit in step **4**), execute the code following the `default` statement.

> #### Note
>
> * the `switch` statement works with all data types (in many languages it works only with numbers),  
> so it can be used with strings and even with objects
> * the `case` values need not be constants, they can be variables and even expressions
> * the comparison of value is done using the identically equal operator, so no type coercion occurs


> #### Note 
> The `switch` statement prevents writing something like this:
> 
> ```js
> if (i == 25) {
>   console.log("25");
> } else if (i == 35) {
>   console.log("35");
> } else if (i == 45) {
>   console.log("45");
> } else {
>   console.log("other");
> }
> ```
> 
> The equivalent switch statement is as follows:
> 
> ```js
> switch (i) {
>   case 25:
>     console.log("25");
>     break;
>   case 35:
>     console.log("35");
>     break;
>   case 45:
>     console.log("45");
>     break;
>   default:
>     console.log("other");
> }
> ```

> #### Tip
> Put a break statement after each case to avoid having cases fall through into the next one;  
> if you need a case statement to fall through, include a comment indicating the intentional omission.
>
> ```js
> switch (i) {
>   case 25: // falls through
>   case 35:
>     console.log("25 or 35");
>     break;
>   case 45:
>     console.log("45");
>     break;
>   default:
>     console.log("other");
> }
> ```

### The do-while Statement

The do-while statement is a post-test loop:  
the escape condition is evaluated only after the code inside the loop has been executed;  
the body of the loop is always executed at least once before the expression is evaluated.

```js
do {
  statement
} while (expression);
```

> #### example
> 
> ```js
> var i = 0;
> do {
>   i += 1;
> } while (i < 10);
> 
> console.log(i); //10
> ```

### The while Statement

The while statement is a pre-test loop:  
the escape condition is evaluated before the code inside the loop has been executed;  
it is possible that the body of the loop is never executed.

```js
while (expression) statement
```

> #### Example
> 
> ```js
> var i = 0;
> while (i < 10) {
>   i += 2;
> }
> ```

### The for Statement

The for statement is a pre-test loop with code before entering the loop and post-loop code.

```js
for (initialization; expression; post-loop-expression) statement
```

> #### Note
> The for loops can be nested within each other.
> 
> ```js
> var s = '\n';
> var n = 3;
> var m = 3;
> 
> for (var i = 0; i < n; i++) {
>   for (var j = 0; j < m; j++) {
>     s += '* ';
>   }
>   s += '\n';
> }
>
> console.log(s);
> "
> * * *
> * * *
> * * *
> "
> ```

> ####Note
> The initialization, control expression, and postloop expression are all optional.  
> You can create an infinite loop by omitting all three, like this:
>
> ```js
> for (;;) { //infinite loop
>  doSomething();
> }
> ```

> ####Note
> The for loop can be turns into a while loop including only the control expression
> 
> ```js
> var count = 10;
> var i = 0;
> for (; i < count; ) {
>   console.log(i);
>   i++;
> }
> ```

### The for-in Statement

The for-in statement is a strict iterative statement used to enumerate the properties of an object.

```js
for (property in expression) statement
```

> #### Example
> 
> ```js
> var obj = {a: 1, b: 2, c: 3};
> var s = '';
> for (var key in obj) {
>   s += key + ' ';
> }
> console.log(s); //"a b c ";
> ```
