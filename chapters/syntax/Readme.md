# Syntax

JavaScript syntax borrows heavily from C and other C-like languages such as Java and Perl.

## Case-sensitivity

In JavaScript, everything is case-sensitive:  
*variables*, *function names*, and *operators* are all case-sensitive.

## Identifiers

An *identifier* is the name of a variable, function, property, or argument.

Identifiers may be one or more characters in the following format:

* the first character must be a letter, an underscore `_`, or a dollar sign `$`
* all other characters may be letters, underscores, dollar signs, or numbers

```js
var name1;  // OK
var _name2; // OK
var $name3; // OK
var $;      // OK
var _;      // OK
var Name;   // OK
var 1name;  // SyntaxError: Unexpected token ILLEGAL
```

> #### tips
> Letters in an identifier may include extended ASCII or Unicode letter characters.
>
> ```js
> var Åmstrong; // OK
> ```
  
  
  
> #### convention
> JavaScript identifiers use camel case:
>
> * the first letter is lowercase
> * each additional word is offset by a capital letter
>
> ```js
> var firstSecond;
> var doSomethingImportant;
> ```

## Comments

JavaScript has both single-line and block comments.

#### single-line comment
begins with `//`:

```js
//single line comment
```

#### block comment
begins with `/*` and ends with `*/`:

    /*
     * This is a multi-line
     * Comment
     */

> #### convention
> for readability each line of block comment starts with `*`

## Statements

JavaScript statements are terminated by a semicolon `;`

```js
var sum = a + b   //valid even without a semicolon - not recommended
var diff = a - b; //valid - preferred
```
> #### tips
> Even though a semicolon is not required at the end of statements, it is recommended to always include one.
>
> Including semicolons helps prevent errors of omission, and improves performance in certain situations,  
> because parsers try to correct syntax errors by inserting semicolons where they appear to belong.

### Multiple statements
Multiple statements can be combined into a code block between curly braces `{` and `}`

```js
{
  test = false;
  alert('hello!');
}
```

## Keywords and Reserved Words

### Keywords

```js
break  
case  
catch  
continue  
do  
debugger  
default  
delete  
else  
finally  
for  
function  
instanceof  
if  
in  
new  
return  
switch  
this  
throws  
try  
typeof  
var  
void  
while  
with  
```

### Reserved words

```js
abstract                              
boolean                       
byte                              
char                              
class                            
const                             
debugger                  
double                  
enum
export
extends
final
float
goto
implements
import
int
interface
long
native
package
private
protected
public
short
static
super
synchronized
throws
transient
volatile
```