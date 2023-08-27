# 2. Add Two Numbers


[문제 링크](https://leetcode.com/problems/add-two-numbers/description/?envType=study-plan-v2&envId=top-interview-150)

2개의 단방향 연결리스트, `l1`과 `l2`가 주어진다.

각각의 연결리스트 노드는 하나의 정수의 1, 10, 100, ... 의 단위를 역방향으로 한 개씩 가지고 있다. ex) 234 = 4 -> 3 -> 2

두 개의 단방향 리스트의 정수를 더한 값을 각각 노드가 역방향으로 한 단위씩 담은 형태를 리턴해야 한다.

ex) 2 -> 4 -> 3, 5 -> 6 -> 4 는 342, 465를 더한 807을 7 -> 0 -> 8 의 연결리스트의 형태로 리턴해야 한다.

## 접근법

```
1. 주어진 l1, l2에 대한 순회를 하며 매번 순회할 때마다 단위를 10씩 곱해준다.
2. l1, l2.next가 None이 아닐때까지 루프를 돌아주며 각 값들을 total에 더해나간다.
3. total이 구해졌다면, 이를 string형변환 해 -1 인덱스부터 0번인덱스까지 순회를 돌아준다.
4. 순회를 돌며, 값을 연결리스트의 노드에 하나씩 할당해준다
```

## 코드

TC - O(n+m)<br>
SC - O(n+m)

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        head = ListNode(-1)
        l3 = head
        total = 0
        count = 1
        while l1 != None or l2 != None:
            val1 = l1.val if l1 is not None else 0
            val2 = l2.val if l2 is not None else 0
            total += (val1 + val2) * count
            count *= 10

            l1 = l1.next if l1 is not None and l1.next is not None else None
            l2 = l2.next if l2 is not None and l2.next is not None else None

        total = str(total)

        for i in range(len(total)-1, -1, -1):
            l3.next = ListNode(total[i])
            l3 = l3.next
        return head.next
```

## 결과

Runtime - Beats 46.46% users<br> 
Memory - Beats 63.67% users

## 회고

연결리스트 자료구조에 대한 이해도가 부족하다고 느꼈다.

2번의 루프로 나뉘어 한 번은 총합을 구하고, 한 번은 이를 역순으로 순회하며 연결리스트를 만드는 과정을 거치고 있다.

Solution 탭을 통해 연결리스트 자료구조를 잘 다룬 코드를 많이 찾아보았고, 대부분 한 번의 루프를 통해 결과를 처리하고 있었다.

코드는 다음과 같다.

```
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        dummyHead = ListNode(0)
        tail = dummyHead
        carry = 0

        while l1 is not None or l2 is not None or carry != 0:
            digit1 = l1.val if l1 is not None else 0
            digit2 = l2.val if l2 is not None else 0

            sum = digit1 + digit2 + carry
            digit = sum % 10
            carry = sum // 10

            newNode = ListNode(digit)
            tail.next = newNode
            tail = tail.next

            l1 = l1.next if l1 is not None else None
            l2 = l2.next if l2 is not None else None

        result = dummyHead.next
        dummyHead.next = None
        return result
```

내 코드와 비교했을 때 우월한 점은 다음과 같다.

- 한 번의 루프를 통해 현재 단위의 값을 계산하고, 그때마다 정답 연결리스트의 노드를 초기화하고 있다.
- 루프에서의 남는 값을 다음 값에 더함으로서 단위에 계속해서 *10을 해주지 않아 다루는 숫자크기가 작아 불필요한 큰 연산이 필요없어진다.
  - constraint에 연결리스트의 최대 길이는 명시되어 있지 않으나, 숫자가 기하급수적으로 커진다면 나의 풀이는 메모리 초과가 날 우려가 있다.
- 불필요한 l1 is not none and l1.next is not none 조건문을 거치지 않는다.

자료구조에 대해 좀 더 많이 공부해야겠다고 느꼈다. 적절한 자료구조를 알고리즘에 맞게 선택했더라도 이를 다룰 줄 모르면 아무 의미가 없다.