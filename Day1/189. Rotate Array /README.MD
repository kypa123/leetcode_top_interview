# 189.Rotate Array

[문제 링크](https://leetcode.com/problems/rotate-array/description/?envType=study-plan-v2&envId=top-interview-150)

배열 `nums`가 주어지고, 이를 회전시켜야 할 횟수 `k` 가 주어진다.

배열의 회전이란, 배열의 오른쪽 끝의 값을 왼쪽 끝으로 옮기는 것이다.

## 접근법

```
1. nums.pop을 통해 배열의 끝값을 가져와 nums.insert(0)을 통해 입력해주었다.
```

## 코드

TC - O(k * n)<br>
SC - O(1)

```
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        for i in range(k):
            nums.insert(0, nums.pop(-1))
```

## 결과

Runtime - Beats 14.16% users<br>
Memory - Beats 69.64% users

## 회고

deque 라이브러리의 rotate method처럼, 굉장히 직관적으로 pop 후에 insert(0) 연산을 통해 해결했다.

다만 퍼포먼스 측면에서는 다소 불리할 수밖에 없다고 느꼈고, 더 나은 퍼포먼스를 기록하는 좋은 풀이법들을 살펴 내 문제점들을 파악하고자 하였다.

```
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        temp = []
        k = k % len(nums)
        temp = nums[-k:]
        nums[k:] = nums[:-k]
        nums[:k] = temp
```

해당 코드를 보며 느낀게 많았다. 내 코드보다 우수한 점은

1. k를 len(nums)로 나눠주면서, 어차피 같은 결과를 만드는 큰 k의 값들을 최소값으로 줄였다.

2. 인덱스 슬라이싱을 통해 pop, insert 등 불필요한 연산을 하지 않았다

3. k만큼의 추가 메모리를 활용하여 시간복잡도를 개선시켰다.

간단명료하면서도 우수한 코드를 짤 수 있도록, 좋은 코드들을 더 많이 봐야겠다.