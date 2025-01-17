---
template: blog-post
title: Hoisting in Javascript
slug: /what-is-hoisting-in-javascript
date: 2021-04-08 22:22
description: Understand what is hoisting in Javascript with code examples, one
  of the most important topic in Javascript
featuredImage: /assets/hoisting-js-cover.png
---
<!--StartFragment-->

Hey guys,

It's soo good to see you here today I am going to explain an important topic of hoisting

It is kind of important as in it is asked in interviews and stuff like that so be better understand it

Now you might be having questions like "What is hoisting?", "What has it to do with my coding in JS?" and similar ones but don't worry we will understand each topic in detail

What is hoisting?

We know that the JS engine parses the program once before running the code ( see my previous article on how the JS engine works) and also we know that each program consists of variables and functions

But before I start explaining hoisting, let's see some code and understand what's going on

```javascript
console.log(greet) //----1

var greet= "Hi";

console.log(greet) //----2
```

If you read the lines of codes patiently before skipping to this line you will see that we have a

1.Console.log(greet)

So what do you think will be the output of the first console.log( ), well var greet is defined after the first console.log( )

— Well the answer is "undefined" but why you ask?

This is the concept of hoisting and in which as the JS engine parses through the code if it encounters the "var" word then it immediately stores the value of that particular variable in the memory heap but as undefined

And when it runs the code if it encounters something like console.log(greet) before even greet is defined then the stored value comes into the play and we get undefined which is the case with the first console.log( greet)

2.Console.log(greet)

Here if you have worked with decent JS you know that the output of the second console.log(greet) is "Hi" because till then the var greet is defined as "Hi" and the undefined is replaced with "Hi" in the memory heap

**Note: This is important that the partial hoisting only appears if the variables are declared using the "var" keyword, the JS engine only performs hoisting in case of the variable when there is a "var" keyword, it won't perform hoisting when the variables are declared using let or const**

Also in the case of variables, there is partial hoisting, why we say its partial hoisting, well after reading the full hoisting part you will understand it

Let's start with an example as always

```javascript
console.log(sing()) //----1

function sing(){
 console.log("uhh lalala")
}

console.log(sing())//----2
```

1.Console.log(sing( ))

Now you know that in the first console.log( ) there will be hoisting but this time its a function, so what will be the output of it

— Well the answer is "uhh lalala"

Are you surprised well don't be because this is what I was talking about when I said full hoisting because functions are fully hoisted

When the JS engine parses the code before running if it encounters the "function" word it directly stores the whole function into the memory heap unlike in the case of variables

2.Console.log(sing( ))

And this one is obvious the output of second console.log( sing( )) "uhh lalala" because it comes after the function is declared

You can remember it as "Function are fully hoisted and variables are partially hoisted"

But the important thing to remember in functions is that the function keyword in Js is important for it to get hoisted if we use function expression rather than function declaration it won't be hoisted

let's see what function declaration and function expressions are

```javascript
console.log(hello())---1
console.log(hi())---2
console.log(hi)---3

//Function declaration 
function hello(){
 console.log("greetings")
}

//Function expression
var hi = function(){
 console.log("casual")
}
console.log(hi())---4
```

1.Console.log( )

Now after reading everything if you understood some things you will be able to answer the first console.log( hello( ))

— Well the answer is "greetings"

This is Fully hoisting the function hello

2.Console.log( )

This one is a little tricky because the function hi is a function expression and a function expression starts with var but in the second console.log(hi( )) the function hi( ) is called inside the console.log( ) and if the function expression is called before it is declared then the answer will be

— "Typeerror"

That will throw an error because it doesn't think of it as a function at the second console.log( ), it thinks of it as a variable

3.Console.log( )

But in the third console.log( ) the JS engine know what "hi" and you guys also know what it is

— "undefined"

Alright, so here as I explained earlier if it encounters the "var" word it will keep it undefined even if it's a function

4.Console.log( )

And the last and fourth console.log( ), the function is already defined and declared so the output will be

— "casual"

As it is called after being defined it will show the output as casual

Now, I know that was a lot to take in but there are few things to know:

1.Things to remember are every time there is execution context there are two things a creation phase and execution phase where there is hoisting involved and it is for a very single function on the call stack. ( If you don't know about execution context please refer to this article)

2.Functions are fully hoisted and variables are partially hoisted

3.Variables defined with let and const are not at all hoisted

4.Function declarations are hoisted, function expression is not

These are the things you need to keep in mind while we are talking about hoisting and I hope you have understood the concept of hoisting and as you encounter questions regarding hoisting it will get a lot clearer

One very last thing, I have always been a supporter of writing code that other developers can understand easily but hoisting makes things complicated and so I try to avoid hoisting but it is a cool concept in Js, and understand the language you are learning doesn't harm so...

Reach out to us on [Twitter](https://twitter.com/aviatecoders) and [Instagram](https://instagram.com/aviatecoders) where we try to provide more value in threads and carousal formats

Keep learning, keep coding

Thank you

<!--EndFragment-->