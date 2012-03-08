# Syntax

- - -

# Syntax

JavaScript syntax borrows heavily from C  
and other C-like languages such as Java and Perl.

- - -

# Syntax

## Case-sensitivity

In JavaScript, everything is case-sensitive:  
*variables*, *function names*, and *operators*.

- - - 

# Syntax

## Identifiers

An *identifier* is the name of a variable, function, property, or argument

* may be one or more characters
* starts with a letter or `_` or `$`
* can contains letters, numbers, `_`, `$`

- - - 

# Syntax

## Identifiers

#### Examples

```js
var name1;    // OK
var _name2;   // OK
var $name3;   // OK
var $;        // OK
var _;        // OK
var Åmstrong; // OK
var π;        // OK
var Name;     // OK
var 1name;    // SyntaxError: Unexpected token ILLEGAL
```

#### Note 
Letters can be in extended ASCII or Unicode
  
- - - 

# Syntax

## Identifiers
  
#### convention

JavaScript identifiers use camel case:

* the first letter is lowercase
* each additional word is offset by a capital letter

```js
var firstSecond;
var doSomethingImportant;
var yetAnotherCamelCaseExample;
```

- - - 

# Syntax

## Comments

#### single-line comment

```js
//single line comment
```

#### block comment

```js
/*
 * This is a multi-line
 * Comment
 */
```

#### Convention
for readability each line of block comment starts with `*`

- - - 

# Syntax

## Statements

JavaScript statements are terminated by a semicolon `;`

```js
var sum = a + b   //valid even without a semicolon - not recommended
var diff = a - b; //valid - preferred
```

- - - 

# Syntax

## Statements

### Multiple statements

Multiple statements can be combined into a code block between curly braces `{` and `}`

```js
{
  test = false;
  alert('hello!');
}
```

- - - 

# Syntax

## Keywords and Reserved Words

### Keywords

```js
break        for          try          
case         function     typeof  
catch        instanceof   var  
continue     if           void  
do           in           while  
debugger     new          with
default      return       
delete       switch       
else         this         
finally      throws       
```

- - -

# Syntax

## Keywords and Reserved Words

### Reserved words

```js
abstract     extends     package      volatile
boolean      final       private      
byte         float       protected    
char         goto        public       
class        implements  short        
const        import      static         
debugger     int         super
double       interface   synchronized
enum         long        throws
export       native      transient
```
