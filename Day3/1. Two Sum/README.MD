# 1. Two Sum

[문제 링크](https://leetcode.com/problems/two-sum/description/?envType=study-plan-v2&envId=top-interview-150)

`MinStack` 클래스의 틀이 주어진다.

`getMin` 연산 시 스택 내부에서 가장 작은 값을 상수의 시간복잡도로 가져와야 한다.

그밖에 push, pop, top 메소드를 구현해야 한다.


## 접근법
```
1. 기존 스택과 큰 차이는 없으나, 상수의 복잡도로 최소값을 가져오려면, 스택 내부의 최소값에 대해 미리 저장해두어야 한다.
2. pop 연산을 통한 제거 이후 최소값이 유지되어야 하므로, 떠오르는 방법은
    2-1. stack 내부에 heapq를 추가적으로 선언하여 그때마다 최소값을 계산한다.
    2-2. 매 스택마다 2개의 값을 저장한다. 하나는 현재 위치의 값, 다른 하나는 현재 위치까지의 최소값
3. 2-2에 명시된 방법으로 구현했다
    3-1. 매 pop 연산마다 heapq 내부에서도 업데이트를 해줘야 하는 점이 시간복잡도를 상수값의 시간복잡도로 해결하는 것이 불가능하기 떄문이다.
```

## 코드
TC - O(1)<br>
SC - O(n)

```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        arr = []
        first = 0
        for i in range(len(nums)):
            if target-nums[i] in nums[i+1:]:
                first = i
                arr.append(i)
                break
        for j in range(first+1, len(nums)):
            if target - nums[first] == nums[j]:
                arr.append(j)
                return arr
```

## 결과

Runtime - Beats 91.06% users<br>
Memory - Beats 5.58% users

## 회고

```
공간복잡도를 더 개선한 사례를 찾아보았으나, 그때마다 min 연산을 통해 최소값을 구하는 대신 최소값을 저장하지 않는 케이스 말고는 찾을 수 없었다.

min 연산을 매 연산마다 실행한다면 상수값을 초과한 시간복잡도가 나오게 되므로, 이는 참고할 수 없다고 판단하여 리팩토링하지 않았다.
```