#189.Rotate Array

[문제 링크](https://leetcode.com/problems/rotate-array/description/?envType=study-plan-v2&envId=top-interview-150)

배열 `nums`가 주어지고, 이를 회전시켜야 할 횟수 `k` 가 주어진다.

배열의 회전이란, 배열의 오른쪽 끝의 값을 왼쪽 끝으로 옮기는 것이다.

##접근법

```
1. nums.pop을 통해 배열의 끝값을 가져와 nums.insert(0)을 통해 입력해주었다.
```

##코드
TC - O(k * n)<br>
SC - O(1)
```
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        for i in range(k):
            nums.insert(0, nums.pop(-1))
```

##결과
Runtime - Beats 14.16% users<br>
Memory - Beats 69.64% users

##회고
```
```