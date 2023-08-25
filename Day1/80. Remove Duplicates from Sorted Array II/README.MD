# 80.Remove Duplicates from Sorted Array II

[문제 링크](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/?envType=study-plan-v2&envId=top-interview-150)

정렬된 배열 `nums`가 주어진다. in-place 알고리즘을 사용하여 추가적인 메모리 없이 각 원소별로 **최대 2번**만 등장하도록 해야한다.

조건에 맞는 원소들의 갯수를 모두 합해 리턴해야 하고, 리턴한 값 만큼의 `nums`배열의 인덱스까지가 중복을 제거한 형태를 띠어야 한다.

ex) [1,1,1,2,2,2,3,3,3,3] -> [1,1,2,2,3,3,?,?], return 6

즉 리턴받는 정답인 6번째 인덱스까지는 중복을 제거한 모습이어야 한다. 그 이후의 인덱스의 값은 상관없다.

## 접근법

```
1. 0번째 인덱스부터 카운팅하여 증가할 i변수, 추가적으로 중복여부를 확인할 flag 변수를 선언헀다.
2. 1번째 인덱스부터 순회하며, 현재 인덱스번째 값이 i인덱스의 값과 같다면,
    2-1. flag가 false라면(현재값은 아직 중복되지 않았다) i += 1, nums[i] = nums[j]로 업데이트해주며, flag = True
    2-2. flag가 true라면(현재 값은 이미 중복) 업데이트는 일어나지 않는다.
3. i번째 인덱스의 값과 순회값이 다르다면 i += 1로 업데이트해주며, flag를 false로 초기화해준다.
```

## 코드

TC - O(n)<br>
SC - O(1)

```
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        i = 0
        flag = False
        for j in range(1, len(nums)):
            if nums[j] == nums[i]:
                if not flag:
                    i += 1
                    nums[i] = nums[j]
                    flag = True
            else:
                flag = False
                i += 1
                nums[i] = nums[j]
        return i+1
        
```

## 결과

Runtime - Beats 89.59% users<br>
Memory - Beats 14.46% users

## 회고

flag라는 변수를 추가 선언함으로 풀이를 했지만, 상대적으로 메모리사용량이 늘어나 순위 분포도가 크게 밀렸다.

추가 변수를 선언하지 않고도 분명 풀이법이 존재할 것이라 생각했고, 그중 가장 깔끔한 풀이법을 찾아보았다.

```
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        ans=2
        for i in range(2,len(nums)):
            if nums[i]!=nums[ans-2]:nums[ans]=nums[i];ans+=1
        return ans
```

위의 풀이법은 정말 단순하게도 카운트하던 인덱스의 값 -2와 비교하여 2개 이상의 중복이 존재하는지를 체크하여 상위 1퍼센트의 메모리를 기록했다.

간단명료한 코드를 짜내는 것은 어떻게보면 재능의 영역이라고 생각하지만, 이런 좋은 코드들을 많이 보다보면 조금은 닮아나갈 수 있지 않을까 하는 희망을 품어본다.