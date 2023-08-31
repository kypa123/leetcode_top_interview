# 150. Evaluate Reverse Polish Notation


[문제 링크](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

문자열 배열 `tokens` 가 주어진다.

해당 배열은 문자열 형태의 숫자, 그리고 수학 연산자 `+`, `-`,`*`,`/` 가 존재한다.

해당 배열은 후위 표기법을 표현한 수학 연산식이며, 이를 계산한 값을 반환해야 한다.

## 접근법
```
1. 스택을 활용하여, 숫자를 만나면 숫자 배열에 이를 쌓아주고, 연산자를 만나면 숫자배열에서 2개를 pop해 연산하고 다시 넣는다.
2. 이를 반복한다.
```


## 코드
k를 연산자의 개수라고 했을 때

TC - O(n + k)<br>
SC - O(n)

```
class Solution:
    def calculator(self, oper, num1, num2):
        if oper == '+':
            return num1 + num2
        elif oper == '-':
            return num1 - num2
        elif oper == '*':
            return num1 * num2
        elif oper == '/':
            return int(num1 / num2)
        
    def evalRPN(self, tokens: List[str]) -> int:
        numarr = []
        operator = []
        for token in tokens:
            try:
                numarr.append(int(token))
            except ValueError:
                num2, num1 = numarr.pop(), numarr.pop()
                numarr.append(self.calculator(token, num1, num2))
                
        return numarr[-1]
```

## 결과

Runtime - Beats 90.30% users<br>
Memory - Beats 50.73% users

## 회고

솔루션 클래스 내부에 함수를 추가 선언함으로서 풀이했다. 

다른 풀이로는 `['+','-','*','/]` 배열을 선언한다던가 

operators 딕셔너리로 람다 함수를 저장한다던가 하는 다양한 방법이 있었다.

`operators = {
            '+': (lambda x, y: operator.add(x, y)),
            '*': (lambda x, y: operator.mul(x, y)),
            '/': (lambda x, y: int(x / y)),
            '-': (lambda x, y: operator.sub(x, y)),
        }`

성능적인 차이는 크게 존재하지 않고, 가독성을 위해 메소드를 따로 선언한 나의 방법이 나쁘지 않은 것 같다고 느껴 리팩토링은 진행하지 않았다.