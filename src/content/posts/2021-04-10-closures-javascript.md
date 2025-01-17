---
template: blog-post
title: Closures | Javascript
slug: /what-is-closures-in-javascript
date: 2021-04-10 09:16
description: Learn about the famous closures and understand Javascript on an
  even deeper level here with examples and advantages of closures
featuredImage: /assets/closures-cover.png
---
<!--StartFragment-->

Closures is an important topic when it comes to JS and it has become so popular that even other big programming languages are adopting the same

To understand closure we first need to have a good knowledge of functions and lexical scoping because closure is dependent on that

You might be using closures without even knowing about it so let's see what closures are why it is such a cool and amazing concept in JS

To start I will explain about functions and higher-order functions so if you already know about it you can directly go to the closure part

Let's start by revising what we know about functions

We know how to call functions

1. Normally calling a function

   ```javascript
   function hello(){
   	console.log("hi)
   }
   hello()
   ```
2. Calling with an object

   ```javascript
   const obj = {
   	name:"Jett",
   	speed(){
   		console.log("Woos")
   	}
   }
   obj.speed()
   ```
3. Using the call method

   ```javascript
   function hello(){
   	console.log("hi)
   }
   hello.call()
   ```
4. We can also use "new" operator

   ```javascript
   const four = new Function("num", "return num")

   four(4)
   ```

We know that whenever a function is called or invoked it creates an execution context and that execution context consists of the "this" keyword, the "arguments" keyword, and finally the variable environment

> ***Functions are a special type of object which are called callable objects in JS***

Why you ask, well we can back that claim up because if you imagine a box with the name of the function and some code and three properties - call, apply and bind

![Function](/assets/functions-are-objects.png "Inside of the function")

If you now go to your text editor and type a function and then see by the intelligence you will see something like this

![Functions are objects](/assets/function.png "Functions are objects")

It will give you the options or the methods that you can use with the function itself so that means it behaves like an object

Now how does this concern us, well if functions are objects then we can store them around like objects, move them and pass them to another function

> ***Functions are first-class citizens in JS***

What does that mean well three things back that claim

1.We can store a function into a variable

```javascript
var greet = function(){}
```

2.We can pass a function as an argument to another function

```javascript
function greet(fn){
	fn()
}
greet(function(){console.log("hello")})
```

3. We can also return a function

```javascript
function greet(){
	return function(){ console.log("Hi there")}
}

greet()()
```

So basically what I am trying to say is function can do pretty much everything other data types can do in JS

### Higher-Order Functions (HOF)

A HOF is a function that can return a function or a function that can take function for an arguments as you have seen from the above examples

And we also know about the lexical scoping in JS and if you don't then you can refer to [](https://developersdomain.netlify.app/execution-context-lexical-environmenet-scope-chain)[this](https://www.aviatecoders.com/execution-context-lexical-environmenet-scope-chain) article but in short, let me tell you

Lexical scoping or static scoping means the available variable data and functions are dependent on where the function is defined

## Closures

Now finally to explain Closures let's start with an example

```javascript
function hello(){
  console.log("greetings")
  var a = "hi"
  return function b(){
    var b = "hi there"
    return function c(){
      var c = "hello there"
      return `${a} ${b} ${c}`
    }
  }
}

hello()()() // hi hi there hello there
```

Now what has happened here, well I wrote the function hello and then declared a variable and returned another function which indeed returns another function, and finally, I accessed all the variables at the end and returned it

Well as you guys know that when function hello is called it is pushed onto the stack and after it returns another function it gets popped off the stack (and if a function gets popped off the stack then their variable environment gets destroyed) then function b comes onto the stack return a function and again pops off the stack

Finally, function c comes and return all the variables that were defined while in function hello and b

But didn't I just said that those functions were popped off the stack and but then too we somehow have access to their variable

And this concept of accessing the variables even if the function is popped off the stack which returning a function is called closure

What happens is the first time when the JS engine parses the code it sees that the variables are mentioned even inside the function which is being returned and so because of that it just stores the variable into a contained called closure and when the function is being called then when the JS engine gets its value from the closure box and puts it in and runs it

This is one of the coolest parts of JS and it can have many uses such they can be memory efficient and use encapsulation

### Memory efficient

```javascript
function work(index){
	const arr = new Array(7000).fill(":)") // create new array with 7000 elements of :)
	console.log("created")
	return arr[index]
}

work(55) // created
work(99) //created
work(800) // created :)
```

Here we have created a function that creates a new Array of 7000 elements with ":)" and finally return it will give index well this process takes time if we call it again and again and is not very memory efficient

What we can do instead is

```javascript
function work(index){
	const arr = new Array(7000).fill(":)") // create new array with 7000 elements of :)
	console.log("created")
	return function (){
			return arr[index]
	}
}

const workHard = work()
workHard()
workHard()
workHard() 
// created :)
```

Here even if we call the workHard function many times it will give only one output and that saves a lot of time and memory instead of creating an array every single time on invocation

### Encapsulation

Also with the help of closure, we can use encapsulation which means is a process of bundling the data (i.e. variables) with the functions acting on that data as you have seen in the previous examples

Was the article helpful? Do you have any doubts? Any topic you would like us to cover?

Reach out to us on [](https://twitter.com/kartikey_yadav7)[Twitter](https://twitter.com/aviatecoders) and [Instagram](https://instagram.com/aviatecoders) where we try to provide more value in threads and carousal formats

Thank You for your time

Keep learning, Keep coding :)

<!--EndFragment-->