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

---

## add two numbers (linked list)

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        # set up a dummy head for the temp new linked list.
        # this will make it easer to call the "answer" value.
        # setting to empty nodes.

        # we need to use the carry variable to make the addititon of the linkeds
        # becasue the nodes can only be single values for the answer
        # ie [4]->[6]->[4]
        #  + [4]->[5]->[6]
        # -------------------
        #    [9]->[2]->[1]

        dummy = cur = ListNode(0)
        carry = 0
        # while at least one of these isnt "None" continue.
        while l1 or l2 or carry:

            # add the values to the carry, move to the next.
            if l1:
                carry += l1.val
                l1 = l1.next
            if l2:
                carry += l2.val
                l2 = l2.next

            # mod the current value, so we can remove the "tens" place digit.
            cur.next = ListNode(carry%10)

            #move to the next node of the linkedlist
            cur = cur.next

            # floor the current value to get the tens place to carry to next value
            carry //=10

        # return the next node of the link that is a nested link with the
        # link of the answer.
        return dummy.next
```

we have to make sure that the next value in the linked list is as single digit and that we can carry the tens place value to the next
node in the link. the only confusing part is the dummy head. but this allows us to call the .next to get the nested linked list?

"Note that we use a dummy head to simplify the code. Without a dummy head, you would have to write extra conditional statements to initialize the head's value." via leetcode solution.

```
Complexity Analysis

Time Complexity: O(max(m,n)+1)
where m is the length of linked list l1, n is the length of linked list l2.
The algorithm needs to iterate at most O(max(m,n)+1) times. "+1" comes from the carry.
Space Complexity:O(max(m,n) + 1)
where m is the length of linked list l1, n is the length of linked list l2.
The algorithm needs to create a new list, and the length will be at most max(m,n)+1
```

---

## 7. Reverse Integer

Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range [-231, 231 - 1], then return 0.

Assume the environment does not allow you to store 64-bit integers (signed or unsigned).

```py
class Solution(object):
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """

        answer = int(str(abs(x))[::-1]) if x > 0 else -1 * int(str(abs(x))[::-1])
        if answer.bit_length() >= 32:
            return 0
        return answer
```

 pretty straight forward problem. the biggest issue i ran into was just trying to handle the zeros. i started by just making it a string then splicing off the firts element. but this didnt handle multiple zeros (ie 109000). but just reversing and turning into int removes all zeros before a hole number. using bit_length tells you how long a elements bit size is. so
 2**31 the largest number that can be calculated with 32 bits is "4294967295". so any number thats larger than that or has a longer bit length of 32 is invalid.