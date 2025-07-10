---
layout: post
title: Kth largest element in an array
---

This is one of those questions where you can immediately tell there are many "expensive" ways to do this. 

Obviously if you sort the array and then iterate to the kth element, you have an nlogn solution.

```python
def findKthLargest(self, nums: List[int], k: int) -> int:
        nums.sort(reverse=True)
        return nums[k - 1]
```

Alternatively, I don't think there seems to be an obvious way to do this logn, skipping the sorting or iterating all the way across step. So the solution must be linear.

Additionally, you probably need an additional data structure but we can inately feel the inadequacy of an object or an additional array to do this. This is a scenario for a minimum heap, which is built into python. What is that? In ten years of coding I've never used this at work, so it's time to google. Here's the question:

## Given an integer array nums and an integer k, return the kth largest element in the array.
## Note that it is the kth largest element in the sorted order, not the kth distinct element.\
## Can you solve it without sorting?

So to solve without sorting, we must iterate through and create a data structure that updates itself and can removes values below the minumum and keeps values that are at k threshold or higher. Our heapq which is a minimum queue by default, does that, and we discard the values we don't need. The root of the tree (or the top of the heap?) is heap[0]. Any other solution would be less efficient because the data structure itself does the sorting needed to do this problem.

```python
import heapq

def findKthLargest(self, nums: List[int], k: int) -> int:
        
        return ???
```

Yep. This is going to get gnarly. Having transitioned from javascript to python in terms of my coding challenges the level of importing that's required to answer most questions have gone up tremendously. A recent interview said "you can tell who is deep in python because they import numpy before even starting the question..."

Heapq is a minimum heap by default. heapq.heappop will remove values and create the new below k minimum we need at the root of our data structure (top of heap or root of tree), and heapq.heappush will help us bring in new values and place them at the appropriate layer. we will also still have to iterate through the list.

```python
import heapq

def findKthLargest(self, nums: List[int], k: int) -> int:
        heap = []
        for num in nums:
        # whoa....

        return heap[0]
```

heaps are initialized with []. So our logic is sort stuff in the heap and then trim the heap.

```python
import heapq

def findKthLargest(self, nums: List[int], k: int) -> int:
        heap = []
        for num in nums:
                # sort stuff in the heap
                heapq.heappush(heap, num)
                # trim the heap
                if len(heap) > k:
                        heapq.heappop(heap)

        return heap[0]
```

You can of course do a bit more here, you can make the if a while, you can also take the full list and heapify it and then just return k but I think that's higher complexity, this is a linear pass, so it's O(n) complexity. It also just keeps track of a heap that's k sized so it's probably more efficient as well, as heapify and other solutions would do work on sorting you probably don't need.