#80.Remove Duplicates from Sorted Array II

[문제 링크](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/?envType=study-plan-v2&envId=top-interview-150)

정렬된 배열 `nums`가 주어진다. in-place 알고리즘을 사용하여 추가적인 메모리 없이 각 원소별로 **최대 2번**만 등장하도록 해야한다.

조건에 맞는 원소들의 갯수를 모두 합해 리턴해야 하고, 리턴한 값 만큼의 `nums`배열의 인덱스까지가 중복을 제거한 형태를 띠어야 한다.

ex) [1,1,1,2,2,2,3,3,3,3] -> [1,1,2,2,3,3,?,?], return 6

즉 리턴받는 정답인 6번째 인덱스까지는 중복을 제거한 모습이어야 한다. 그 이후의 인덱스의 값은 상관없다.

##접근법
```
1. 0번째 인덱스부터 카운팅하여 증가할 i변수, 추가적으로 중복여부를 확인할 flag 변수를 선언헀다.
2. 1번째 인덱스부터 순회하며, 현재 인덱스번째 값이 i인덱스의 값과 같다면,
    2-1. flag가 false라면(현재값은 아직 중복되지 않았다) i += 1, nums[i] = nums[j]로 업데이트해주며, flag = True
    2-2. flag가 true라면(현재 값은 이미 중복) 업데이트는 일어나지 않는다.
3. i번째 인덱스의 값과 순회값이 다르다면 i += 1로 업데이트해주며, flag를 false로 초기화해준다.
```

##코드
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

##결과
Runtime - Beats 89.59% users
Memory - Beats 14.46% users

##회고
```
```