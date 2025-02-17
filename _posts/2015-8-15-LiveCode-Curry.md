---
layout: post
title: LiveCode Curry
---

Tonight, I watched Cassandra's talk on functional programming, and I got pretty excited about currying, composing, and piping functions. I wanted to live code some practical examples, as I must admit it took seeing this several times for me to really wrap my head around this topic and I hope this helps!

I would recommend going to Ramda.js's website and pulling up a console there. Another option would be to npm install ramda and try these functions there. If you use sublime and do not have a JS build system, try this link from my classmate <a href="http://jdlawrence.github.io/javascript/closures/2015/08/03/console-inside-sublime-text.html">Jamil</a>. You can also grab it from CDN via

```html
<script src="//cdnjs.cloudflare.com/ajax/libs/ramda/0.17.1/ramda.min.js"></script>
```
<!-- Currying is a transformation you can do to allow functions to take their some of their arguments at different times. Currying lets us partially fill the functions and keep them in position for later.

```javascript
function area(height, width) { return height * width; }
var curryArea = R.curry(area);

curryArea(2);    // [function]
curryArea(2)(5); // 10

```
Why is this useful?

```javascript
function that invokes
var lines = R.invoker(1, 'split')('/n');
var split = R.split('/n');
```
var getItems = R.compose(
  R.filter(R.propEq('eventType',"ITEM_DESTROYED")),
  R.flatten,
  R.map(R.prop('events'))
)
-->

<a href="http://alicekamada.github.io/" >"Pointfree Code is code that never refers to the code it handles:
it focuses on the logic, easier to reason about, and never have to wonder about the state."</a>

This isn't exactly related but another helpful trick I've learned after doing alot of data transforms in the console is to save the data object or array as a global variable and then to copy the temporary variable.

```javascript
/*in console*/
Data Object = {...}; 
            // right click on the edge of the Object
            // store as a temporary variable
            // creates 'temp1'
copy(temp1) // and this is available for 
            // pasting in text editor.
```

**This is a stub... there's more to come**

<!-- Anyways, we had a toy problem earlier in the program that asked us to write the functions for piping and composing functions. A pipe function asked us to create a function such that

```javascript
var newfunc =  R.pipe(func1, func2, func3)
```

where the newfunc(args_provided_to_function_one) =  -->

