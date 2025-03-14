---
layout: post
title: livecode bind
---

In my few weeks in Telegraph Academy, I've discovered I learn best from live coding and I want to bring some of that feel to my blog. <a href="https://en.wikipedia.org/wiki/Live_coding" target="_blank">Live coding</a> is a programming practice centered on the use of improvising interactive programming, there are live websites with many free, live tutorials and others simply challenging them to build something in a short period of time. <br /><br /> One reason I find them valuable is unlike slides, contrived exercises or doing the problem on your own, the live-coder puts on a show and gives me a chance to see an idea take shape. It also gives me confidence knowing that a quote-enquote professional programmer also makes typos, forgets keywords, and needs a moment to look at documentation. Finally, live coding also helps me establish patterns to look for and makes practical and succinct examples. <br /><br />For example, I have been struggling with the concept of **call**, **apply**, and **bind** and a live coding session in class went a long way towards demistifying it for me. Here's an expanded look at it! Open your console and try this out: <br />

```javascript
var alice = {teeth:"dirty"};
```
alice is a javaScript object with dirty teeth. She needs to up her dental hygiene game, and we've decided alice needs a native method to help her.

```javascript
alice.brush = function () {
  this.teeth = "clean";
  console.log("brushing...")
}
```
90% of the time **this** refers to the object to the left of the dot during the invocation of the function, meaning for us, alice.

```javascript
alice.brush()
       (1) brushing...
alice -->
			 Object {teeth: "clean"}
```
This will change the teeth property of the alice object. What if we wanted to change the condition of alice's teeth without using a native method? Let's bring in floss.

```javascript
floss = function () {
  this.teeth = "clean";
  console.log("flossing...")
}
```
Calling alice.floss() will not work!. Try it! Floss is not available to alice, and the **this** is not targeting alice, it has no logical target and instead targets the window, the global default value. We can use either the method **call** or **apply** to reset **this**, and make the function target the first argument of **call** or **apply** instead of the window. Assuming alice's teeth have been reverted to dirty:

```javascript
floss.call (alice) // or floss.apply (alice)
        (1) flossing
alice -->
        Object {teeth: "clean"}
```
There's more good things that happen with **call** and **apply**, they allow us to utilize additional arguments. **Call** lets us add our arguments as additional parameters. Here's an example using mouthwash:

```javascript
mouthwash = function (isCoolMint, isFresh) {
  this.teeth = (isCoolMint) ? "cool mint clean" : "clean"
  if (isFresh) { this.teeth = "so fresh and so clean"; }
}
mouthwash.call(alice, true); -->
			 Object {teeth: "cool mint clean"}
mouthwash.call(alice, false, true); -->
			 Object {teeth: "so fresh and so clean"}
```

**Call** lets us capture our arguments from the function and use them as parameters following the redirected **this**. **Apply** is a similar function that lets us capture the arguments of our function, but instead as an array. One method that always helps me is to remember that **(A)pply** helps you work with an (A)rray of arguments, and **(C)all** helps with arguments with (C)ommas.

```javascript
heavyDutyMouthwash = function() {
var howClean = ""
    for (var i in arguments) {
      console.log("swish"); // potency!
      howClean += (arguments[i]+" & ")
    }
  this.teeth = howClean + "clean";
}
```
 The arguments of a function is an array-like object which keeps track of all parameters passed in at call time. **Apply** will allow us to use each member of this array as arguments.

 ```javascript
 var neopolitan = ["fresh","mint","soft"]
 heavyDutyMouthwash.apply(alice,neopolitan) -->
        (3) swish
 alice -->
        Object {teeth: "fresh & mint & soft & clean"}
```

Using **call** on heavyDutyMouthwash would have processed the neopolitan array as a single array, being less effective at eliminating tooth decay and also forcing the array to a string and producing a different result:

 ```javascript
 var neopolitan = ["fresh","mint","soft"]
 heavyDutyMouthwash.call(alice,neopolitan) -->
        (1) swish
 alice -->
        Object {teeth: "fresh,mint,soft clean"}
```

**Bind** is the last of the **this** adjusting functions I'm going to talk about, it is certainly the most intimidating and most powerful. **Bind** delivers a new function that is ready to be called, and it's first argument also adjusts the **this**. I heard many times without really processing what that meant: we finally have a mechanism to make Alice's teeth be taken care of indefinitely! We will also use set interval, using the function made by **bind** and a time interval.

 ```javascript
alice.routineBrushing = function(){
  setInterval(this.brush,1000)
}
alice.routineBrushing() -->
     //Try this out and see what happens!
```
*this.brush* is a function definition that is waiting to be executed by
As cool as this is what about flossing? As someone who has had lots of maxillofacial work and cavities, I know this isn't enough. Let's get alice to floss consistently. See if you can do this without reading ahead.

 ```javascript
alice.routineFlossing = function(){
  setInterval(floss.bind(this),2000)
}
alice.routineFlossing() -->
     //Try this out and see what happens!
```

This line delivers a line of code that not only converts floss.bind(this) into an anonymous function ready to be invoked, it also adjusts this to take advantage of the floss method. Another way to picture the function is:

 ```javascript
alice.routineFlossing = function(){
  setInterval(function(){
    var fn = floss
    return function() {
      fn.apply(this, arguments)
    }
  }(),2000)
}
alice.routineFlossing() -->
```

This is not exactly what is happening to **bind** under the hood, take a close look at the **bind** prototype, but it is similar somewhat, but applied on the function and using this.

 ```javascript
Function.prototype.bind = function (scope) {
  var fn = this;

  return function () {
      return fn.apply(scope);
  };
}
```

 As a closing note, Live coding is something I find helpful and so do others: <a href="https://www.livecoding.tv/" target="_blank"> here is a link to a site focused on it. </a> **Call**, **apply**, and **bind** are hard especially if you are new to programming, but these three functions are powerful features I am excited to use and learn more about. It helped me to spend some time coding through this exercise and inventing new scenarios for alice and her dental woes and I hope it helps you.