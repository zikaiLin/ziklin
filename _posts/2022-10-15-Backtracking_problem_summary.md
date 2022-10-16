---
editor_options: 
  markdown: 
    wrap: 72
layout: post
title: "Algorithms with Leetcode: Backtracking"
author: "Zikai Lin"
classes: wide 
categories:
  - leetcode
  - algorithms
tags:
  - Python
  - backtracking
  - algorithms

---

[TOC]



# Backtracking



## 78 Subsets

For each subset, we have every single element whether to include or not. And therefore we have $$2^n$$ possibilities. And therefore, if we use brutal force, the time complexity is too much.

``[1,2,3]``



![image-20221015211920191](/Volumes/easystore/Dropbox (Personal)/GithubPage/ziklin/assets/78subset.png)

*credit to Neetcode.io*



#### Breakdown



At each value of ``nums``,  we can divided into two possible cases:

- We want to add ``nums[i]`` into the result?  **Or**
- We DON'T want to add `nums[i]` into the result.



Therefore, as illustrated in the figure above, starting from the beginning of the array, at each `nums[i]`, we can expand it into two different subtrees (add vs not add). And at the end of the tree, i.e. the leaves, contains all possible subsets that we want to return.



To solve such problems, we can use Depth First Search (DFS), which is commonly used in binary tree structure. 



#### Conclusion

Remember that for backtracking problem, we always want to identify the sub-problems.

- What is the sub-problems: *include* vs *NOT include*
- Is a tree good enough for this type of problems? Yes
- DFS vs BFS? **DFS**



------



## 39 Combination Sum

#### Problem description

https://leetcode.com/problems/combination-sum/

Given an array of **distinct** integers `candidates` and a target integer `target`, return *a list of all **unique combinations** of* `candidates` *where the chosen numbers sum to* `target`*.* You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

The test cases are generated such that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.



**Example 1:**

```
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.
```

**Example 2:**

```
Input: candidates = [2,3,5], target = 8
Output: [[2,2,2,2],[2,3,3],[3,5]]
```

**Example 3:**

```
Input: candidates = [2], target = 1
Output: []
```



#### Breakdown



Does brutal force works here? Probably no, because each number can be picked out for **unlimited** number of times. 



So here what is the decision tree?

- For each node (each number in the array), expand the whole possible choices as the children.



At each level of the decision tree, how do we determine that if we can move forward or keep searching?

- If the path sum is greater than the target, we don't have to keep searching because all the values in the array are **positive**



#### Python solution

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        
        res = []
        
        subsum = 0
        subset = []
        
        def dfs(i, target, subsum):
            nonlocal res
            if subsum == target:
                res.append(subset.copy())
                return None
            
            if i >= len(candidates) or subsum > target:
                return None
            
            subset.append(candidates[i])
            dfs(i, target, subsum + candidates[i])
            
            subset.pop()
            dfs(i+1, target, subsum)
            
        dfs(0, target, 0)
        
        return res
```


​            
​            
​        