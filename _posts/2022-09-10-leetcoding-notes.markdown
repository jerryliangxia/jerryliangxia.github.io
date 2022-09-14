---
layout: "post"
title: "Leetcoding Notes"
date: 2022-09-10 11:19:00 -0400
categories: jekyll work
permalink: "/:title"
---

Good questions to start with:

- Shuffle String
- Check if two String Arrays are Equivalent
- Count Items Matching a Rule
- Contains Duplicate
- TwoSum
- Move Zeroes, Remove Duplicates
- Reverse Integer, Palindrome Number
- Rotate Array
- First Bad Version
- Search Insert Position
- Search in Rotated Sorted Array
- First and Last Position of Element in Sorted Array
- Find Minimum in Rotated Sorted Array

Small Tips

- If you are using the first element of the array, remember to extract from the list starting at the 1-indexed element
- If you are using a table for DP, make the DP table the same length as the input array

<h3>General useful notes</h3>

```python
# Using a global variable and helper function
class Solution(object):
    def main(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        global out
        out = 0

        def helper(root):
            global out

            if not root:
                return 0
            left = valueSum(root.left)
            right = valueSum(root.right)
            tilt = abs(left - right)
            out += tilt
            return left + right + root.val

        helper(root)
        return out

d[num] = d.get(num, 0) + 1
l.insert(0, num)
float('inf'), float('-inf')
```

Arrays:

```python
# Convert list to string
new_string = ''.join(map(str, list))

# Basic reverse iteration
for i in range(len(nums)):
    cur = digits[len(digits)-i-1]

# Parsing an array from an index
new_arr = arr[1:]

# same goes for strings... (more parsing)
new_str = str[start:end]
remove_three_from_end = str[:len(str)-3]
remove_one_from_start = str[1:]

# flatten a list using list comprehension (can be used multiple times)
flat_list = [item for sublist in l for item in sublist]
# is the same as ...
flat_list = []
for sublist in l:
    for item in sublist:
        flat_list.append(item)
```

Dicts:

```python
# Again, using list comprehension
new_list = [[k, v] for k,v in dict.items()]

# Sorting - based on values
dict_sorted_based_on_values = dict(sorted(d.items(), key=lambda item:item[1]))
# Sorting based on keys is simple
dict_sorted_based_on_keys = sorted(d)
# sort by keys and reverse
keys = sorted(dict.keys(), reverse=True)
```

<h3>Leetcode question-specific notes</h3>

<h4>Reversing integers:</h4>

```python
# Always have a running sum
runningSum = 0
while x != 0:
    runningSum = runningSum * 10 + x % 10
    x /= 10

# Another way (checking integer palindrome)
halfReversedInteger = 0
while x > halfReversedInteger:
    halfReversedInteger = halfReversedInteger * 10 + x / 10
    x /= 10
return halfReversedInteger == x or halfReversedInteger == x / 10
```

Example Leetcode problem [(Plus One)](https://leetcode.com/problems/plus-one/)

```python
# Adding into an array
def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]

        cur = digits[len(digits)-i-1]
        """
        carry = 1
        for i in range(len(digits)):
            if carry == 0:
                break
            cur = digits[len(digits)-i-1]
            cur += carry
            carry = cur/10
            cur %= 10
            digits[len(digits)-i-1] = cur
        if carry == 1:
            digits.insert(0, 1)
        return digits
```

<h4>Binary Search</h4>

Basic algorithm:

```python
# This searches for an index where a target lies
l, r = 0, len(nums)-1
while l <= r:
    mid = (l + r)/2
    if nums[mid] == target:
        return mid
    if nums[mid] < target:
        mid = l + 1
    else:
        mid = r - 1
return l
```

For iterating through an array whilst swapping elements:

```python
'''
have a slow and fast pointer
slow will always point to the index to be swapped, and increment only when needed
otherwise, i will continue to move forward
if i and j point to the same spot (if the list thus far is already fine), then it will
stay the same
'''
j = 0
for i, a in enumerate(nums):
    if nums[i] != val:
        nums[i], nums[j] = nums[j], nums[i]
        j += 1
return j
```

<h4>Search in a binary tree</h4>

```python
def searchBST(self, root, val):
    """
    :type root: TreeNode
    :type val: int
    :rtype: TreeNode
    """
    if not root:
        return None
    if root.val == val:
        return root
    elif root.val > val:
        return self.searchBST(root.left, val)
    else:
        return self.searchBST(root.right, val)
```

<h4>BFS in a Binary Tree</h4>

Example question: Finding the [mode](https://leetcode.com/problems/find-mode-in-binary-search-tree/) with a dictionary:

```python
def findMode(self, root):
    """
    :type root: TreeNode
    :rtype: List[int]
    """
    d = {}
    if not root:
        return []
    q = [root]
    maxCount = 0
    while q:
        size = len(q)
        for i in range(size):
            node = q.pop(0)
            d[node.val] = d.get(node.val, 0) + 1
            maxCount = max(maxCount, d[node.val])
            if node.left:
                q.append(node.left)
            if node.right:
                q.append(node.right)
    out = []
    for k, v in d.items():
        if v == maxCount:
            out.append(k)
    return out
```

<h4>DFS in a Binary Tree</h4>

[Basic depth question](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

```python
def maxDepth(self, root):
    """
    :type root: TreeNode
    :rtype: int

    using dfs
    """
    def helper(root, count):
        if not root:
            return 0
        left = helper(root.left, count) + 1
        right = helper(root.right, count) + 1
        return max(left, right)

    return helper(root, 0)
```

... more to come later!
