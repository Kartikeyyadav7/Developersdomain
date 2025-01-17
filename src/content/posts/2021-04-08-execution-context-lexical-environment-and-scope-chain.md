---
template: blog-post
title: Execution Context, Lexical Environment and Scope chain
slug: /execution-context-lexical-environmenet-scope-chain
date: 2021-04-08 20:46
description: "Understand the most core of Javascript about execution context,
  lexical environment, and scope chain "
featuredImage: /assets/cover-image-execution-context.png
---
<!--StartFragment-->

Hey guys,

So execution context, lexical scope, and scope chain are sort of fundamental topics in JS so it's important to learn about it

Let's get started

## **Execution Context**

Now we know about the call stack (if you don't please refer to the last blog post [here](https://www.aviatecoders.com/how-javascript-works)) and we know that functions that are called goes onto the call stack and after returning the functions they are popped off the call stack and it gets empty

*We can say that every function that goes into the call stack has its execution context*

```javascript
function hello(){
 return "Hey guys"
}

function greetings(){
 return hello()
}

greetings()
```

Let's see this with an example

So in the above example when the JS engine encounters the function call greetings( ) it makes an execution context of that function and puts it onto the call stack and after that, it encounters hello( ) and makes its execution context and puts it onto the stack and finally, it returns "Hey Guys" and everything pops off one by one.

**A new execution context is created whenever a function is executed as the JS engine goes through the code**

![Execution Context](/assets/execution-context.png "Execution Context")

But always the very first execution context is the "Global Execution Context" which is defined even before any code is written in the JS file

The Global execution context has the global object which is the window object, the "this" keyword, and hoisting.

It has two phases the creation phase and the execution phase

In the creation phase, there is the window object, "this" keyword, and hoisting and

In the execution phase, the code is run

As you might know at the beginning the "this" keyword and the window object are the same

![Global Execution Context](/assets/global-execution-context.png "Global Execution Context")

## **Lexical Environment**

Before going into the lexical environment, let's understand what lexical means well it means where you write something or define something

So, as we know that when our program is run we have execution context of functions on the call stack and you can understand the lexical environment as each function has its planet where its variable is located and no one outside of the planet can use those variables

Let's understand this with an example

```javascript
function hello(){
 console.log("hell")
 const a = 10
}

function greet(){
 console.log("greet")
 const b = 20
 hello()
}

function start(){
 console.log("starting greet")
 const c = 30
 greet();
}

const d = 40

start()
```

Here as you can see when the start() function is called, it starts execution each function one by one, now if you want to see this in action please go to this ([latentflip](http://latentflip.com/loupe/?code=JC5vbignYnV0dG9uJywgJ2NsaWNrJywgZnVuY3Rpb24gb25DbGljaygpIHsKICAgIHNldFRpbWVvdXQoZnVuY3Rpb24gdGltZXIoKSB7CiAgICAgICAgY29uc29sZS5sb2coJ1lvdSBjbGlja2VkIHRoZSBidXR0b24hJyk7ICAgIAogICAgfSwgMjAwMCk7Cn0pOwoKY29uc29sZS5sb2coIkhpISIpOwoKc2V0VGltZW91dChmdW5jdGlvbiB0aW1lb3V0KCkgewogICAgY29uc29sZS5sb2coIkNsaWNrIHRoZSBidXR0b24hIik7Cn0sIDUwMDApOwoKY29uc29sZS5sb2coIldlbGNvbWUgdG8gbG91cGUuIik7!!!PGJ1dHRvbj5DbGljayBtZSE8L2J1dHRvbj4%3D)) website and copy-paste the code

So as you can see the hello function has variable a but the function hello doesn't have access to other variables like the variable b or c because they on another function but it does have access to variable d because it's on the global scope or environment

Similar is the case with variable b or c because they are both inside their respective functions and only have access to their variables and that's what lexical environment means

That's why I said to image each function that goes onto the call stack and an execution context is created and it has its planet as well and no one other the function itself can access that planets variables

![Lexical Environment](/assets/lexical-environment.png "Lexical Environment")

The same thing can be done with the functions as well we can define functions inside of each other and stuff like that which we are going to cover in the scope chain

So just remember that when we say lexical environment it just means where is that variable or function written in our code

## **Scope chain**

Let's see and learn about what scope chain is

What it does is that when the Js engine first parses through the code it just links functions and variables around it on where they are written

Now how it does that well depends majorly on where the function is defined so if the function is defined like this eg

```javascript
function hello(){
 console.log("hell")
}

function greet(){
 console.log("greet")
 hello()
}

function start(){
 console.log("starting greet")
 greet();
}
```

Now as you can see in this example the functions are defined on the main body of the program that means they are linked or their execution context is linked directly to the global execution context

So that means where ever if we define a variable in the global execution context every function will have the access to it

Every function is individually linked to the global execution context

But in this example

```javascript
function start(){
 console.log("hell")
 var a = "a";
 return function hello(){ 
 var b = "b";
 return function greet(){
  var c = "c";
    return "Ok";
 }
}
}

start() // this will invoke function hello()
start()() // this will invoke function greet()
start()()() // this will return Ok
```

As you can see in the above example we are defining the function one inside the another and that means the scope chains of the functions will be linked to each other, and that is the most important thing to understand in the scope chain

Here you can also understand each function as an individual planet

— So the bigger planet global has the planet start inside of it and the planet start will have hello inside of it and finally, we will have planet greet inside of it

Always remember that the planet greet which is inside of everybody will have access to every variable but no one has access to the variables of greet

For the planet hello it will have access to every variable except for greet's variable environment

For the planet start it will have access to the global variables but not the planet's inside of it

For more explanation:-

1. Let me explain how these functions are linked to each other - so the last function or the last child named greet( ) will have access to both var a and var b because they are their parent
2. Now for hello( ) it has access to var a but it doesn't have the connection with greet( ) which is variable c so if you try to console.log(c) then it will throw a reference error
3. For a start( ) it only has access to var its variable but not b or c and similarly it will give a reference error if we try to access those

But the common thing is that every function has access to the global scope and its variables

That's what scope chain is in Javascript

Before I leave here is an important difference between functional and block scope which I guess you should also know

Function scope and block scope

Initially, Js could only use function scoping as we have studied before and most of the other programming languages have block scoping

eg

```javascript
if(5>4){
 var secret = "555";
}

function secret(){
 var secret2 = "555";
}

//In javascript we can access the secret variable from here like outside of the if statement
//but we can't access secret2 and thats why Js is called function scoped


console.log(secret) // "555"
console.log(secret2) // reference error

// But in many other programming languages we can't access that the secret variable 
// because they are block scoped
```

But if we use let and const instead of var in the If statement then Js will also be able to use block scoping and we won't be able to access the variable secret from outside of the if statement

Well these are concepts and theory of execution context, lexical scope, and scope chain, I hope you enjoyed learning it and understanding the stuff

Was the article helpful? Do you have any doubts? Any topic you would like us to cover?

Reach out to us on [Twitter](https://twitter.com/aviatecoders) and [Instagram](https://instagram.com/aviatecoders) where we try to provide more value in threads and carousal formats

Thank You for your time

Keep learning, Keep coding :)

<!--EndFragment-->