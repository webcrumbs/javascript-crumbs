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
