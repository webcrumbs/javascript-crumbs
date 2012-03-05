# Statements

- - -
## code block statement

    !js
    {
      //code block
      {
        //nested code block
        //use indentation
      }
    }

- - -
## `if` statement

    !js
    if (condition) statement1 else statement2

    !js
    if (condition1) statement1 else if (condition2) statement2 else statement3

    !js
    if (condition1) {
      statement1 
    } else if (condition2) {
      statement2 
    } else {
      statement3
    }

- - -
## `switch` statement

    !js
    switch (expression) {
      case value1: statement1; break;
      case value2: statement2; break;
      //...
      case valueN: statementN; break;
      default: statement
    }

- - -
## `do-while` statement

    !js
    do {
      statement
    } while (expression);

- - - 
## `do-while` statement

    !js
    var i = 0;
    do {
      i += 1;
    } while (i < 10);

    console.log(i); //?

- - -
## `while` statement

    !js
    while (expression) statement


- - - 
# `while` statement

    !js
    var i = 0;
    while (i < 10) {
      i += 2;
    }

- - -
## `for` statement

    !js
    for (initialization; expression; post-loop-expression) statement

- - -
## `for` statement

#### `while` using `for`

    !js
    var count = 10;
    var i = 0;             //initialization
    for (; i < count; ) {  //expression
      console.log(i);
      i++;                 //post-loop-expression
    }

- - -
## `for` statement

#### infinite loop

    !js
    for (;;) { //don't try this at home!
      doSomething();
    }

- - -
## `for in` statement

    !js
    for (property in object) statement

- - -
## `for in` statement

    !js
    var obj = {a: 1, b: 2, c: 3};
    var s = '';
    for (var key in obj) {
       s += key + ' ';
    }
    console.log(s); //?;

