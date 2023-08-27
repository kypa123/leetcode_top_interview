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

Runtime - Beats 73.14% users<br>
Memory - Beats 12.25% users

## 회고

코드가 좀 난잡하다는 생각이 들었고, 개선사항을 적용하고자 하였다.

개선사항은 다음과 같다.

- 의미없는 flag를 제거하고, 조건이 맞지 않는다면 즉시 false를 리턴
- replace가 아닌, 전체코드를 검사하여 공백, 특수문자 등 불필요한 요소를 제거한 문자열을 생성
- 문자열을 순회하는 것이 아닌, 슬라이싱을 통해 거꾸로 뒤집고 원본과 같은지 확인. [::-1] 연산은 문자열을 뒤집는 가장 빠른 built-in 함수이기 때문

개선사항을 적용한 코드는 다음과 같다.

```
class Solution:
    def isPalindrome(self, s: str) -> bool:
        s = ''.join([word.lower() for word in s if word.isalnum()])
        if s == s[::-1]:
            return True
        return False
```

코드가 훨씬 간결해졌고, 메모리를 조금 더 사용하여 Runtime을 Beats 98.59% 로 끌어올릴 수 있었다.

문자열을 순회하며 공백, 특수문자를 제거한 리스트를 만든 뒤 이를 다시 join하여 문자열을 만드는 과정에서 메모리를 더 사용한 것이다.

리스트를 만들고 join하는 과정을 개선하자면, list를 만드는 것이 아닌 새로운 string으로 처음부터 만들면 된다. 코드는 다음과 같다.

```
class Solution:
    def isPalindrome(self, s: str) -> bool:
        string=''
        for word in s.lower():
            if word.isalnum():
                string += word
        if string == string[::-1]:
            return True
        return False
```

Runtime - Beats 98.11% users<br>
Memory - Beats 86.77% users