# Algorithm Notes
Algorithm Q/A from Leetcode / Hackerrank

## Two Sum
#### Q: Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:
```text
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

#### Hint 1:
A really brute force way would be to search for all possible pairs of numbers but that would be too slow. Again, it's best to try out brute force solutions for just for completeness. It is from these brute force solutions that you can come up with optimizations.

#### Hint 2:
So, if we fix one of the numbers, say x, we have to scan the entire array to find the next number y which is value - x where value is the input parameter. Can we change our array somehow so that this search becomes faster?

#### Hint 3:
The second train of thought is, without changing the array, can we use additional space somehow? Like maybe a hash map to speed up the search?

#### Answer 1 (Brute force):
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
      for i in range(len(nums)):
        for j in range(i+1,len(nums)):
          pair_sum = num[i] + num[j]

          # check condition
          if pair_sum == target:
            return [i,j]

```

#### Explanation:
If we can sum two numbers that are adjacent to each other from the left end to the right end of the array, we can find two numbers that sum up to the target eventually.
1. First we want to loop through the array and pick a number, which could be done by the first for loop.
2. We then pick the number that is to the right side of the first number we picked in step 1. This is done by the second for loop.
  - It is important to note that to pick the number that is on the right of the first picked number, we do the following:
  ```python
  # add 1 to the beginning of the index
  for j in range(i+1,len(nums))
  ```
3. We add the two numbers that were picked and check if they match the target value. If it is a match, return the respective indexes in a list, i.e. `[i,j]`.

Note the run time for this solution is `O(n^2)`.

#### Answer 2 (Dictionary/ Hashmap method):
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # False if length of array <= 1
        if len(nums) <= 1:
            return False

        dic = {}
        for i in range(len(nums)):
            if nums[i] in dic:
                return [dic[nums[i]], i]
            else:
                dic[target - nums[i]] = i
```

#### Explanation
We will store complements as the key in the dictionary. Then we will check whether an element in `nums` is in one of the key values in the dictionary. If so, we will return the value of the dictionary and the index.
