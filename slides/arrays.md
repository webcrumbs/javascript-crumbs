# Array

- - -
## definition

    !js
    var a = ['one', 'two', 'three'];
    var empty = [];
    var plain = [1+2,'four'];
    var matrix = [[1,2,3], [4,5,6], [7,8,9]];
    var sparseArray = [1,,,,5];

Arrays are objects, but of a special type because:  
– the names of their properties are automatically assigned using numbers  
– they have a `length` property which contains the number of elements in the array  

    !js
    var a = ['one', 'two', 'three'];
    a.length; //3
    typeof a; //"object"

- - -
## access

Arrays can be accessed through square bracket notation.

    !js
    var a = ['one', 'two', 'three'];
    a[1]; //"two"
    a['1']; //"two"
    a[1] = 2
    a[1]; //2
    var matrix = [[1,2,3], [4,5,6], [7,8,9]];
    matrix[0][1]; //2

- - -
## `push(item...)` method

It accepts any number of item to push in the array.  
It returns the array's new length.  

    !js
    var colors = [];   // create an array
    var count = colors.push('red', 'green'); // push any number of items
    count;  // 2
    colors; // ["red", "green"]

    count = colors.push('black');   // push another item on
    count;  // 3
    colors; // ["red", "green", "black"]
- - - 
## `pop()` method

It acceps no parameter.  
It returns and removes the last element in the array.  
If the array is empty, return undefined.

    !js
    var colors = new Array('red', 'green', 'black');

    var item = colors.pop(); // get the last item
    item; // "black"
    colors.length; // 2
    colors; // ["red", "green"]