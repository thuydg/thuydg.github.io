---
layout: blog
title: Study javascript and object oriented
category: blog
tags: [javascript, oop]
summary: Javascript
image: http://i.ytimg.com/vi/coIsvOMYEi0/hqdefault.jpg
---

# Contents

## Define a class in javascript

Javascript is a prototype-based language and contains no class. Instead, Javascript uses functions as classes. Defining a class is as easy as defining a function.

     var Person = function() {};


## How to create an object base on function

     var person1 = new Person();
     var person2 = new Person();

## Constructor

Constructor is called at the moment of instatiation. It is a method of class. In Javascript, a function serves as the constructor of the object so there is no need to explicit define a constructor method.

     var Person = function() {
       console.log("a new Person was born!");
     }
     var person1 = new Person();

## The property

Properties are variables that is contained in class.
Every instance that is created will have these variables.
You can use the keyword "this" to get access to the variables inside of the class.

     var Person = function(givenName) {
       this.name = givenName;
     }

     var person1 = new Person("New_name");
     console.log("A new person has created! let's call him as: " + person1.name );

## The methods

Methods are functions but follow the same logic as properties.
To define a method, assign a function to a named property of the class's "prototype" property.

      var Person = function(givenName) {
        this.name = givenName;
      }

      Person.prototype.sayHello = function() {
        console.log("Hello, my name is" + this.name );
      }

      var person1 = new Person("New_name");
      person1.sayHello();

## Inheritance

Inheritance is a way to create a class as a specialized version of one or more classes. The specialized class is commonly called the "child", and the others is called the "parents".

     //Define for Person class
     var Person = function(givenName) {
       this.name = givenName;
     }
     Person.prototype.walking = function() {
       console.log("I am walking");
     }
     Person.prototype.sayHello = function() {
       console.log("Hello, my name is" + this.name );
     }

     //Define Student constructor
     function Student(givenName, subject) {
       //Call the parent constructor
       Person.call(this, givenName);
       this.subject = subject;
     }
     //Create the prototype that inherits form Person.prototype
     Student.prototype = Object.create(Person.prototype);
     Student.prototype.constructor = Student;
     //Replace sayHello
     Student.prototype.sayHello = function(){
        console.log("Hello, I'm " + this.firstName + ". I'm studying " + this.subject + ".");
     };

## Nodejs module pattern and inheritance

For Animal class like following:

```
function Animal() {
  var walked = false;
  function walk() {
    console.log('walking...');
    walked = true;
  }

  function hasBeenWalked() {
    return walked;
  }

  return {
    walk: walk
  , hasBeenWalked: hasBeenWalked
  }
}

module.exports = Animal
```

We can create Cat class that inherits Animal class like following codes.

```
var Animal = require('./animall')

function Cat() {
  var cat = {}
  var walked = false

  cat.__proto__ = Animal()

  cat.pat = function pat() {
    console.log('being patted')
  }

  cat.lasagna = function lasagna() {
    console.log('Lasagna!')
    walked = true
  }

  return cat
}
```

# Reference

* [Javascript object oriented programming](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript)
* [The module pattern and inheritance](http://metaduck.com/08-module-pattern-inheritance.html)
