---
layout: post
title: longest common prefix
---

This question seems very easy: find the longest common prefix between a set of words.

```python
strings = ["blast","blow","black"]

# -> "bl"
```

my first approach at this was from the front, i.e. i = 0 and climbing. This is tricky because not all the strings have the same length. Therefore, take a portion from the whole and reduce from that full length. Lots of these iteration problems will either be measure all against a separate variable, or selection on from within. In this case, we should look at strings[0] and compare to strings[1:] (the rest)

```python
prefix = strings[0]

for string in strings[1:]:
        #....
```
Why this works is because we can compare prefix to string, and we will never look where an index does not exist, i.e. index 4 on blow. Some solutions split the concept of prefix and prefix length into two variables, but if you can decrement prefix. i.e. 

```python
prefix = prefix[:-1]

# vs

prefix_length -= 1
prefix = prefix[0:prefix_length]
```
You can save a line and be more idiomatic. Even through I said I hate the syntax it is more space efficient. The other keys are iterating through strings but also using a while loop to check each prefix versus the string

```python
prefix = strings[0]

for string in strings[1:]:
        # condition
                prefix = prefix[:-1]
return prefix
```

So what is the condition? To compare prefix to string[0:prefix_length], we can just take prefix and match length. The for loop will keep decrementing immediately from "blast" to "blas" to "bla" to "bl", possibly hitting "bla" in "black" but then in the next iteration skipping to "bl" as "blo" from "blow" will be modified by the while. The best part of this is looking at an index greater that what is present will still output the full string and not fail (index out of error). So it's: 

```python
def longestCommonPrefix(strings: list[str]) -> str:
        prefix = strings[0]

        for string in strings[1:]:
                while prefix != string[0:len(prefix)]:
                        prefix = prefix[:-1]
        return prefix
```

