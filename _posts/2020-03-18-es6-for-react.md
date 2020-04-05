---
layout: post
title: ES6 Features for React
image: "assets/img/thumbnails/es6.png" #seo tag
tags: [ES6, JavaScript]

header-color: rgb(33, 33, 33);

excerpt_separator: <!--more-->
published: true
---

In this post, we are going to take a look at common ES6 features that are very helpful in React projects and in general JavaScript development. ES6 (ECMAScript 6) is a JavaScript standard released in 2015, which introduced many new powerful features that help in writing concise, clear and readable code. It is supported across all the major browsers<!--more-->, you can check it's status on [Can I Use](https://caniuse.com/). 

* TOC
{:toc}
  Following topics will be covered in this post.

### Template literal
> Template literals (template strings) provide the ability to create single and multi-line strings with variables between them

We use the back quote characters ` to represent a template string. We can create multi-line strings without adding special characters like \n. Also we can add variable values by putting a variable between ${}.

```jsx
let total   = 100
let product = 'Dell laptop'
let message = `The price for product ${product} is ${total}
               Thank you.`
```
Printing message will generate the following output:
```output
The price for product Dell laptopn is 100
Thank you
```


### Arrow function
> Arrow functions provide a shorter way of defining a function. Also arrow have no binding to `this`, allowing arrow functions to be safely used as event handlers and access component's properties without using bind(this) method to explicitly bind it to the class context.

Just like any JS function, arrow functions can also be passed as parameters. They are used in two flavors. 
#### As a statement
In this case, a single statement is executed from the arrow function. A single statement can be represented using round braces () or no braces at all.

*Note: Return keyword will give error when using this variant*

```jsx
let log = () => console.log('Hello') 
let getMessage = (message) => 'Hello ' + message // explicit return keyword will give error
let getMessageGlobal = (message) => ('Hello ' + message) // explicit return keyword will give error

log() // prints 'Hello'
getMessage('React') // return string with value 'Hello React'
getMessageGlobal('World') // return string with value 'Hello World'
```
#### As a block
In  this case, a whole code block is executed from teh arrow function. The code block is opened using curly braces {}. 

*Note: We have to mention return keyword, if we want to return something in this variant*

```jsx
let mulBy10 = (input) => {
    let result = input * 10
    return result
}

mulBy10(100) // returns a number with value 1000
```

### Spread operator
> Spread operator ... allows spreading(actual copy not just a reference) of elements in an iterable collection (array or string) to individual elements and function parameters.


```jsx
let params = ['name', 'age']
let fullParams = ['device', 'location', ...params] // will become ['name', 'age','device', 'location']

let obj = {name:'bob', className:10} // class is a keyword in JS so we use className
let newObj = {height: 6, ...obj} // {height: 6, name: 'bob', className: 10}
```

### Enhanced object properties
These features provide a shorter way of modifying/ creating properties in an object.
#### Property shorthand
Property shorthand syntax provides a shorter way to adding/modifying properties in an object.
```jsx
let x = 1, y = 10,  z = 20
let demo = {x, y} // {x:1, y:10}
// mixing it up with the spread operator to add new properties
demo = {...demo, z, p:100} // {x:1, y:10, z:20, p:100}
```
In React, we'll mostly use the **property shorthand** to create new objects or add new properties to existing objects. A common case of using spread operator with property shorthand is to add new properties in the state object.
#### Computed property names
> Computed property names are dynamic property names.

This is a very interesting feature that adds a lots of conciseness and readability in the code. 
```jsx
let propertyName = 'anything' // we can even use template literal here `name${someVar}`
let myObject     = {name: 'Bob', title:'The builder', [propertyName]: 100} // {anything: 100, name: 'Bob', title: 'The builder'}

// a common use-case in React when we have multiple inputs and we want to update their values in the state during onChange event
this.setState{[event.target.name]: event.target.value}
```
### Destructuring
Destructuring allows us to get values from arrays and objects into variables.
#### Array matching
In this case, we get values out of array into variables. For it, we use square braces around the variable names.
```jsx
let ls = [10,15,5,1,2]
let [a, b] = ls 
console.log(a , ' ', b) // 10 15
[a, b] = [b, a] // interesting case
console.log(a , ' ', b) // 15 10
```
If the array length is less than the variable counts we are trying to get out of, then they'll get undefined value.
#### Object matching
In this case, we get values out of object into variables. For it, we use curly braces around the variable names.
```jsx
let someObj = {name: 'Bob', className: 10} // class is a keyword in JS so we have to use className
let {name, className} = someObj
console.log(name, ' ', className) // Bob 10
```
#### Parameter context matching
We can use the same concepts as before to the get values from objects and arrays into parameters.
```jsx
function getParameterFromArray( [a, b, c] ){
  console.log(a,b,c)
}
getParameterFromArray([1,2,3,4,5]) // prints 123

function getParameterFromObject( {name, className} ){
  console.log(name, ' ', className)
}
getParameterFromObject({name: 'Bob', className: 10, height: 6.0}) // prints Bob 10
```
### Let and const
ES6 also allows us to **block level scoping** using let and const keyword for variables creation.
So basically, JS has function level scoping and that can be quite limiting or result in unexpected behavior for people that are used to block level scoping. 
Block level scoping works on code blocks like loops, if conditions etc. Using let and const to declare a variable we can create block scoped variables. I'll write a post about all the details and gotchas for let and const in a separate post. 
```jsx
var myFunction = null // using var here only for demo
if(1==1) // Opening a Block
{ 
  let blockVar = 10 // later replace it with var to see the difference
  myFunction = ()=>{
    // Our business requirement: It supposed to print 10 always
    console.log('Result: ', blockVar) // accesses the block level variable
  }
}
blockVar = 20 // creates a global variable and won't alter ones in the block
myFunction() // prints Result: 10

// const also have same block level scoping as let; however, they cant be reassigned
const TAX = 10
TAX = 20 // ERROR: Assignment to constant variable
```
In order to check the difference between var and let, replace let variable with a var. You'll see  that block level variables using var are created in the global scope and thats a bummer. In JavaScript, we have only function level scopes. Thankfully using let we have a simpler and cleaner solution for declaring block scoped elements.

### Declaring classes
ES6 also introduces proper syntax for creating classes. Previously we had to add methods and properties using prototypes on function objects.
```jsx
class Test(){
  constructor(){
    this.x = 10 // creating properties
    this.y = 20
  }
  // creating a method
  test(){
    console.log(this.x, ' ', this.y)
  }
}
```



