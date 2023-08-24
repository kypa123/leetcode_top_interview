# 26.Remove Duplicates from Sorted Array

[문제 링크](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/?envType=study-plan-v2&envId=top-interview-150)

정렬된 배열 `nums`가 주어진다.

`in-place` 알고리즘을 활용하여 추가 메모리 없이 중복된 값들을 제거해야 한다.

중복되지 않은 값들을 각각 한개씩 `nums`의 0번인덱스에 가깝게 끌어와야 한다.

ex) [1,2,2,3,3,4,5] -> [1,2,3,4,5,_,_]

중복되지 않은 값들의 개수를 리턴한다.


## 접근법

```
1. 추가 메모리, 배열, visited는 허용되지 않는다.
2. 0번째 인덱스부터 카운팅을 시작하고, 카운트 인덱스의 값과 순회하는 인덱스의 값이 다르다면, 배열의 카운트 인덱스 번째 값을 업데이트한다.
3. 업데이트가 일어나면 카운트 인덱스를 1 증가시킨다.
4. 카운트 인덱스 + 1을 리턴한다.
```

## 코드

TC - O(n)<br>
SC - O(1)

```
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        i = 0
        for j in range(1, len(nums)):
            if nums[i] != nums[j]:
                i += 1
                nums[i] = nums[j]
        
        return i + 1
```

## 결과

Runtime - Beats 93.41% of users<br>
Memory - Beats 52.36% of users


## 회고

in-place 알고리즘을 풀면서 코딩테스트를 준비하며 무작정 알고리즘을 외워왔던 과정에서 건너뛰어버린 기본기들을 배우게 되는 느낌이었다.

동적 계획법을 처음으로 접했을 때 굉장히 막막했고 이해하기 어려웠는데, 그때 느꼈던 CS 기본기의 부재들을 이번 문제를 통해 조금이나마 배우게 된 느낌이었다.

굳이 사용하지 않아도 될 메모리는 사용하지 않도록 의식하면서 코드를 짜보아야겠다고 느꼈다.