
Ways of instantiating an object:
  * Factories(DEFAULT): Functions that create and return objects
    * More flexible and easier
    * Have private properties
    * DOesnt use this
  * Prorotypes
    * Better performance
    * Less memory
  * Class: instanciate with new (fast but dont use because this is not correctly bound)

**Factories**
Function that returns an object. consts are encapsulated by closure. And only talk is available, and it has aceess to sound
```javascript
const dog = () => {
  const sound = 'woof'
  return {
    talk: () => console.log(sound)
  }
}
const sniffles = dog()
sniffles.talk() // Outputs: "woof"
```


**Using Object.Create to create with prototype**
```javascript
const food = {
  init: function (type) {
    this.type = type
  },
  eat: function () {
    console.log('You ate the ' + this.type)
  }
}
food.name="BaseFood";
const waffle = Object.create(food)
waffle.init('waffle')
waffle.eat() // Output: "You ate the waffle"
food.isPrototypeOf(waffle)//true
console.log(waffle.name) // Falls back to the prototypes name = "BaseFood";
waffle.name="waffle"
console.log(waffle.name) // now it has its name: "waffle";
```

**JSON**
```javascript
var string = JSON.stringify({name: "X", born: 1980});
console.log(string); // → {"name":"X","born":1980}
console.log(JSON.parse(string).born); // → 1980
```

**Filter**
It filters out the elements in an array that don’t pass a test.
```javascript
console.log(ancestry.filter(function(person) {
  return person.father == "Carel Haverbeke";
}));
```

**Map**
```javascript
The map method transforms an array by applying a function to all of its elements and building a new array from the returned values. The new array will have the same length as the input array, but its content will have been “mapped” to a new form by the function.
console.log(map(overNinety, function(person) {
  return person.name;
}));
```

**Reduce**
computing a single value from arrays: adding numbers or finding the person with the earliest year of birth in the data set. The parameters to the reduce function are, apart from the array, a combining function and a start value.
```javascript
console.log(reduce([1, 2, 3, 4], function(a, b) {
  return a + b;
}, 0));
// → 10
console.log(ancestry.reduce(function(min, cur) {
  if (cur.born < min.born) return cur;
  else return min;
}));
```


**Bind**
The bind method, which all functions have, creates a new function that will call the original function but with some of the arguments already fixed.

**Apply / Call**
Passes the first argument to the function's this.
```javascript
function speak(line) {
  console.log("The " + this.type + " rabbit says '" + line + "'");
}
var fatRabbit = {type: "fat", speak: speak};

speak.apply(fatRabbit, ["Burp!"]);
// → The fat rabbit says 'Burp!'
speak.call({type: "old"}, "Oh my.");
// → The old rabbit says 'Oh my.'
```

**Getters and setters**
```javascript
var pile = {
  elements: ["eggshell", "orange peel", "worm"],
  get height() {
    return this.elements.length;
  },
  set height(value) {
    console.log("Ignoring attempt to set height to", value);
  }
};
console.log(pile.height);
// → 3
pile.height = 100;
// → Ignoring attempt to set height to 100
```



--


#Douglas Crockford the Javascript programming language

Javascript definitive guide Oreilly (rhinoceros)

Loosely typed: any type can be used anywhere

**names**
  * all functions, vars, params lowercase
  * Constructors uppercase
  * _ initial for implementation
  * $ initial for machines
**lambda:** Functions as first class objects

**logical** Operands
  && And
  * if first operand is truthy, returns second.
  * else returns first.
  * Can be used to avoid null refs.  
```javascript return a && a.member;
```

|| Or
* if first operand is truthy, returns first.
* else returns second.
* Can be used to fill defaults
```javascript var last = input || nr_items;
```

**string to number** +"42" = 42
**strings** are immutable

