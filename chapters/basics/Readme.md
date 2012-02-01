# Language Basics

## Syntax

ECMAScript’s syntax borrows heavily from C and other C-like languages such as Java and Perl.

### Case-sensitivity

Everything is case-sensitive:
*variables*, *function names*, and *operators* are all case-sensitive.

### Identifiers

An identifier is the name of a variable, function, property, or function argument.

Identifiers may be one or more characters in the following format:

* the first character must be a letter, an underscore (_), or a dollar sign ($)
* all other characters may be letters, underscores, dollar signs, or numbers

Letters in an identifier may include extended ASCII or Unicode letter characters.

By convention, ECMAScript identifiers use camel case:

* the first letter is lowercase
* each additional word is offset by a capital letter

for example:

    firstSecond
    doSomethingImportant

### Comments
ECMAScript uses C-style comments for both single-line and block comments.

A *single-line comment* begins with two forward-slash characters, such as this:

    //single line comment

A *block comment* begins with a forward slash and asterisk (/*) and ends with the opposite (*/):

    /*
     * This is a multi-line * Comment
     */

Note that even though the second and third lines contain an asterisk,
these are not necessary and are added purely for readability.
(This is the format preferred in enterprise applications.)

