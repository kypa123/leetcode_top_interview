# 169.Majority Element

[문제 링크](https://leetcode.com/problems/majority-element/description/?envType=study-plan-v2&envId=top-interview-150)

배열 `nums`가 주어진다.

배열의 길이를 `n`이라고 했을 때, 배열 `nums`에서 n / 2 이상의 횟수로 등장하는 값을 리턴하면 된다.


## 접근법

```
1. 배열의 길이 / 2를 통해, 리턴해야 할 상한선을 구한다.
2. Counter 라이브러리를 통해 각 원소의 개수를 구한다.
3. 각 원소의 개수가 상한선을 넘는다면, 이를 리턴한다.
```

## 코드

TC - O(n)<br>
SC - O(n)

```
from collections import Counter

class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        n = len(nums)/2
        c = Counter(nums)
        for key, val in c.items():
            if val >= n:
                return key
```

## 결과

Runtime - Beats 70.66% of users<br>
Memory - Beats 68.22% of users

## 회고

Counter를 활용하여 모든 요소의 개수를 세고 계산하는 것이기 때문에, O(n)의 복잡도를 가진 해결법이었다.

더 나은 메모리 퍼포먼스를 가진 솔루션을 살펴보니, Counter를 사용하지 않고 직접 hashmap을 선언해 그때그때마다 Count를 하고 기준을 넘어가는 순간 즉시 리턴하는 방법이 많았다.

```
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        hash = defaultdict(int)
        for num in nums:
            hash[num]+=1
        return max(hash, key=hash.get)
```

코딩테스트를 준비하다보면 이러한 케이스 하나하나마다 효율을 고려하여 문제를 해결하지는 않았다. 코딩테스트만을 준비하는 것이라면 나의 방법이 틀렸다고 생각하지는 않는다.

코딩테스트는 언제나 worst case를 준비하는 방식으로 해결해야 하기 때문이다.

하지만 만약 현업에서 이러한 기능을 구현할 일이 생긴다면 worst case만을 고려한 해결법이 아닌, 이런 통상적인 케이스를 위한 코드를 짜는 것이 맞겠다고 느꼈다. 