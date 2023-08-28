# 209. Minimum Size Subarray Sum


[문제 링크](https://leetcode.com/problems/minimum-size-subarray-sum/description/?envType=study-plan-v2&envId=top-interview-150)

배열 `nums` 와 정수 `target` 가 주어진다.

`nums` 내부의 연속된 부분배열 중, 합이 target보다 크거나 같은 최소 길이를 구하는 문제이다. 

## 접근법

```
1. 모든 값을 더해도 target보다 작다면 0을 리턴한다.
2. 슬라이딩 윈도우 알고리즘을 활용하여, 카운트할 인덱스를 0으로 초기화해두고 nums를 순회하며 값을 total에 누적시켜 준다.
3. 매 순회마다 값을 total에 더한다. 이때 total이 target보다 크거나 같다면
    3-1. total값이 target보다 작아질 때까지 0으로 초기화해둔 카운팅 인덱스의 값을 빼준다.
    3-2. 값을 빼줄때마다 인덱스를 1 증가시켜준다.
    3-3. 값을 업데이트할 때마다, answer = min(end - start)로 업데이트해 준다.
```

## 코드

TC - O(n)<br>
SC - O(1)
```
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        if sum(nums) < target:
            return 0
        answer = len(nums)
        start = 0
        l = len(nums)
        total = 0

        for i in range(l):
            total += nums[i]
            if total >= target:
                while total >= target:
                    answer = min(answer, i - start + 1)
                    total -= nums[start]
                    start += 1
        return answer
```

## 결과

Runtime - Beats 94.54% users<br>
Memory - Beats 5.96% users 

## 회고

매 루프마다 리스트를 슬라이싱해서 sum하는 방식으로는, 시간초과의 우려가 있는 문제이다.

슬라이딩 윈도우 알고리즘, 이진탐색 등 기초적인 알고리즘은 반드시 공부하고 문제풀이에 임해야 효율적인 코드를 짜낼 수 있다고 다시한번 느꼈다.