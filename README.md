# LC-Python25
Backtracking 5

## 491.Non-decreasing Subsequences, 46.Permutations

June 26, 2023  4h

Congratulations!\
This is the 25th day for leetcode python study. Today we will learn more about the Backtracking!\
The challenges today are about how to use set to remove duplicates, and how to cut branch in the for loop. And only collecte the desired results in the backtracking function.~~need to delete later~~.


## 491.Non-decreasing Subsequences
[Reading link](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0491.%E9%80%92%E5%A2%9E%E5%AD%90%E5%BA%8F%E5%88%97.md)\
[video](https://www.bilibili.com/video/BV1EG4y1h78v/?spm_id_from=pageDriver&vd_source=63f26efad0d35bcbb0de794512ac21f3)\
[leetcode](https://leetcode.com/problems/non-decreasing-subsequences/)\
This is very similar but actually different from the subset II question, there are duplicates in the given array and we need to remove duplicates in the same tree layer. The difference is that we can't sort the given array beforehand, because this will change the original order. \
The subset questions don't need a termination condition. Because when the startIndex is larger than the numbers.size, the for loop will not be executed and will automatically end.
```python
# ways 1: use set to remove duplicates
class Solution:
    def findSubsequences(self, nums: List[int]) -> List[List[int]]:
        result = []
        path = []
        self.backtracking(nums, 0, path, result)
        return result

    def backtracking(self, nums, startIndex, path, result):
        if len(path) > 1:    #only collect desired results!
            result.append(path[:])
            #attention: no return here, just collect all nodes on the tree
        
        uset = set()    #use set to remove duplicate on the same tree layer
        for i in range(startIndex, len(nums)):
            if nums[i] in uset or (path and nums[i]<path[-1]):    #remove dup and cut branch, soo cool!
                continue    #branch cutting for 2 conditions
            
            uset.add(nums[i])   #record the element has been used in this tree layer
            path.append(nums[i])
            self.backtracking(nums, i+1, path, result)
            path.pop()
```


## 46.Permutations
So the permutation question is different from the conbination and subset questions, and don't need a startIndex because the order of the numbers matters. Here we use used array to mark which number has already been used. \
And all the results for possible permutations are in the leaf nodes. The termination condition is that the results size equals to the given numbers size.
```python
# ways 1: use set to remove duplicates, no startIndex!
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        result =[]
        self.backtracking(nums, [], [False]*len(nums), result)
        return result

    def backtracking(self, nums, path, used, result):
        if len(path)==len(nums):
            result.append(path[:])
            
        for i in range(len(nums)):
            if used[i]:
                continue
            used[i] = True
            path.append(nums[i])
            self.backtracking(nums, path, used, result)
            path.pop()
            used[i] = False
```


## 47.Permutations II
Need to remove duplicates on the same tree layer, while the duplicates on the tree depth is allowed. To remove duplicates and keep the same numbers together, we need to sort the given array first.\
used[i - 1] == true，used[i - 1] == false will both work.\
```python
# ways 1: 
class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        result = []
        self.backtracking(nums, [], [False]*len(nums), result)
        return result
    
    def backtracking(self, nums, path, used, result):
        if len(path)==len(nums):
            result.append(path[:])
        
        for i in range(len(nums)):
            if used[i] or (i>0 and nums[i]==nums[i-1] and not used[i-1]):
                continue
            used[i] = True
            path.append(nums[i])
            self.backtracking(nums, path, used, result)
            path.pop()
            used[i] =  False
```


