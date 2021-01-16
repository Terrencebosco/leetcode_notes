# Easy Questions 2020/2021

## 1688. Count of Matches in Tournament
You are given an integer n, the number of teams in a tournament that has strange rules:

If the current number of teams is even, each team gets paired with another team. A total of n / 2 matches are played, and n / 2 teams advance to the next round.
If the current number of teams is odd, one team randomly advances in the tournament, and the rest gets paired. A total of (n - 1) / 2 matches are played, and (n - 1) / 2 + 1 teams advance to the next round.
Return the number of matches played in the tournament until a winner is decided.

### My Solution:
```python
class Solution(object):
    def numberOfMatches(self, n):
        """
        :type n: int
        :rtype: int
        """

        matches = 0

        while n != 1:
            matches +=  (n+1) // 2
            n //= 2
        return matches
```

General Idea: while we have more than 1 possible match we take the floor + 1
of the current number of matches. we then set the number of matches to n // 2
this will handle all the odd matches because we take add 1 to the odd for the bye
team and if the n is odd we take the floor and ignore the bye team.

### Result:
Runtime: 16 ms, faster than 75.00% of Python online submissions for Count of Matches in Tournament.
Memory Usage: 13.5 MB, less than 25.00% of Python online submissions for Count of Matches in Tournament.

---


## Two Sum

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order.

Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].

### My Solution:

```python
   for i in range(len(nums)):
            for j in range(len(nums)-1):
                if (nums[i] + nums[j] == target) and (nums[i] != nums[j]): # check element not index.
                    return [i,j]
                continue
```

not correct, my solution solves the general test case but runs into errors when
with edge cases. when the elements of the array are adentical like `[3,3]` i run into
issues because we dont want to the solution to be made with the same element.
for example `[1,3]` is an invalade array for target = 6 even though 3+3=6.

### leetcode Solution:

```python
       h = {}
        for i, num in enumerate(nums):
            n = target - num
            if n not in h:
                h[num] = i
            else:
                return [h[n], i]
```
first we create an empty dictionary. then we enumerate over the array given to us.
we set n to be the difference between the target and the value of the current enumerated index. i idea here is, we are looking for a number thats in our dict. the
number will be the difference between the targen and our current value, in this case "n". we and the sum of two numbers to be equal to the target. so the same logic can be
applied to the difference of the target and current val. because n+val=target.
if "n" is not in our dictionary. we set the key as the current value and the value as the index.
if n IS in the dictionary we return the answer. in this case a list with `[h[n],i]` where h[n] is a dictonary reference to the key we set prior and the current index that
sum to the targe.

### Referance:
brute force two pointer solution:
```py
      n = len(nums)
        idx1=None
        idx2=None
        for i in range(n-1):
            for j in range(i+1,n):
                if nums[i]+nums[j]==target:
                    idx1,idx2=i,j
                    break
        return [idx1,idx2]
```

---

## XOR bitwise operation
we can use the XOR operatior (^) to find the difference in two sets of strings/integers. but this tells us the difference in the set of char. for example `a = 1223 and b = 123` we want
the `2` to be returned because thats the difference in the two sets of numbers. so
```py
def find_difference(str_1, str_2):

    # we concat the strings into one set
    c = str_1 + str_2

    #store the bits
    temp = 0
    # itter through concated string and save the BIT version of the i'th to temp
    # this will store bits and then revers the bit if it shows up again.
    # this will only work if there are even sets of chars in the strings
    # with only 1 odd char
    for i in c:
        # The ord() function returns an integer representing the Unicode character.
        temp ^= ord(i)
    return chr(temp)

```
this same operation can be used with ints but dont need to convert to int unicode.

[XOR doc](https://python-reference.readthedocs.io/en/latest/docs/operators/bitwise_XOR.html)

[ord doc](https://www.programiz.com/python-programming/methods/built-in/ord)
