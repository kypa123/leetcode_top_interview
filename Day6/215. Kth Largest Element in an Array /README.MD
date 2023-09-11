# 215. Kth Largest Element in an Array

[문제 링크](https://leetcode.com/problems/kth-largest-element-in-an-array/description/?envType=study-plan-v2&envId=top-interview-150)

정수 배열 `nums`, 정수 `k`가 주어진다.

`nums`안에서 `k`번째 큰 수를 반환해야 한다. 

## 접근법

1. `nums` 를 reverse 정렬한다.
   
2. k번째 인덱스의 값을 반환한다.

## 코드
TC - O(n log n)<br>
SC - O(n)


```
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        temp = sorted(nums,reverse=True)
        return temp[k-1]
    
```

## 결과

Runtime - Beats 45.85% users<br>
Memory - Beats 82.68% users

## 회고

직관적으로 먼저 풀고, `solve without sorting`이라는 조건을 만족하기 위한 개선 코드를 짜고자 하였다.

sort를 하지 않고 정렬되지 않은 상태에서 순서에 따른 값을 구하려면, `heap` 자료구조를 사용해야 한다.

파이썬은 최대 힙을 지원하지 않기에, 각 원소에 - 를 입력하여 음수값으로 저장하는 방법을 통해 max heap 자료구조를 사용하거나,

일단 최소힙을 만들고 len(heap) - `k` 만큼 heappop연산을 해도 괜찮을 것 같다고 생각했다.

두 번째 풀이로 해결하였다.

```
import heapq

class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        heapq.heapify(nums)
        for i in range(len(nums) - k):
            heapq.heappop(nums)
        return heapq.heappop(nums)
```