# 153. Find Minimum in Rotated Sorted Array

[문제 링크](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/?envType=study-plan-v2&envId=top-interview-150)

정렬된 배열 `nums`가 주어진다.

`nums`는 내부의 랜덤한 원소만큼 rotate 되어 있을 수도 있다.

`nums`배열의 최소값을 리턴하라. O(log n)의 시간 복잡도로 해결하라.

## 접근법

```
1. rotate 전의 0번 인덱스의 값을 찾아야 하는 문제다. rotate이후엔 반드시 정렬되지 않은 부분이 존재하는데, 0번 인덱스는 반드시 여기에 있다.
2. O(log n)의 복잡도를 만족하려면 이분탐색을 진행해야 하며, 반으로 나눌 때마다 left, 혹은 right와 mid를 비교하여 정상적으로 정렬이 되어있는지를 확인한다.
3. 정렬되지 않은 쪽으로 이분탐색을 추가 진행한다.
4. 만약 mid가 왼쪽, 오른쪽 양쪽보다 작다면 정답이다.
```


## 코드
TC - O(log n)<br>
SC - O(1)

```
class Solution:
    def findMin(self, nums: List[int]) -> int:
        left = 0
        l = len(nums)
        right = l-1

        while left <= right:
            mid = (left + right) // 2
            if nums[mid] < nums[(mid+1)%l] < nums[mid-1]:
                return nums[mid]
            if nums[right] < nums[mid]:
                left = mid + 1
            else:
                right = mid - 1
        return nums[left]
            
```

## 결과

Runtime - Beats 83.30% users<br>
Memory - Beats 9.20% users


## 회고

이분탐색을 진행하던 중, mid < mid+1 < mid - 1를 만족하는 것이 곧 정답이고 이를 리턴하도록 하였다.

다른 Solution 들을 살펴보면, 탐색 도중 값을 발견하더라도 리턴하지 않고, 그냥 끝까지 이분탐색을 진행 후 left 혹은 right의 원소를 리턴하는 방법을 사용했다.

if 조건문을 하나 없앰으로서 탐색 자체를 더 빠르게 진행하고 어떤 케이스던 탐색을 끝마친 후에 값을 리턴하는 방식인 것이다.

```
class Solution:
    def findMin(self, nums: List[int]) -> int:
        l,r=0,len(nums)-1
        while l<=r:
            m=(l+r)//2
            if nums[m]<nums[r]: r=m
            else: l=m+1
        return nums[r]
```

내 코드가 요행을 바라고 검색 도중 값을 우연히 찾아내길 기대하는 걸까?

어차피 worst case 는 모든 탐색을 끝마친 후에 리턴하는 것이기 때문에 나도 이에 맞춰서 짜야 하는것일까?

솔직히 잘 모르겠다. 하지만 모든 상황에 대비한 로직을 짤 수 있어야겠다고 생각했다.