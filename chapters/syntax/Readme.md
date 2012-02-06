# Syntax

JavaScript syntax borrows heavily from C and other C-like languages such as Java and Perl.

## Case-sensitivity

In JavaScript, everything is case-sensitive:  
*variables*, *function names*, and *operators* are all case-sensitive.

## Identifiers

An *identifier* is the name of a variable, function, property, or argument.

Identifiers may be one or more characters in the following format:

* the first character must be a letter, an underscore (_), or a dollar sign ($)
* all other characters may be letters, underscores, dollar signs, or numbers

Letters in an identifier may include extended ASCII or Unicode letter characters.

By convention, JavaScript identifiers use camel case:

* the first letter is lowercase
* each additional word is offset by a capital letter

    firstSecond
    doSomethingImportant

### Comments

JavaScript uses C-style comments for both single-line and block comments.

A *single-line comment* begins with two forward-slash characters:

    //single line comment

A *block comment* begins with a forward slash and asterisk (/*) and ends with the opposite (*/):

    /*
     * This is a multi-line
     * Comment
     */

Note that even though the second and third lines contain an asterisk,
these are not necessary and are added purely for readability.
(This is the format preferred in enterprise applications.)

## Statements

Statements in ECMAScript are terminated by a semicolon,

    var sum = a + b //valid even without a semicolon - not recommended
    var diff = a - b; //valid - preferred

Even though a semicolon is not required at the end of statements, it is recommended to always include one.

Including semicolons helps prevent errors of omission, such as not finishing what you were typing,
and allows developers to compress ECMAScript code by removing extra white space
(such compression causes syntax errors when lines do not end in a semicolon).

Including semicolons also improves performance in certain situations,
because parsers try to correct syntax errors by inserting semicolons where they appear to belong.

Multiple statements can be combined into a code block by using C-style syntax,
beginning with a left curly brace ({) and ending with a right curly brace (}):

    if (test) {
      test = false;
      alert("hello!");
    }

Control statements, such as if, require code blocks only when executing multiple statements.
However, it is considered a best practice to always use code blocks with control statements,
even if there’s only one statement to be executed.
Using code blocks for control statements makes the intent clearer,
and there’s less chance for errors when changes need to be made.

    if (test)
        alert("hello!"); //valid, but error-prone and should be avoided

    if (test) { //preferred
         alert(test);
    }


## Keyowrds and Reserved Words

### Keywords

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

### Reserved words

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
