#169.Majority Element

[문제 링크](https://leetcode.com/problems/majority-element/description/?envType=study-plan-v2&envId=top-interview-150)

배열 `nums`가 주어진다.

배열의 길이를 `n`이라고 했을 때, 배열 `nums`에서 n / 2 이상의 횟수로 등장하는 값을 리턴하면 된다.


##접근법
```
1. 배열의 길이 / 2를 통해, 리턴해야 할 상한선을 구한다.
2. Counter 라이브러리를 통해 각 원소의 개수를 구한다.
3. 각 원소의 개수가 상한선을 넘는다면, 이를 리턴한다.
```

##코드
TC - O(n)<br>
SC - O(n)
```
from collections import Counter

class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        n = len(nums)/2
        c = Counter(nums)
        for key, val in c.items():
            if val >= n:
                return key
```

##결과
Runtime - Beats 70.66% of users<br>
Memory - Beats 68.22% of users

##회고
```
```