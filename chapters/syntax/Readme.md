# Syntax

## Syntax

### C-like syntax

JavaScript syntax borrows heavily from *C* 
and other C-like languages such as *Java* and *Perl*.

### Case-sensitivity

In JavaScript, everything is case-sensitive:  
*variables*, *function names*, and *operators* are all case-sensitive.

## Identifiers

An **identifier** is the name of a *variable*, *function*, *property*, or *argument*.

Identifiers 

* may be one or more characters
* start with a letter, `_`, or `$`
* may contain letters, numbers, `_`, or `$`

```js
var Name;     // OK
var name;     // OK
var _;        // OK
var _name1;   // OK
var $;        // OK
var $name2;   // OK
var π;        // OK
var Åmstrong; // OK
var 1name;    // SyntaxError: Unexpected token ILLEGAL
```

## Comments

JavaScript has both single-line and block comments.

### single-line comment

```js
// this is a single line comment
```

### block comment

```js
/*
 * This is a multi-line comment
 * note that just for readability 
 * each line of block comment starts with `*`
 */
```

## Statements

Statements are terminated by a semicolon `;`

```js
var diff = a - b; //OK
var sum = a + b   //OK but don't forget semicolon!
```
> #### tips
> Even though a semicolon is not required at the end of statements, it is recommended to always include one.
> 
> Including semicolons helps prevent errors of omission, and improves performance in certain situations,  
> because parsers try to correct syntax errors by inserting semicolons where they appear to belong.

Multiple statements can be combined into a code block between curly braces `{` and `}`

```js
{
  test = false;
  alert("hello!");
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
