# Backtracking problem summary



## 78 Subsets

For each subset, we have every single element whether to include or not. And therefore we have $$2^n$$ possibilities. And therefore, if we use brutal force, the time complexity is too much.

``[1,2,3]``



![image-20221015211920191](/Volumes/easystore/Dropbox (Personal)/LeetCode刷题/Backtrack/78subset.png)

*credit to Neetcode.io*

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









