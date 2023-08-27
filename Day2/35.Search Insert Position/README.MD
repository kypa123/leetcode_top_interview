# 35. Search Insert Position


[문제 링크](https://leetcode.com/problems/search-insert-position/description/?envType=study-plan-v2&envId=top-interview-150)

정렬된 배열 `nums`와 `target` 정수가 주어진다.

만약 `target`이 `nums`에 존재한다면 해당 값의 인덱스를,

존재하지 않는다면 정렬된 값이 유지되도록 `target`을 insert할 위치의 인덱스를 반환해야한다.

## 접근법
```
1. 투 포인터 알고리즘, 이분탐색을 활용하여 target의 위치를 탐색한다.
2. 탐색을 종료한 시점의 start, end의 중간지점을 리턴한다. 이때 mid의 값괴 비교하여 크거나 작은 경우를 검사하여 중간지점 +1을 추가한다. 
```

## 코드

TC - O(log n)<br>
SC - O(1)

```
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        start = 0
        end = len(nums)

        while start < end:
            mid = (start + end)//2 
            if nums[mid] < target:
                start = mid+1
            elif nums[mid] > target:
                end = mid-1

            else:
                break
        mid = (start + end) // 2
        if mid < 0:
            return 0
        if mid >= len(nums):
            return len(nums)
        if nums[mid] < target:
            return mid + 1

        return mid
```

## 결과

Runtime - Beats 97.88% users<br>
Memory - Beats 14.20% users

## 회고

마지막의 mid를 다시 계산하는 3개의 if문을 없애고 싶었다. 이분탐색이 끝나면 즉시 값을 도출해낼 수 는 없을까?

검색 결과 좋은 답변을 찾을 수 있었다. 이분탐색을 할 때 주의해야 할 점은 종료조건, 루프시마다 바뀌는 start, end의 업데이트를 신중하게 해야한다는 점인데 

너무 안일하게 빠르게 코드를 짜내려고 했었고, 결과적으로 깔끔하지 못한 로직이 만들어졌던 것 같다.

```
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        start = 0
        end = len(nums)-1

        while start <= end:
            mid = (start + end)//2 
            if nums[mid] < target:
                start = mid+1
            elif nums[mid] > target:
                end = mid-1
            else:
                return mid
        
        return start
```

start <= end 로 while 루프 조건을 변경하였고, 값이 일치한다면 즉시 값을 리턴하도록 변경하였다.

반복문을 통한 이분탐색은 start <= end 로 조건을 설정함으로서 마지막 순회까지 진행해야 올바른 값을 얻을 수 있다.

왜 start < end 는 올바르게 동작하지 않은걸까? 예제를 직접 실행해가며 문제점을 확인한 결과, 다음과 같은 문제점을 발견할 수 있었다.

```
start < end의 문제점은 start와 end가 1의 차이로 좁혀졌을 때 나타난다.
각각 1,2일때 중앙값인 1번째 인덱스에 대해 검사를 하게 되는데, 해당 인덱스보다 target이 클수도, 작을수도 있다.
target이 작다면 start에 insert 하여도 상관없지만, 크다면 mid + 1을 해줘야 하므로 이는 적절한 답이 아니게 된다.
start <= end의 경우 마지막으로 검사할 값에 대해 start를 +1, 혹은 유지하는 것으로 최종 확인을 거쳐 즉시 원하는 인덱스값을 얻을 수 있게 된다.
```

유명한 알고리즘들을 의심하지 않고 단순하게 외우기만 해서 생겨난 문제인 것 같다.

직접 이를 구현하고 실행해가며 이해해야 비로소 내 것이 되는구나 느꼈다.