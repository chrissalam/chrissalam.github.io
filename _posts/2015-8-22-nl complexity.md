---
layout: post
title: nl complexity
---

I wanted to start off by saying succinctly and firmly that I believe using regular expressions are often more time complex, certainly less intuitive, and often only effective for niche situations when it comes to solving coding challenges and interview questions... however, I am still fascinated with it!

A time complexity optimized solution will having the fewest amount of operations.
A space complexity optimized solution refers to have fewest amount of stored information.
RegExp solutions offer a chance at <a href="https://en.wikipedia.org/wiki/Computational_complexity_theory">computational complexity</a>, albeit an artificial kind. It's like fighting with an exotic weapon or wrestling left handed, the challenge is extra enticing.

The fourth, and most magical and completely illusionary goal is **"newline complexity"**, or **"/n complexity"** which is something I made up, to address the goal of every RegExp purist --> to solve the problem in as few lines as possible, *sans a minifier*, generally ignoring other complexities. The pursuit of the **regexp one-liner** as an answer is the ultimate prize.

Here are some short problem approaches which I would **never attempt during an interview...** but are presented here.

<center>**First Non-repeated Character**</center>

*"Write a function `f(a)` where a is a string that contains characters and the function returns the first character in the string that is not repeated anywhere else. If there are only repeated characters or no repeated characters return 'none'."*

```javascript
var firstNonRepeatedCharacter = function (string) {
  var i;
  for (i = 0; i < string.length; i++) {
    if (string.match(new RegExp(string[i], 'g')).length === 1) {
      return string[i];
    }
  } return "none";
};

//Test Suite
firstNonRepeatedCharacter = function('aabcc');
                  // --> 'b'
firstNonRepeatedCharacter = function('aabc');
                  // --> 'b'
firstNonRepeatedCharacter = function('aacc');
                  // --> 'none'
```

A simple iterative for loop solution would have addressed this within linear complexity. Save that mess for interviews... here we instead create a new RegExp within the for loop (a terrible performance no-no, of course), and then we run that regExp against the string. If we get exactly one solution, that's our answer!

<center>**Common Characters**</center>

*"Write a function `f(a, b)` which takes two strings as arguments and returns a string containing the characters found in both strings (without duplication), in the order that they appeared in `a`. Remember to skip spaces and characters you have already encountered! Extra credit: Extend your function to handle more than two input strings."*

```javascript
var commonCharacters = function (string1) {
  var string1Chars = {}, strNoDups = "", i, j;

  string1.split("").forEach(function (element) {
    string1Chars[element] = true;
  });

  for (i in string1Chars) { if (i) {strNoDups += i; } }

  for (j = 1; j < arguments.length; j++) {
    strNoDups = strNoDups.match(new RegExp('[' + arguments[j] + ']', 'g')).join("");
  }

  return strNoDups;
};

//Test Suite
console.log(commonCharacters('aceexivoue', 'aegihobue'));
                  // --> 'aeiou'
console.log(commonCharacters('aecexivou', 'aegihobu', 'aeefilou'));
                  // --> 'aeiou'
console.log(commonCharacters('dcba', 'abcd'));
                  // --> 'dcba'

```
First variables are declared. Next an involved step must be taken to remove the duplicates from the base case string. String1 may have duplicate characters in it, and we must travel through the string to remove them. I am not aware of a less newline complex regexp to solve this particular part of the problem, so I objectified the string and put it back together. After that, we RegExp each other string through the base case string to filter out what we want.

<center>**Longest Run**</center>

*"Write a function `f(a)` which takes one string as an argument and looks for the longest subset of repeated characters within the string and returns the index at which the run begins and ends. If two runs tie, please return the first."*

```javascript
var longestRun = function (string) {
  var max = 0, longRun;
  string.replace(/(\w+)\1+/g, function (set) {
    if (set.length > max) {
      max = set.length;
      longRun = set;
    } return set;
  });
  return (max === 0) ? [0, 0] :
  [ string.match('[' + longRun + ']').index,
    string.match('[' + longRun + ']').index + max - 1 ];
}

//Test Suite
console.log(longestRun("abbbc"));
                  // --> [ 1, 3 ]
console.log(longestRun("abc"));
                  // --> [ 0, 0 ]
console.log(longestRun("abbcc"));
                  // --> [ 1, 2 ]
```

JavaScript's replace function takes a callback. Here, I hijack the replace function, and add a max finder to it. You have to return the set or else you will modify the input string so I am searching for a more elegant way to do this without re-writing the exec or other javascript functions, as <a href="http://blog.magnetiq.com/post/2723860058/syntactic-sugar-rexexpexec-with-callbacks" >I've seen </a>. This way, each match get's processed rather than each iteration, and the match contains what I need to return the information. The ternary at the end is a little clumsy, here's an alternative method:

```javascript
  if (max === 0) {return [0, 0]; }
  else {
  var startIndex = string.match('[' + longRun + ']').index;
  return [startIndex, startIndex - 1 + max];
  }
```

Here's examples of some gnarly knotted solutions that try out new ideas and take extra time to get there. It's about the journey right? Unless you are actually working on the production solution...

**This is a stub, there's more coming**
