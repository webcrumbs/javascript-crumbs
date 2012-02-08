## Statements

#### Code Blocks
consists of zero or more expressions enclosed in curly brackets `{` and `}`;
they can be nested within each other indefinitely.

```js
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
```

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

> #### Convension 
> Use code blocks for control statements, even when it is only one expression.
> ```js
> if (test)
>   console.log('hello!'); //valid, but error-prone and should be avoided
> 
> if (test) { //preferred
>   alert(test);
> }

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

The step-by-step procedure for executing a `switch` statement is as follows:

1. evaluate the `switch` `expression` found in parentheses, remember it
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

The `switch` statement prevents writing something like this:

```js
if (i == 25) {
  console.log("25");
} else if (i == 35) {
  console.log("35");
} else if (i == 45) {
  console.log("45");
} else {
  console.log("other");
}
```

The equivalent switch statement is as follows:

```js
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
```

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

var i = 0;
while (i < 10) {
  i += 2;
}

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