**false** values
  undefined (not defined or can be set as undefined )
  0
  NaN
  false
  null (no value
  ""
* everything else is objects

**Objects** An object is a hashtable (name, value) pairs

return; retue=rns undefined.
constructors will return this.

**maker function**
```javascript
function maker(name, grade){
  var it = {};
  it.name=name;
  it.grade=grade;
  return it;  
}
myObject = maker('Jack', 2);
```
---
##~~~~~maybe move this to Object contstuctor

##Prototyal inheritance
**Linkage** Greater expressive power, different than classes.
* Objects can have a link to aother object.
* If an attempt to access a name fails, the link will be used to the old object.
* NOT used for storing. Only stores on the primary obeject.
* So you make objects similar to existing objects, and then customized
* YOu can chain many objects, Object.prototype is always the last.
* hasOwnProperty() //is it a member of the object

```javascript
myOldObject.level=3;
var myNewObject = object(myOldObject) //inherits from myOldObject
//myNewObject points to myOldObject

myNewObject.level+=1; //new object doesnt have level.
//so it takes level from oldObject
// But always stores in the current one, not on the parent.
```

```javascript
object(o); //makes an empty objet with a link to o

function object(o){
  function F() {}
    F.prototype = o;
    return new F();
}
newObject = object(oldObject)
```

* augmenting yhr prototype augments all its objects
* but changes to obkects will not go back to the prototype

#inheritance
* Constructor Functions
* new operator
* prototype member


# ~object.prototype HAS to point to another object.... from which it inherits

**object Properties**
* No equality on objects!!!!
* Only check references to the same object(pointers) === true if are the same
* passed by ref.
* delete myObj[name]//changes it to undef.


###Ways og Object construction
* new Object()
* {} //preferred
* object(object.prototype)

##arrays
* DO NOT USE FOR IN
* use traditional for
* mutable
* use [] to create neew array.
* linked to array.prototype
* check if is array:  value instanceof Array;
* Dont use arrays as prototypes.
* augment array or array.prototype;

**methods**
* concat:  merges arrys
* join: outputs a single string
* pop + push
* slice sort .
* delete will leave an undefined hole in the middle use **splice** instead.
* splice(a,b) starting at a delete b number of stuff.

**splice**
```javascript
  myarr=['a','b','c','d'];
  myarr.splice(1,1); //['a','c','d']
```

## Functions
* First class objects.
* work like any other value
* inherit from object, can store name value pairs
* Called lambda in other languages.
* It is secure.
* **Static Scoping** Inner functions have access to the params of the functions it is contained in.
* **closure** The variable still have access to the parents values, even if the parent doesn't exist anymore (has returned); has access to it, IS NOT A COPY.
Each function has it's own scope. Are local vars to the function. (meaning that multiple calls to the same method will not mess with each other.)

**Static Vars on Functions**
```JavaScript
~~~
```

###Function Invocation.
* 'this' is bound at invocation time.
**Function Form**
  ```javascript functionObject(args)
  ```
  * this is set to the global obj.
  * not very useful
  * makes it harder to write helper functions within a method because it doesn't have access to outer this.
  * use ``` var that = this; ``` in the inner.

**Method Form**
  ```JavaScript
  thisObject.MethodName(args)
  thisObject["MethodName"](args)
  ```
  * this on the function will be a reference to thisObject

**Constructor Form**
  ```JavaScript new functionObject(args)
  ```
  * A new object is created and assigned to this.   
  * if no return is especified, this will be returned.

**Apply Form**
  ```JavaScript functionObject.aply(thisObject, [args])
  ```
  *  ~~~




#### Invocation: Arguments
* functions also receive a parameter called ``` arguments ```
* contains invocation args in an array-like object with length.
```Javascript
function sum(){
  arguments.lenth;
  add all in arguments array
  return total
}
```

##Augmenting Built in types.
* For example add **trim** to string
```Javascript
  String.prototype.trim = function () {
    return this.replace(
      /^\s*(\S*(\s+\S+)*)\s*$/, "$1");
  }
```
**Augmenting Strings**

```Javascript
var data = {
  name: 'Carl',
  state: 'Happy'
};
var template = 'someone named {name} is {state}'
var myStr = template.supplant(data);

String.prototype.supplant = function(o) {
  return this.replace(/{([^{}]*)}/g,function(a, b) {
    var r = o[b];
    return typeof r === 'string' || typeof r === 'number' ? r : a;
  });
};
```

## typeof
object='object'
function='function'
***array='object'***
number='number'
string='string'
boolean='boolean'
***null='object'***
undefined='undefined'

##eval DONT USE    Unless you can absolutely trust JSON.
* Compiles and returns the result
* Is what the browser uses to convert strings into actions.
``` eval(string)
 ```
* same as New function Functtion

## (global) Object
* container for global vars and all built in objects
* On browsers window is the global.
* sometimes 'this' points to it. ``` var global = this; ```

**this is evil**
* Functions and vars can crash with each other.
* try to reduce its use
* vars without var are global.
* Create ONE global object and place everything there.


## Encapsulation
* Has no leakage
* Only shows what we want to return.
* Uses closures
* makes all vars private.

```javascript
YAHOO.Trivia = function () {
  //define common vars & functions here
  return {
    getNextPoster: function (cat,diff){   /* ...Stuff..  */}
    showPoser: function () {   /* ...Stuff..  */}
    }
}
var trivia = YAHOO.Trivia();
}
```

###RegExp
-patterns enclosed in slashes

##inheritance.
* Object oriented code reduce
* two schools: Classical(JAva) Prototypal(JS)
* Objects inherit fro object with a secret link to another object.






##DOM STUF WITH JS~~~
document.getElementbyId(id)


# End Douglas

---

####This

**Object Literal**
 var stooge = {
         "first-name": "Jerome",
         "last-name": "Howard"
};
stooge.first-name="asd";
stooge["first-name"]; //asd

**Prototype** Every object is linked to a prototype object from which it can inherit properties.

When we make changes to an object, the object’s prototype is not touched:

The prototype link is used only in retrieval. If we try to retrieve a property value from an object, and if the object lacks the property name, then JavaScript attempts to retrieve the property value from the prototype object. And if that object is lacking the property, then it goes to its prototype, and so on.  This is called ***delegation***.



So object.prototype points to another object.
This example is to illustrate prototypes. DONT use new.
```javascript
var man = {};  
man.sex="male";

var yehuda = Object.create(man);  
yehuda.firstName="Yehuda";  
yehuda.lastName="Katz";

console.log(yehuda.sex);       // "male"  
console.log(yehuda.firstName);  // "Yehuda"  
console.log(yehuda.lastName);   // "Katz"

var man2 = Object.getPrototypeOf(yehuda); // returns the man object  
console.log(man===man2);
```





###Enumeration
For in //doesnt guarantee order.
For each
for(var i; i<length;i++)

###delete
delete another_stooge.nickname;

###Global Vars
Weaken the resiliency of programs.
Use one single global var MyApp.

####Functions
Functions in js are objects. Can be used as any other values. And can have other inside functions.
Invocation: Every call receives 'this' and args.

###Method Invocation
* When a function is stored as a property of an object, we call it a method. When a method is invoked, this is bound to that object. (when invocation contains a dot . )
 ```javascript
     var myObject = {
         value: 0,
         increment: function (inc) {
             this.value += typeof inc === 'number' ? inc : 1;
} };
myObject.increment( ); // myObject.value => 1
myObject.increment(2);// myObject.value => 3
```

###The Function Invocation
* When a function is not the property of an object, then it is invoked as a function:
```javascript   var sum = add(3, 4);    // sum is 7
```
When a function is invoked with this pattern, this is bound to the global object.
```javascript

myObject.double = function () {
  var that = this; // Workaround.
  var helper = function () {
    that.value = add(that.value, that.value);
  };
  helper(); // Invoke helper as a function.
};
     // Invoke double as a method.
myObject.double( );
myObject.value(); // 6
```

###The Constructor Invocation Pattern **DO NOT USE THIS (new)**
* If a function is invoked with the *new* prefix, then a new object will be created with a hidden link to the value of the function’s prototype member, and this will be bound to that new object.
* Functions intended to use **new** prefix are called constructors.
* By convention, they are kept in variables with a capitalized name.
* *new* returns a new object with a pointer to the constructor's prototype

```javascript
// Create a constructor function called Quo. It makes an object with a status property.
var Quo = function (string) {
  this.status = string;
};
// Give all instances of Quo a public method called get_status.
Quo.prototype.get_status = function () {
  return this.status;
};

var myQuo = new Quo("confused");// Make an instance of Quo, with a link to the constructor.prototype.
document.writeln(myQuo.get_status()); // Get method from he constructor prototype (Quo)
```



###The Apply Invocation Pattern
functions can have methods.

The apply method lets us construct an array of arguments to use to invoke a func- tion. It also lets us choose the value of this. The apply method takes two parame- ters. The first is the value that should be bound to this. The second is an array of parameters.
```javascript

// Make an array of 2 numbers and add them.
var array = [3, 4];
var sum = add.apply(null, array);    // sum is 7
// Make an object with a status member.
var statusObject = {
  status: 'A-OK'
};
// statusObject does not inherit from Quo.prototype,
// but we can invoke the get_status method on
// statusObject even though statusObject does not have
// a get_status method.
var status = Quo.prototype.get_status.apply(statusObject);
// status is 'A-OK'

```

####Return
A function always returns a value. If no return specified, it returns udefined.

###Public methods
* method that uses this to access an object
* can be reused with many 'classes'

```javascript
function(string) { //can be used with any object
  return this.member + string;
}
```
###MOdule
* Varuables defined in a module are only visible in the module
* FUnctions can be used to contain modules

###Singletons
* Objects instantiated *once*
* can be created with object notation

* Another way of writing a singleton.(using closures)

```javascript
var singleton = function(){
  var privateVar;
  function provateFunc(){};

  return {
    firstmethod: function(a,b){
      //dostuff with private var & function
    }
  }
}(); //we assign the result of invoking the function to the singleton.

singleton.firstmethod(1,2);
```

###Power Constructor
* using a singleton module pattern in a constructor and we have a power constructor

```javascript
function powerConstructor(){
  var that=object(oldObject); //or use that={};
  var privateVar;
  function provateFunc(){};
  //Privileged methods, gettes, setters etc.
  that.firstmethod: function(a,b){
      //dostuff with private var & function  
  }
  return that;
}
myObject=power_constructor();
```

**Functions in Loops**
When assigning functions in a loop, all will be bound to the same closure.
~~
REALLY REMEMBER THIS.


#Debugging
if(something==='wrong){
  debugger;
}
~ Complete this Stuff
---

#### High Order Functions
A function that can accept other function as an argument. This is called **Composition:** of functions.
This works because in js functions are values.

```javascript
var isDog = function(animal){
	return animal.species==='dogs';
	}
var dogs = animals.filter(isdog);
var dogs = animals.filter(anml => anml.species==='dogs')
```
##### Map
Transforms the array. (Opposite is reject)
```javascript
//returns names of the animals.
var names = animals.map(function(animal){
	return animal.name;
})

//map to return other val
var names = animals.map(function(animal){
	return animal.name+ 'is a '+ animal.species;
})
```

##### Reduce
See my [Reduce](moarCode/reduceExamples.md) page for details.
```javascript
var orders = [
  { amount: 250 },
  { amount: 400 }
]

var totalAmount = orders.reduce( function(sum, order) {
  return sum + order.amount
}, 0) //takes an object as starting point. 0 here
//totalAmount=>650

```

##3promises
Dealing with asyinc callbacks.

##### Arrow functions (ES6)
(args) => {code}

```javascript
var names = animals.map((x) => x.name)
```






The **create**




**Closures:** The function body has access to vars defined outside it. (All functions in JS are closures).
Example: Callback functions can access stuff availabele to them where they were declared.
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures

**pure functions**

**Call+apply**

**assign**



**Composition:** What objects do
**Inheritance:** modeled around what they are

**Factories:** Function that create objects and return the. Simpler than classes.

####classes DO NOT USE
```javascript
class Dog {
  constructor() {
    this.sound = 'woof'
  }
  talk() {
    console.log(this.sound)
  }
}
const sniffles = new Dog()
sniffles.talk() // Outputs: "woof"
$('button.myButton').click(sniffles.talk) //outputs stuff you dont want
```

####Factories  USE
```javascript
const dog = () => {
  const sound = 'woof'
  return {
    talk: () => console.log(sound)
  }
}
const sniffles = dog()
sniffles.talk() // Outputs: "woof"
```

favor composition over inheritance
###Composition
Designing types around what they do
Composition example [here](moarCode/compositionExample.md)

###Inheritance
Designing types around what they are
You get the object but also a lot of extra stuff you dont need

**object.assign({}, meower(state)) **
Takes an object and assigns the properties of the other passed objects

**currying** Function that takes arguments. Uses the first arg and returns a new function and calls it with the secnd arg and so on.

**lodash**

**Bind**



----


## Don't Use
**new** Use **create**

**for** or **for in** because order is not known. Use: **for each**

```javascript
Object.keys(objet).for each
```

---

## Use

JsLint

---

---
## Angular.js
Directives
extensions to HTML like ng-app to star angular


ng-model="name" : adds model from a text box to the view model. Can be printed with {{  name }}

adds data array to viewModel
<body ng-init="names=[{name:'John Smith', city:'Phoenix'}, {name:'John Doe', city:'Philly'}]">
ng-repeat allows to list an array
ng-repeat="person in personArray"

Order:
ng-repeat="just in personArray | orderBy:'name'"
{{cust.name | uppercase}}

Filter/search
<input Type="text" ng-model="nameText" />
<li ng-repeat="just in personArray | filter:nameText '">
{{cust.name }} </li>

Scope is a view-Model. It is the glue between view and controller: $scope.
Controller sould't know the view because it may be different view for desktop, mobile etc.. View may know the controller.
$scope is the data of the view.
VController receives the $scope and passes the data in it.
function SimpleController($scope){
	$scope.data='asd';
}
view. Only this part gets the div,
<div ng-controller='SingleController'>
{{ data }}
<//div>
View Defines which controller it will use

ng-click="loginEmail()"
calls the function on the controller

---
## D3.js
```html
D3

 <script>

      var scale = d3.scale.linear()
        .domain([1, 5])   // Data space
        .range([0, 200]); // Pixel space

      var svg = d3.select("body").append("svg")
        .attr("width",  250)
        .attr("height", 250);

      function render(data, color){

        // Bind data
        var rects = svg.selectAll("rect").data(data);

        // Enter: Constructing the elements. only adds elements that weren't there and properties that won't change

        rects.enter().append("rect")
          .attr("y", 50)
          .attr("width",  20)
          .attr("height", 20);

        // Update: stuff that changes
        rects
          .attr("x", scale)
          .attr("fill", color);

        // Exit: delete unused
        rects.exit().remove();
      }

      render([1, 2, 2.5],     "red");
      render([1, 2, 3, 4, 5], "blue");
      render([1, 2],          "green");

    </script>


rects.enter().append("rect").data

```

---

# Videos

Asynchronous Programming at Netflix - @Scale 2014 - Web
https://www.youtube.com/watch?v=gawmdhCNy-A

James Coglan: Practical functional programming: pick two | JSConf EU 2014
https://www.youtube.com/watch?v=XcS-LdEBUkE

Bret Victor The Future of Programming
https://www.youtube.com/watch?v=8pTEmbeENF4

Philip Roberts: What the heck is the event loop anyway? | JSConf EU 2014
https://www.youtube.com/watch?v=8aGhZQkoFbQ

---

# Extras
cool guy tutorial videos: https://www.youtube.com/playlist?list=PL0zVEGEvSaeEd9hlmCXrk5yUyqUag-n84

---

# Books
- Programming Javascript applications - Eric Elliot
- You Don't Know JS: Up & Going -  Kyle Simpson



#jsconf




#STUFF YOU SHOULDN'T USE

## Constructor functions
Start with capital letter and create instances with new
The new object’s prototype will be the object found in the prototype property of the constructor function.

```javascript
function Rabbit(type) {
  this.type = type;
}
var blackRabbit = new Rabbit("black");
console.log(blackRabbit.type);  // → black

Rabbit.prototype.speak = function(line) {
  console.log("The " + this.type + " rabbit says '" + line + "'");
};
blackRabbit.speak("Doom..."); // → The black rabbit says 'Doom...'
```
