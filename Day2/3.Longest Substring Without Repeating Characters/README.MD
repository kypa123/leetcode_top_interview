# 3. Longest Substring Without Repeating Characters


[문제 링크](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/?envType=study-plan-v2&envId=top-interview-150)

문자열 `s`가 주어진다

문자열의 단어들이 중복되지 않는 조건에서 가장 긴 부분 문자열을 구해야한다

## 접근법
```
1. deque 라이브러리를 통해 양방향 큐를 활용한다.
2. 문자열을 순회하며, 문자가 큐에 없다면 더해준다.
3. 이미 큐에 존재한다면, max_len 변수를 max(max_len, len(q))를 통해 업데이트해준다.
    3-1. 해당 단어의 인덱스만큼 popleft()를 통해 새로 문자를 받고 기존의 문자를 제거해 업데이트해준다.
```


## 코드

TC - O(n^3)<br>
SC - O(n)

```
from collections import deque
class Solution:    
    def lengthOfLongestSubstring(self, s: str) -> int:
        max_len = 0

        q = deque()
        for i in s:
            if i not in q:
                q.append(i)
            else:
                index = q.index(i)
                for j in range(index + 1):
                    q.popleft()
                q.append(i)
            max_len = max(max_len, len(q))

        return max_len
```

## 결과

Runtime - Beats 59.18% users<br>
Memory - Beats 45.10% users

## 회고

두 가지 개선사항이 필요하다고 느꼈다.
1. if i in q 연산만큼의 n번의 q 순회
2. index만큼의 q.popleft() 연산

해당 연산이 시간복잡도를 크게 증가시키는 요인이라고 생각했고, deque가 아닌 다른 자료구조를 사용해야겠다고 생각했다.
요소 조회, 제거, 추가에 O(1)만큼의 복잡도가 드는 set 자료구조를 사용하면 위의 개선사항을 만족할 수 있다고 생각했다.
또한, 개선사항을 적용하기 위해서는 중복되는 단어를 만났을 때 이전 중복단어까지의 인덱스만큼 단어를 제거해줘야 하므로, 인덱스값이 필요하다.
순차적으로 순회해나가면서, 단어를 만날때마다 0번 인덱스부터 다시 순회하며 해당 단어만큼 제거해주는 두 개의 포인터를 추가 활용하여 문제를 해결했다.

```
class Solution:    
    def lengthOfLongestSubstring(self, s: str) -> int:
        max_len = 0
        check = set()
        left = 0

        for right in range(len(s)):
            if s[right] not in check:
                check.add(s[right])
                max_len = max(max_len, right - left+1)
            else:
                for i in range(left, right):
                    if s[i] == s[right]:
                        left = i+1
                        break
                    else:
                        check.remove(s[i])
        return max_len
```

TC - O(n)<br>
SC - O(n)

