---
layout: post
title: Longest substring without repeating characters
---

This is one of those questions where you can overlook edgecases immediately if you opt for a purely linear approach. If it seems easy, in this case it's like leetcode medium, maybe it's actually harder. I've done this one and immediately gotten the first three test cases to pass, and then the zeroth case (string = '') isn't handled. That should actually clue you in to the face that you are probably missing other cases as well. In my case, I was missing the case of `abcadef`, i.e. I found `abc`, and restarted and found `adef`, missing `bcadef`. This is a signal to consider while looping through a sliding window approach, rather than a linear approach. Additionally you can probably get by with a dictionary in python but I think a set is the best way to document substring uniqueness. 

```

```

WIP