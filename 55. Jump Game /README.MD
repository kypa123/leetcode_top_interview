#55.Jump Game

[문제 링크](https://leetcode.com/problems/jump-game/description/?envType=study-plan-v2&envId=top-interview-150)

`nums`배열이 주어지며, 0번째 인덱스부터 마지막 인덱스까지 도달할 수 있는지 여부를 리턴한다.

각 배열의 원소는 현재 인덱스값에서 **이동할 수 있는 거리를 의미한다.**

ex) [2,3,1,1,4] -> true<br>
[3,2,1,0,4] -> false

##접근법
```
1. 배열 arr를 선언해, 각 인덱스가 도달가능한지 여부를 판단했다.
2. nums를 순회하며, 현재 인덱스가 arr를 참조해 도달가능하다면, 현재 인덱스 + 1~현재인덱스의 값 을 arr에서 1로 표시해준다.
3. 마지막 인덱스의 arr값이 도달가능이라면 true를, 아니라면 false를 리턴한다.
```

##코드
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

##결과
Runtime - Beats 12.70% users
Memory - Beats 25.44% users

##회고
```
```