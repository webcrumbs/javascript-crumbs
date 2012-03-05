# Object methods

- - -
## definition
An object contains properties.  
Since functions are just data, a property of an object can contain a function.  
In this case, you say that this property is a *method*.

    !js
    var dog = {
      name: 'Benji',
      talk: function(){
        alert('Woof, woof!');
      }
    };

- - -
## invocation

    !js
    var hero = {
      breed: 'Turtle',
      occupation: 'Ninja',
      say: function() {
        return 'I am ' + hero.occupation;
      }
    };

    hero.say();    // "I am Ninja"
    hero['say'](); // "I am Ninja"

- - -
## `this` value 

Inside a method, there is a special way to access the object this method belongs to:  
by using the special value `this`.

    !js
    var hero = {
      name: 'Rafaelo',
      sayName: function () {
        return this.name;
      }
    };

    hero.sayName();   // "Rafaelo"