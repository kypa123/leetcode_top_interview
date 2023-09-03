# 33. Search in Rotated Sorted Array

[문제 링크](https://leetcode.com/problems/search-in-rotated-sorted-array/?envType=study-plan-v2&envId=top-interview-150)

중복되지 않은 원소들로 이루어진 정렬된 배열 `nums`, 정수 `target`이 주어진다.

해당 배열은 배열에 존재하는 랜덤한 원소 중 하나만큼, 배열이 rotate 되어 있다.

배열 속에 target 이 존재한다면 해당 인덱스값을, 없다면 -1을 리턴해야 한다.

O(log n)의 시간복잡도로 해결해야한다.

## 접근법

1.log n의 복잡도로 해결하기 위해서 이분탐색을 진행한다.

2.일반적인 이분탐색과 다른 점은, rotate 여부에 따라 정상적인 이분탐색이 진행되지 않을 수 있다는 점이다. 

3.따라서 매 루프마다 rotate 되지 않고 정상적인 sorted 형태의 절반인지 여부를 확인하면서 탐색을 진행한다.

3-1. mid값이 left원소보다 크다면 왼쪽이 정상적으로 sort되었는지 (left <= target < mid) 확인하고, 그렇다면 왼쪽을 탐색, 아니라면 오른쪽을 탐색한다.

3-2. right의 경우에도 같은 체크를 해준다.



## 코드

TC - O(log n)<br>
SC - O(1)

```
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1
        
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] == target:
                return mid
            if nums[left] <= nums[mid]:
                if nums[left] <= target < nums[mid]:
                    right = mid - 1
                else:
                    left = mid + 1
            else:
                if nums[mid] < target <= nums[right]:
                    left = mid + 1
                else:
                    right = mid - 1
        return -1
```

## 결과

Runtime - Beats 62.47% users<br>
Memory - Beats 33.26% users


## 회고

조건에 대해 고민을 많이 해야 했던 문제였다. O(log n)의 복잡도로 해결하기 위해서 이분탐색을 진행해야 한다는 것은 이해했지만

정렬되지 않은 배열에 대해 진행하기 위해서 다양한 조건을 생각해야 하는 문제였던 것 같다.