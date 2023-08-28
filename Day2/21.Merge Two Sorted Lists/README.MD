# 21. Merge Two Sorted Lists

[문제 링크](https://leetcode.com/problems/merge-two-sorted-lists/)

2개의 정렬된 단방향 연결리스트, `list1`과 `list2`가 주어진다.

각 노드를 순회하며 크기에 맞는 순서대로 병합하고, 이를 리턴해야 한다.

## 접근법

```
1. 새로운 연결리스트 노드를 생성하고, 연결리스트를 순회하며, 각 값을 비교한다.
2. 더 작은 값을 처음 초기화한 노드.next에 할당해주며, 해당 리스트만 list.next를 해준다.
3. 두 연결리스트가 모두 순회를 마치면, 결과를 리턴한다. 
```

## 코드
TC - O(n)<br>
SC - O(1)

```
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        head = ListNode(-1)
        cursor = head
        while list1 != None and list2 != None:
            if list1.val < list2.val:
                cursor.next = list1
                list1 = list1.next
            else:
                cursor.next = list2
                list2 = list2.next
            cursor = cursor.next
        if list1 == None:
            cursor.next = list2
        else:
            cursor.next = list1
        
        return head.next
```

## 결과

Runtime - Beats 5.97% users<br>
Memory - Beats 100% users


## 회고

처음으로 연결리스트 자료구조를 활용한 문제에서 Solution 탭의 우수한 답변들과 크게 다르지 않은 코드를 짜내어서 뿌듯했다