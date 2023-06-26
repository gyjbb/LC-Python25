# LC-Python25
Backtracking 5

## 491.Non-decreasing Subsequences, 

June 26, 2023  4h

Congratulations!\
This is the 25th day for leetcode python study. Today we will learn more about the Backtracking!\
The challenges today are about ~~need to delete later~~.


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
        if len(path) > 1:
            result.append(path[:])
            #attention: no return here, just collect all nodes on the tree
        
        uset = set()    #use set to remove duplicate on the same tree layer
        for i in range(startIndex, len(nums)):
            if nums[i] in uset or (path and nums[i]<path[-1]):
                continue    #branch cutting for 2 conditions
            
            uset.add(nums[i])   #record the element has been used in this tree layer
            path.append(nums[i])
            self.backtracking(nums, i+1, path, result)
            path.pop()
```


## 46.
全排列 本题重点感受一下，排列问题 与 组合问题，组合总和，子集问题的区别。 为什么排列问题不用 startIndex 


## 47.
全排列 II 本题 就是我们讲过的 40.组合总和II 去重逻辑 和 46.全排列 的结合，可以先自己做一下，然后重点看一下 文章中 我讲的拓展内容。 used[i - 1] == true 也行，used[i - 1] == false 也行 

