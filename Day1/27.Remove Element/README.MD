# 27.Remove Element

[문제 링크](https://leetcode.com/problems/remove-element/description/?envType=study-plan-v2&envId=top-interview-150)

`nums` 배열 안의 `val` 정수를 전부 삭제해야 한다.

`in place` 알고리즘을 사용하여 추가 메모리를 할당하지 않고 해결해야 한다.

`val`이 아닌 숫자들의 개수를 리턴하며, `nums` 배열은 `val`이 아닌 숫자들을 전부 0번째 인덱스쪽으로 당겨서 가져와야 한다.

즉, val이 3일때 [3,2,2,3] -> [2,2,_,_]으로 업데이트해야 한다.

## 접근법

```
1. in-place 알고리즘을 사용해야 하므로, 배열을 선언하고 val이 아닌 숫자들을 집어넣는 방법은 사용할 수 없다.
2. nums를 순회하며 0번째 인덱스부터 확인을 한다. 이때 val이 아니라면 카운팅하고 있는 인덱스값에 값을 집어넣는다.
3. 카운팅하는 인덱스를 +1 한다.
4. 마지막으로 카운팅한 인덱스를 리턴한다. 카운팅한 인덱스는 val이 아닐때마다 업데이트가 일어나므로 val이 아닌 숫자의 값과 같다.  
```

## 코드

TC - O(n)<br>
SC - O(1)

```
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        answer = 0
        for i in range(len(nums)):
            if nums[i] != val:
                nums[answer] = nums[i]
                answer += 1
        return answer
```

## 결과

TC - Beats 46.62% users<br>
SC - Beats 33.75% users

## 회고

in place 알고리즘은 국내 코딩테스트를 준비하는 입장에서는 쉽게 접하지 못하는 문제였다.

보통 국내 코딩테스트의 문제들은 공간복잡도를 신경쓴다기보다는 넉넉한 메모리를 제공하고 최대한 빠른 시간복잡도를 확보하여 문제를 해결하는 문제가 절대 다수였다.

대부분 O(n^2)의 복잡도를 O(n log n)으로 줄인다던가 하는 방식이었다.

그런 면에서 리트코드의 in place 알고리즘 문제들은 꽤 색다른 느낌의 문제라고 느껴졌고, 자료구조의 굉장히 기초적인 개념들을 복습하게 해주는 기회였던 것 같다. 