# 125.Valid Palindrome

[문제 링크](https://leetcode.com/problems/valid-palindrome/?envType=study-plan-v2&envId=top-interview-150)

문자열 `s`가 주어지며, 해당 문자열이 Palindrome인지 여부를 리턴한다.

Palindrome이란, 공백을 제외한 문자열을 역방향으로 읽어도 정방향으로 읽은것과 같은 문자를 말한다.

## 접근법

```
1. 투 포인터 알고리즘을 활용해, start = 0, end = len(s)-1로 각각 시작과 끝 인덱스를 지정해준다.
2. while문을 통해 각 인덱스의 값이 서로 같은지를 확인하며, 아니라면 순회를 즉시 종료하고 False를 리턴한다.
3. 끝까지 순회를 마쳤다면 True를 리턴한다
```

## 코드

TC - O(n)<br>
SC - O(1)

```
class Solution:
    def isPalindrome(self, s: str) -> bool:
        s.replace(" ", '')
        s.lower()
        start = 0
        end = len(s)-1
        flag = False
        while start < end:
            if s[start] != s[end]:
                flag = True
                break
            start += 1
            end -= 1
        if flag:
            return False
        return True
```

## 결과


## 회고

```
```