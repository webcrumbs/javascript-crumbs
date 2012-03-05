# Objects

- - -
## definition
Objects are colleciton of key/value pairs.

    !js
    var hero = {
      breed: 'Turtle',
      occupation: 'Ninja'
    };

Keys are strings: sometimes you have to quote them.
    
    !js
    var o = {
     something: 1,
     'yes or no': 'yes',
     '!@#$%^&*': true
    };
- - -
## access properties
    
    !js
    var hero = {
     breed: 'Turtle',
     occupation: 'Ninja',
     'finger count':  3
    };

### Dot notation.

    !js
    hero.breed; // "Turtle"

### Square bracket notation.

    !js
    hero['finger count']; // 3

### If property name is stored in a variable, use it with square bracket notation.

    !js
    var keyName = 'occupation';
    hero[keyName]; // "Ninja"
- - -
## set properties

### Properties can be dynamically added and modified using both notations.

    !js
    var hero = {};
    hero.breed = 'turtle';
    hero['name'] = 'Leonardo';
    console.log(hero);

- - -
## delete properties

### Properties can be even deleted.

    !js
    var hero = {};
    hero.breed = 'turtle';
    hero['name'] = 'Rafaelo';
    delete hero.breed;
