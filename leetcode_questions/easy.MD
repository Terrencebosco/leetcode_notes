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

