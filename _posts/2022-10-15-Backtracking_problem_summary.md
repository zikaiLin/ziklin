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



![image-20221015211920191](/Volumes/easystore/Dropbox (Personal)/GithubPage/ziklin/images/78subset.png)

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



## 90. Subsets II

#### Problem Description



Given an integer array `nums` that may contain duplicates, return *all possible subsets (the power set)*.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

 

**Example 1:**

```
Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]
```

**Example 2:**

```
Input: nums = [0]
Output: [[],[0]]
```

 

**Constraints:**

- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`





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



*So here what is the decision tree?*

- For each node (each number in the array), expand the whole possible choices as the children.



*(Stoppign rule) At each level of the decision tree, how do we determine that if we can move forward or keep searching?*

- If the path sum is **greater or equal** than the target, we don't have to keep searching because all the values in the array are **positive**



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

 

## 40. Combination Sum II



Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sum to `target`.

Each number in `candidates` may only be used **once** in the combination.

**Note:** The solution set must not contain duplicate combinations.

 

**Example 1:**

```
Input: candidates = [10,1,2,7,6,1,5], target = 8
Output: 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]
```

**Example 2:**

```
Input: candidates = [2,5,2,1,2], target = 5
Output: 
[
[1,2,2],
[5]
]
```

 

**Constraints:**

- `1 <= candidates.length <= 100`
- `1 <= candidates[i] <= 50`
- `1 <= target <= 30`



#### Breakdown

Still, we need to think about what the decision tree is. 



Using the example as an illustration:

```
candidates = [10,1,2,7,6,1,5]
```

After being sorted: candidates = [1,1,2,5,6,7,10]



- Include 1 vs not include 1:
  - Include 1 -> create a subproblem where arr =  [1,1,2,5,6,7,10], target = 8-1 = 7
  - Not include 1 -> Then we have to **make sure that the **



#### Code


        
```python
class Solution:
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        candidates.sort()
        
        res = []
        cur = []
        def backtrack(cur, pos, target):
            if target == 0:
                # basecase, find a path
                res.append(cur.copy())
            if target <= 0:
                # Stop tracking
                return
            
            
            prev = -1
            for i in range(pos, len(candidates)):
                # Case 2: skip candidates[i]
                if candidates[i] == prev:
                    continue
                
                # Case 2: include candidates[i]
                cur.append(candidates[i])
                backtrack(cur, i+1, target - candidates[i])
                cur.pop() # cleanup
                
                # record prev
                prev = candidates[i]
        backtrack([], 0, target)
        return res
                
                
                
                
```


​            



## 77. Combinations









## 46. Permutations

Given an array `nums` of distinct integers, return *all the possible permutations*. You can return the answer in **any order**.

 

**Example 1:**

```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

**Example 2:**

```
Input: nums = [0,1]
Output: [[0,1],[1,0]]
```

**Example 3:**

```
Input: nums = [1]
Output: [[1]]
```

 

**Constraints:**

- `1 <= nums.length <= 6`
- `-10 <= nums[i] <= 10`
- All the integers of `nums` are **unique**.



#### Breakdown

*How many possible results exists for permutation?*

- $$\mathrm{Permute}(n) = n!$$



*What does the decision tree look like? (suppose we are using the example)* 

1. We pop one number out of `[1,2,3]`:
   -  `[1,2,3]`  -> `[2,3] + [1]` 
     -  `[2,3]`  -> `[3] + [2]` 
     -  `[2,3]`  -> `[2] + [3]` 
   - `[1,2,3]`  -> `[1,3] + [2]` 
     -  `[1,3]`  -> `[1] + [3]` 
     -  `[1,3]`  -> `[3] + [1]` 
   - `[1,2,3]`  -> `[1,2] + [3]` 
     -  `[1,2]`  -> `[1] + [2]` 
     -  `[1，2]`  -> `[2] + [1]` 
2. The backtracking problem can therefore be described as:
   - Each time, we pop one number out (from 1 to n)
   - Run a DFS and sub-divide the array into all possible orders
   - After the DFS, we append the number we popped out to it



#### Solution:

Credit to *Neetcode.io* 

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        result = []
        
        if (len(nums) == 1):
            return [nums.copy()]
        
        for i in range(len(nums)):
            n = nums.pop(0)
            perms = self.permute(nums)
            
            for perm in perms:
                perm.append(n)
            result.extend(perms)
            nums.append(n)
                
        
        return result
            
```







- 