---
layout: post
title: inflection point where character count match
---

Here's a quick one. We commonly do iterations that lead to character counts. This one is looking for a moment where the left side and the right side have the same character count. In my interview, I quickly setup a for loop with a while loop inside it that found the counts, however this is way to algorithmly complex O(n^2). Of course then the interviewer asks for a better answer and left I'm scambling to find a better answer. I'll give you a clue in case you run into this, when the question wants you to compare one side of an array to another, that is a tell to try this with 2 for loops, one after the other. 2 non-nested for loops is O(2n) ~ which is the same as 0(n). When you do something that's 0(n^2), there might be a way you can do this with unnested loops, or nLog(n), or maybe use sorting.

```javascript
// Find all indices when leftside and rightside character counts are equal
s = 'raabaca'

// Leftside count at index 4: {'r':1,'a':2,'b':1}
// Rightside count at index 4: {'c':1,'a':2,'b':1}

```

Then let's find a way to keep track of these counts on the first pass and then build the comparison when you iterate backwards.

```javascript
s = 'raabacaf'
map = {}

for (let i of s) {
	map[i] = map[i] ? map[i] + 1 : 1
    // console.log(map)
    // -> {'r':1}
    // -> {'r':1,'a':1}
    // -> {'r':1,'a':2}
    // -> {'r':1,'a':2,'b':1}
    // -> {'r':1,'a':3,'b':1}.
    // -> etc
}
```

So obviously during my challenge I immediately started doing calculations on the match here. The best thing to do is to leave what you calculated. Looking at all this info, I saw when looking at this afterwards I was keeping track of too much.

```javascript
s = 'raabacaf'
counts = []
for (let i of s) {
	map[i] = map[i] ? map[i] + 1 : 1
    counts.push(Object.keys(map).length)
    // console.log(counts)
    // -> [1]
    // -> [1, 2]
    // -> [1, 2, 2]
    // -> [1, 2, 2, 3]
    // -> [1, 2, 2, 3 ,3]
    // -> etc
}
```

So this sets us up to look at this in reverse. The trick is how do we go in reverse? This is a little easier in python. In JS:

```javascript
s = 'raabacaf'
for (let i = s.length - 1; i >= 0; i--) {
    // console.log(i, s[i])
    // -> 7 f
    // -> 6 a
    // -> 5 c
    // -> etc
}
```

So this is good. Now we just need to keep track of character count again.

```javascript
s = 'raabacaf'

// -------------

map = {}
for (let i = s.length - 1; i >= 0; i--) {
	map[s[i]] = map[s[i]] ? map[s[i]] + 1 : 1
    counts.push(Object.keys(map).length)
    // console.log(map)
    // ->                   [1]
    // ->                [2, 1]
    // ->             [3, 2, 1]
    // ->          [3, 3, 2, 1]
    // ->       [4, 3, 3, 2, 1]
    // ->    [4, 4, 3, 2, 2, 1]
    // -> [4, 4, 4, 3, 2, 2, 1]
    // -> etc
}
```

I am showing this backwards to help visual this. This is also too much info. We don't need to keep track of these, we just need to compare them to the array we kept!

```javascript
count = 0

// -------------

map = {}
for (let i = s.length - 1; i >= 0; i--) {
		map[s[i]] = map[s[i]] ? map[s[i]] + 1 : 1
    if (Object.keys(map).length == counts[i - 1]) {
        // This is all the info we wanted!
    	count+=1
    }
}
```

We don't need detail on char counts, we don't need the letters themselves. Read that question and do as little work as possible. Leverage the limitations of the problem, because otherwise you will end up with too high a complexity, space or algorithmically, and / or you will run out of time. Here's it all together.

```javascript
s = 'raabacaf'
counts = []
count = 0
map = {}

for (let i of s) {
	map[i] = map[i] ? map[i] + 1 : 1
    counts.push(Object.keys(map).length)
}

// -> [1, 2, 2, 3, 3, 4, 4, 5]

map = {}
for (let i = s.length - 1; i >= 0; i--) {
		map[s[i]] = map[s[i]] ? map[s[i]] + 1 : 1
    if (Object.keys(map).length == counts[i - 1]) {
    	count+=1
    }
}

console.log(count) // -> 2
```

{:refdef: style="text-align: center;"}
![Sample King's Tours](/images/dsa/kingstour.png)
{: refdef}
