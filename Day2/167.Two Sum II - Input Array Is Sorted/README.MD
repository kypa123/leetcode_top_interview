# 167.Two Sum II - Input Array Is Sorted

[문제 링크](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/?envType=study-plan-v2&envId=top-interview-150)



## 접근법

정렬된 `List` 배열이 주어지고, `target` 정수가 주어진다. 배열 속에서 2개의 숫자를 더하여 `target`이 만들어지는 숫자를 찾아야한다.

반드시 정답이 존재하는 문제이다.

투 포인터 알고리즘을 통해 0번째 인덱스와 끝 인덱스를 체크하여 두 수의 합을 계속해서 계산해줬다.

`target`보다 작다면 시작 인덱스를 +1, 크다면 끝 인덱스를 -1하며 진행했다.

## 코드

TC - O(n)<br>
SC - O(1)
```
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        start = 0
        end = len(numbers)-1
        while start < end:
            curr = numbers[start] + numbers[end]
            if curr == target:
                return [start+1, end+1]
            elif curr < target:
                start += 1
            else:
                end -= 1
        return []
```

## 결과

Runtime - Beats 99.67%<br>
Memory - Beats 57.86%

## 회고

해당 문제같은 경우, `반드시 정답이 존재한다`는 조건이 붙기 때문에 좀 더 직관적인 while 루프의 조건을 명시할 수 있다.

답이 존재하지 않을수도 있다면, left와 right가 만날 때까지 루프를 도는 것이 일반적이지만 해당 문제는 그렇지 않기 때문이다.

따라서, 다음과 같이 개선사항을 적용할 수 있다.

```
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        start = 0
        end = len(numbers)-1
        while numbers[start] + numbers[end] != target:
            if numbers[start] + numbers[end] < target:
                start += 1
            else:
                end -= 1
        return [start+1, end+1]
```

코드가 좀 더 짧아졌고, while 반복문의 반복조건에 제한사항을 명시함으로서 if조건문을 줄일 수 있었다.