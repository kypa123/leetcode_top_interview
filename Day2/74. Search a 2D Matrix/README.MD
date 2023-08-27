# 74. Search a 2D Matrix


[문제 링크](https://leetcode.com/problems/search-a-2d-matrix/description/?envType=study-plan-v2&envId=top-interview-150)

정렬된 2차원배열 `matrix`, `target` 정수가 주어진다

`matrix`의 각 배열의 첫 정수는 이전 배열의 마지막 정수보다 크다

`matrix` 안에 `target`이 존재하는지 리턴해야 한다

## 접근법
```
1. 각 배열의 처음과 끝 사이에 target이 있는지 검사하여, 검색해야 할 배열을 특정화한다.
2. 해당 배열에 target이 존재하는지 확인한다.
```

## 코드

TC - O(nm)<br>
SC - O(1)

```
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        for mat in matrix:
            start = mat[0]
            end = mat[-1]
            if not start <= target <= end:
                continue
            else:
                if target in mat:
                    return True 
                else: return False
```

## 결과

Runtime - Beats 64.80% users<br> 
Memory - Beats 58.3% users


## 회고

배열도 정렬되고, 매트릭스 또한 정렬되었기 때문에 이분탐색을 사용하면 좀 더 성능을 개선할 수 있을 것이라고 생각헀다.

첫 번째로, 검사할 배열을 찾는 과정이다. 각 배열의 마지막 값과 다음 배열의 첫번째 값을 비교하여 이분탐색을 진행한다.

```
x, y = len(matrix),len(matrix[0])
start, end = 0, x-1

while start<=end:
    mid=(start+end)//2
    if target < matrix[mid][0]:
        end = mid -1
    elif target>matrix[mid][-1]:
        start = mid+1
    else:
        break

row = (start + end) // 2
```

`x`는 매트릭스의 배열의 개수, `y`는 매트릭스의 배열의 원소의 개수를 각각 나타낸다.

어떤 배열을 선택할지 정하기 때문에, `x`를 기준으로 검색을 실시한다.

이분탐색을 통해 배열이 정해졌다면, 정해진 배열 내부에서 `target`에 대한 이분탐색을 실시한다.

```
l,r = 0, y-1
while l <= r:
    mid = (l+r)//2
    if target < matrix[row][mid]:
        r = mid-1
    elif target > matrix[row][mid]:
        l = mid+1
    else:
        return True
return False
```

결과 코드는 다음과 같다.

```
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        x, y = len(matrix),len(matrix[0])
        start, end = 0, x-1

        while start<=end:
            mid=(start+end)//2
            if target < matrix[mid][0]:
                end = mid -1
            elif target>matrix[mid][-1]:
                start = mid+1
            else:
                break

        row = (start + end) // 2
                
        l, r = 0, y-1
        while l<=r:
            mid = (l+r)//2
            if target < matrix[row][mid]:
                r = mid-1
            elif target > matrix[row][mid]:
                l = mid+1
            else:
                return True
        return False
```

결과적으로 시간복잡도를 O(mn) -> O(log mn)으로 개선할 수 있었다.

정렬된 조건 속에서 이분탐색을 실행하면, 대다수의 경우에서 좋은 퍼포먼스를 기대할 수 있다.


코딩테스트를 준비하다 보니, 늘 풀이를 즉흥적으로 생각하고 빠르게 구현하는 것이 습관이 된 것 같다.

최적의 알고리즘을 즉흥적으로 떠올릴 수 있는 그날까지 꾸준히 실력을 쌓아야겠다고 느꼈다.