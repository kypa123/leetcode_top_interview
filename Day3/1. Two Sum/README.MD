# 1. Two Sum

[문제 링크](https://leetcode.com/problems/two-sum/description/?envType=study-plan-v2&envId=top-interview-150)

배열 `nums`, 정수형 `target` 가 주어진다.

`nums`안에서 더하면 `target`이 되는 숫자 2개의 인덱스를 반환해야 한다.

반드시 정답이 하나만 존재하고 같은 원소를 2번 사용할 수 없다. 

## 접근법
1. 공간복잡도와 시간복잡도 중 어디에 중점을 두고 풀지 고를 수 있다고 생각했다.
2. 시간복잡도를 중점으로 푼다면 해시테이블(딕셔너리)를 통해 매 원소마다 `target - 원소`를 딕셔너리에 저장하고, 이미 존재한다면 이 두 쌍이 곧 정답이다.
3. 공간복잡도를 중점으로 푼다면, 두 번의 루프를 통해 `target - 원소` 가 `arr[:현재 인덱스 + 1]`에 존재하는지 계속해서 체크해주면 될 것이다.

## 코드

TC - O(n^2)<br>
SC - O(1)

```
공간복잡도에 중점을 두고 품
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


TC - O(n)<br>
SC - O(n)
```
시간복잡도에 중점을 두고 품
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        d = {}
        n = len(nums)

        for i in range(n):
            temp = target - nums[i]
            if temp in d:
                return [d[temp], i]
            d[nums[i]] = i

        return []
```
## 결과

Runtime - Beats 38.33% users<br>
Memory - Beats 100% users

Runtime - Beats 64.31% users<br>
Memory - Beats 50.91% users

## 회고

퍼센테이지로는 다소 보기 힘들지만, 메모리를 더 사용한 쪽의 런타임이 약 12배가량 더 빨랐다. (854ms -> 71ms)

메모리는 14.9mb, 17.6mb로 약 30% 더 사용하였다.

속도와 메모리는 트레이드오프라고 알고있는데, 정답이라고 할 순 없지만 현대의 알고리즘은 넉넉한 메모리 속에서 빠른 속도를 구현하는 것이 대부분인 것 같다.