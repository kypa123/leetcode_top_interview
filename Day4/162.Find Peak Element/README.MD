# 162. Find Peak Element


[문제 링크](https://leetcode.com/problems/find-peak-element/description/?envType=study-plan-v2&envId=top-interview-150)

`peak element`란, 양옆의 원소보다 큰 원소를 말한다.

`nums` 배열이 주어지며, 배열 속의 `peak element` 를 찾아 반환해야 한다.

3가지 조건이 주어진다.

1. -1번 인덱스 혹은 배열 길이보다 큰 값은 **언제나 옆 원소보다 더 작다고 판단한다.**
2. 양옆의 값은 같지 않다.
3. 정답은 여러개다. 그중 아무거나 반환해도 괜찮다.


## 접근법

1. 배열의 길이가 1이거나, 0번 인덱스의 값이 1번 인덱스보다 크다면 0을 리턴한다.
2. 마지막 원소의 값이 마지막 원소의 값 -1보다 크다면 배열의 길이-1 를 반환한다. 0 인덱스 배열이기 때문
3. 아니라면, 1번 인덱스부터 순회하며 양옆의 인덱스의 값보다 값이 크다면 인덱스를 반환한다.


## 코드
TC - O(n)<br>
SC - O(1)

```
class Solution:
    def findPeakElement(self, nums: List[int]) -> int:
        if len(nums) == 1 or nums[0] > nums[1]:
            return 0
        if nums[-1] > nums[-2]:
            return len(nums)-1
        
        for i in range(1, len(nums)-1):
            if nums[i-1] < nums[i] and nums[i+1] < nums[i]:
                return i
```

## 결과

Runtime - Beats 99.53% users<br>
Memory - Beats 61.44% users


## 회고

문제를 읽는 즉시 O(n)의 복잡도의 해결법으로 풀었다.

하지만 문제의 끝부분에 O(log n)의 시간복잡도로 풀어야 한다는 요구를 뒤늦게 읽게 되었고,

discussion 탭의 장문의 일침을 읽게 되었다.

```
When people see ths question, I think most people will immediately come up with the linear search solution,
which is to examine each num and compare it with its two neighbours. 
No braniner, right? Then people are thinking why this kind of question would appear in the question pool and why it's even rated as Medium. 
Then they might go to the Solution tab and see someone writing up a big article explaining a better solution and probably think, why bother? 
That's an overkill.

These types of questions are so undervalued by people. 
And these are the questions we should pay more attention to. 
I'm sure in a real question, the interviewer will not be satisfied by the linear solution. 
Why? Because the straightforward linear scan solution isn't using all of the clues given in the question. 
These clues, including

1. No adjacent two numbers are the same
2. the two end of the arrays are -∞
3. You can return any peak.

are all the clues that we can base upon to get to the final BS solution. 
When you are reading a question, pay great attention to these clues. 
If your solution does not involve all of the clue provided, you might not get the optimal solution. 
This is not any random question, it's asked by Facebook, Google, etc., for multiple times. 
There is a reason why it exist and please don't downvote it without even attempting to understand it.
```

요는 해당 문제를 100% 이해하고 풀었다고 말하기 위해선, 주어진 3가지 조건을 만족하며 O(log n)의 복잡도를 통한 풀이를 충분한 고민끝에 도출했는가?

그렇지 않다면, 너는 성급하며 충분한 생각을 거치지 않고 답을 도출하는, Google과 Facebook같은 저명한 회사에서는 절대 납득하지 않을 풀이를 도출한 것이라는 뜻이었다.

내가 뭘 놓치고있을까? 3가지 조건중 첫 번째 조건만 만족한 결과를 도출한 것이 문제라고 생각했다.

`양옆의 값은 같지 않다`, `정답은 여러개이며, 그중 하나만 반환해도 된다`, `O(log n)의 시간복잡도를 가져라`의 조건을 충족해야 한다고 생각했다.

시간복잡도 O(log n)을 충족하기 위해서는 이분탐색을 진행하는 것이 답을 도출하는 방법인가 하는 생각이 들었다.

하지만 내가 알기로는 이분탐색은 sort 상태의 배열에만 사용할 수 있는 것이라고 생각했는데 

solution 탭을 들어가보니 실제로 이분탐색을 활용한 풀이들이 많이 존재했으며, 이것이 곧 정답인 것처럼 적혀있었다.

솔직히 이해가 완전히 가지는 않는다. 절반의 왼쪽에만 값이 존재하고 오른쪽엔 존재하지 않는 경우, 이분탐색으로 오른쪽을 탐색하게 된다면 답이 나오지 않을 수도 있지 않은가?

아직까지도 완벽히 이해하진 못하겠지만, 이분탐색을 사용한 정답코드는 다음과 같다.

```
class Solution:
    def findPeakElement(self, nums: List[int]) -> int:
        if len(nums) == 1:
            return 0

        left = 0
        right = len(nums)-1
        while left <= right:
            mid = (left+right) // 2
            if ( mid == 0 or nums[mid] >= nums[mid-1] ) and ( mid == len(nums)-1 or nums[mid] >= nums[mid+1] ) :
                return mid
            elif nums[mid] <= nums[mid+1]:
                left = mid+1
            else:
                right = mid-1
        return -1
```