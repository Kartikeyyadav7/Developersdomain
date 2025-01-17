---
template: blog-post
title: Call, Bind and Apply In Javascript
slug: /what-is-call-bind-apply-in-javascript
date: 2021-04-10 08:48
description: Many developers get confused or don't understand the basics of
  call, bind, and apply, in this article, you will understand everything related
  to call, bind and apply
featuredImage: /assets/callbindapply-cover.png
---
Hey guys,

So you might have heard about these famous methods especially the bind method as it used so much, so let's try and understand about these

## Call and Apply

```javascript
function greeting(){
  console.log("hello")
}
greeting() // hello
greeting.call() //hello
greeting.apply() //hello
```

This is a very simple code that I have written, it's just a function named greeting but at the end, you might realize something you could have not seen before, I am not talking about the normal function call greeting but when we use call and apply

As you see from the code snippet that I have also written the output of the function call so the first that we regularly use is the normal function call and it outputs hello but the next is also a function call which we use doing the call method and it gives the same output as hello and lastly using apply method we also get the same output

Well underneath the hood JS uses .call() method where a function is invoked that means greeting.call() is always used and greeting() is just the shortcut way to write that
And when we use apply it gives the same result

We have seen the result of using call and apply but now let's see how they can be useful

```javascript
const student1 = {
	name: "Harry",
	percent:60,
	increment(){
		 return this.percent = 100
	}
}
student1.increment()
```

What I have done here is I have defined an object named student1 and given name and percent and also an increment method to it so that the percent can be incremented whenever the method is called( if you don't know about the "this" keyword please refer to [this](https://www.aviatecoders.com/how-this-keyword-works-in-javascript)[ ](https://developersdomain.netlify.app/how-this-keyword-works-in-javascript)article)

Now what I want to do is used use increment method of the student1 and use it for another object named student2

```javascript
const student1 = {
	name: "Harry",
	percent:60,
	increment(){
		 return this.percent = 100
	}
}

const student2 = {
	name:"Marry",
	percent:30
}

student1.increment()
student1.increment.call(student2) 
```

If you run this code in your editor, you will find out that the percent of student2 has increased to 100 and that is the benefit of using the call function is that we don't have to repeat the method in every object that needs it and helps in writing DRY code

Also, the call method can accept parameters like so

```javascript
const student1 = {
	name: "Harry",
	percent:60,
	increment(num1, num2){
		 return this.percent += num1 + num2
	}
}

const student2 = {
	name:"Marry",
	percent:30
}

student1.increment(10,20)
console.log(student1.percent) //90
console.log(student2.percent) //30
student1.increment.call(student2, 20,50)
console.log(student2.percent) //100
```

And the output will be 100 for student2 and 30 for student1

Now we know what call does and now let's see what apply does differently from the same example

```javascript
const student1 = {
	name: "Harry",
	percent:60,
	increment(num1, num2){
		 return this.percent += num1 + num
	}
}

const student2 = {
	name:"Marry",
	percent:30
}

student1.increment(10,20) //90
console.log(student2.percent) //30
student1.increment.apply(student2, [20,50])
console.log(student2.percent) //100
```

Well apply doesn't do anything much different it just changes the way we pass argument using apply we pass arguments through an array but it returns the same result

Now if you want to choose whether to use call or apply it depends on how to want to pass the arguments, if you want to pass them as an array then use apply, if you want to pass normally use call

Also as you can see from the above example the method increment has the "this" keyword which helps us to use it in other objects as well, if a method doesn't have that can't use it

## Bind method

Moving on to the bind part and what it does let's see

Well unlike call and apply which instantly give the output, bind on the other hand return a function

```javascript
const student1 = {
	name: "Harry",
	percent:60,
	increment(num1, num2){
		 return this.percent += num1 + num2
	}
}

const student2 = {
	name:"Marry",
	percent:30
}

student1.increment(10,20) //90
console.log(student2.percent) //30
const incrementedStudent2 = student1.increment.bind(student2, 20,50)
incrementedStudent2()
console.log(student2.percent) //100
```

So bind helps us to store the borrowed method for later use in form of a new function

You might have seen the bind method being used for the 'this' keyword, which is a common thing that bind method is used for

Let me explain the bind method passes the "this" keyword which refers to a certain object as an argument to itself, it's like storing the "this" keyword for later use and returning a function

```javascript
const singer = {
  name:"Joy",
  sing(){
    console.log("1", this)
    var singAgain = function() {
		console.log("2", this)
  }
  return singAgain.bind(this)
  }
}

singer.sing()()
```

This is an example that I used while explaining the "this" keyword

So in this, as you can see I have used the bind method to store or bind the "this" keyword which refers to the object singer because if you see carefully it is not inside the function singAgain( ) it's inside the sing function where the "this" keyword still refers to the object singer

Now as we know that the bind function stores the value for later use and binds it to the particular function it is attached to and then returns a function

If you run this code inside the console you will see that both the first console.log and second refer to the same object which is the singer object

And if any of you are wondering why is singer.sing()() is called twice well because if you only do like singer.sing() then it just returns the singAgain function it doesn't invoke it, so to invoke we have to again call it

Was the article helpful? Do you have any doubts? Any topic you would like us to cover?

Reach out to us on [](https://twitter.com/kartikey_yadav7)[Twitter](https://twitter.com/aviatecoders) and [Instagram](https://instagram.com/aviatecoders) where we try to provide more value in threads and carousal formats

Thank You for your time

Keep learning, Keep coding :)

<!--EndFragment-->