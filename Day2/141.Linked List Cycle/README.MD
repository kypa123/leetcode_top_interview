# 141. Linked List Cycle


[문제 링크](https://leetcode.com/problems/linked-list-cycle/submissions/1032668283/?envType=study-plan-v2&envId=top-interview-150)



## 접근법

단방향 연결리스트의 head가 주어진다

해당 연결리스트가 순횐되는지 여부를 체크하여야 한다

Floyd's tortoise and hare 알고리즘을 활용하여, 연결리스트에 순환이 이루어지는지 체크해주었다

해당 알고리즘을 사용한다면, 순환의 시작점까지 특정할 수 있지만

해당 문제는 순환의 존재여부만을 확인하면 되니 필요없다

## 코드
TC - O(n)<br>
SC - O(1)

```
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        if not head or not head.next:
            return False
        
        tort = hare = head
        while hare and hare.next:
            tort = tort.next
            hare = hare.next.next
            if tort == hare:
                return True
        return False
```

## 결과

Runtime - Beats 85.86% users<br>
Memory - Beats 24.12%

## 회고

처음으로 head.next 혹은 head가 null인 가능성은 사실상 while문의 조건상으로도 검사할 수 있는 부분이다. 

따라서 처음의 조건을 제거하여 좀 더 간결한 코드가 될 수 있도록 리팩토링하였다.

```
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        tort = hare = head
        while hare and hare.next:
            tort = tort.next
            hare = hare.next.next
            if tort == hare:
                return True
        return False
```