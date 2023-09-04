# 148. Sort List


[문제 링크](https://leetcode.com/problems/sort-list/?envType=study-plan-v2&envId=top-interview-150)

인결리스트의 head, `head`가 주어진다.

해당 연결리스트를 정렬 후 리턴해야 한다.

## 접근법

1. 우선 arr에 연결리스트를 순회하며 값을 모두 담고, 이를 sort한다.

2. arr를 순회하며 새로운 연결리스트를 만들고, 이를 리턴한다

## 코드
TC - O(2n + nlog n)<br>
SC - O(2n)

```
class Solution:
    def sortList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        arr = [] 
        while head != None:
            arr.append(head.val)
            head = head.next
        arr.sort()
        nd = ListNode(0)
        hd = nd
        for a in arr:
            nd.next = ListNode(a)
            nd = nd.next
        return hd.next
```

## 결과

Runtime - Beats 84.25% users<br>
Memory - Beats 22.68% users


## 회고

이번 문제는 오랜 시간 고민했지만 효율적인 방법을 생각해낼 수 없었다.

Solution 탭을 확인하고 정리가 잘 되어있는 코드들을 여러개 확인했고, 연결리스트는 분할정복 기법으로 정렬할 수 있다는 것을 알 수 있었다.

Array를  활용한 sort 구현은 할 수 있지만 연결리스트라는 자료구조를 직접 다뤄볼 기회가 많지 않아 다소 생소했던 것 같다.

아래는 가장 깔끔하다고 생각하는 Merge Sort 코드이다. 이를 여러번 확인하며 내 것으로 만들어야겠다.

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def divide(self,head):
        slow,fast=head,head.next
        while fast and fast.next:
            slow=slow.next
            fast=fast.next.next
        return slow
    
    def Merge(self,l,r):
        temp=ans=ListNode()
        while l and r:
            if l.val<=r.val:
                temp.next=l
                l=l.next
            else:
                temp.next=r
                r=r.next
            temp=temp.next
        if l:
            temp.next=l
        if r:
            temp.next=r
        return ans.next
            
    def sortList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head or not head.next:
            return head
        left=head
        right=self.divide(head)
        temp=right.next
        right.next=None
        right=temp
        left=self.sortList(left)
        right=self.sortList(right)
        return self.Merge(left,right)
```