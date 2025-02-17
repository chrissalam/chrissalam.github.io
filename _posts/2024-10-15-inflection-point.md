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
counts = []
count = 0
map = {}


for (let i of s) {
	map[i] = map[i] ? map[i] + 1 : 1
    //
}
```

```javascript
s = 'raabacaf'
counts = []
count = 0
map = {}


for (let i of s) {
	map[i] = map[i] ? map[i] + 1 : 1
    counts.push(Object.keys(map).length)
}

map = {}
for (let i = s.length - 1; i >= 0; i--) {
		map[s[i]] = map[s[i]] ? map[s[i]] + 1 : 1
    if (Object.keys(map).length == counts[i - 1]) {
    	count+=1
    }
}
```

{:refdef: style="text-align: center;"}
![Sample King's Tours](/images/dsa/kingstour.png)
{: refdef}
