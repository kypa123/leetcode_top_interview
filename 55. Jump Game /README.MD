# 55.Jump Game

[문제 링크](https://leetcode.com/problems/jump-game/description/?envType=study-plan-v2&envId=top-interview-150)

`nums`배열이 주어지며, 0번째 인덱스부터 마지막 인덱스까지 도달할 수 있는지 여부를 리턴한다.

각 배열의 원소는 현재 인덱스값에서 **이동할 수 있는 거리를 의미한다.**

ex) [2,3,1,1,4] -> true<br>
[3,2,1,0,4] -> false

## 접근법

```
1. 배열 arr를 선언해, 각 인덱스가 도달가능한지 여부를 판단했다.
2. nums를 순회하며, 현재 인덱스가 arr를 참조해 도달가능하다면, 현재 인덱스 + 1~현재인덱스의 값 을 arr에서 1로 표시해준다.
3. 마지막 인덱스의 arr값이 도달가능이라면 true를, 아니라면 false를 리턴한다.
```

## 코드

TC - O(n^2)<br>
SC - O(n)

```
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        l = len(nums)
        arr = [0]*l
        arr[0] = 1
        for i in range(l):
            if arr[i]:
                for j in range(nums[i]+1):
                ##순회중 이미 마지막 인덱스에 도달했다면
                    if i + j >= l-1:
                        return True
                    arr[i+j] = 1
        if arr[l-1] == 1:
            return True
        return False
```

## 결과

Runtime - Beats 12.70% users<br>
Memory - Beats 25.44% users

## 회고

각 인덱스에서 모든 경우의 수, 최대 10^5만큼 계산할 수 있는 굉장히 위험한 풀이방식이었다.

분명 더 나은 풀이법이 있을 것이라고 생각해, 좋은 솔루션을 찾아보았다.

```
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        if len(nums) == 1:return True
        i = 0;j = i
        for i in range(100000):
            if j > i+nums[i]:pass
            else:j = i+nums[i]
            i+=1
            if i > j:break
            if j >= len(nums)-1:return True
        return False
```

하나하나 도달가능한지 확인하지 않고, j라는 변수를 통해 도달가능한 값들을 계산하고 있다.

만약 도달할 수 없는지 여부는 if i > j: break 조건문으로 간단하게 해결하고 있다.

굉장히 짧고 간단한 풀이법으로도 문제를 해결할 수 있구나 싶었다.

더욱 더 꾸준히 공부하고, 좋은 코드를 접해야겠다.