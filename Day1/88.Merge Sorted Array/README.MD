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

최대한 직관적이고 빠른 풀이법으로 작성한 답변이었지만, `pop(0)` 연산이 `O(n)`의 시간복잡도의 연산이기 때문에 O(n^2)의 시간복잡도가 나왔고, 이를 좀 개선하고 싶었다.

따라서 pop연산이 아닌, `nums2` 배열의 i - m의 인덱스를 직접 조회하고 값을 복사하여 O(n)의 복잡도로 개선할 수 있다고 생각했다.

```
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        for i in range(m, m+n):
            nums1[i] = nums2[i-m]
        nums1.sort()
```

기본기란 이런 것을 말하는 것인가 싶다. 코테준비를 하며, "무조건 빠르게 풀자"는 마인드로 늘 알고리즘 문제를 풀어왔지만, 이러한 당연하고도 사소한 것들을 잘 지키지 못한 것 같다.