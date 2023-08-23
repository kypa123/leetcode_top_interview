# Merge Sorted Array

[문제 링크](https://leetcode.com/problems/merge-sorted-array/description/?envType=study-plan-v2&envId=top-interview-150)

`num1`, `num2` 두 개의 정렬된 배열을 병합하여 `num1` 배열을 업데이트하는 문제이다

이때, `num1`은 `num2` 배열의 길이만큼 배열의 끝에 0이 존재한다

`m` 과 `n`이 주어지며, 각각 `num1`, `num2`의 0이 아닌 값의 개수이다


## 접근법

```
1. nums1의 m번째 인덱스 이후부터는 0이 n개만큼 존재한다.
2. 따라서, nums1 배열의 m ~ m+n 번째 인덱스에 nums2의 값들을 채워넣으면 된다고 판단했다.
```

## 코드

tc - O(n^2)
sc - O(1) 

```
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        for i in range(m, m+n):
            nums1[i] = nums2.pop(0)
        nums1.sort()
```

## 결과

Runtime
Beats 67.80% of users

Memory
Beats 99.91% of users

## 회고
```
```
