# 155. Min Stack

[문제 링크](https://leetcode.com/problems/min-stack/description/?envType=study-plan-v2&envId=top-interview-150)

`MinStack` 클래스의 스켈레톤 코드가 주어진다.

push, pop, top, getMin 메소드를 구현해야 한다.

모든 메소드는 O(1)의 시간복잡도를 가져야 한다.

## 접근법

1. push, pop, top은 기본 스택 자료구조를 구현하듯 만들어준다. init함수에 array를 선언하고 이를 스택으로 사용한다.
2. getMin 메소드는 스택 내부의 최소값을 반환하는 메소드이다. 이를 O(1)의 복잡도로 구현하기 위해서는 3가지 방법이 생각났다.
   - 매 원소마다 현재 위치까지의 최소값을 저장한다
   - 클래스 내부에 힙을 추가 선언해서 최소값을 저장한다
   - 스택을 2개를 두고, 매 원소마다 최소값을 최소값 스택에 집어넣는다
3. 첫 번째 방법으로 구현하였다.

## 코드
TC - O(n)<br>
SC - O(n)

```
class MinStack:

    def __init__(self):
        self.stack = []

    def push(self, val: int) -> None:
        self.stack.append(val)

    def pop(self) -> None:
        self.stack.pop()

    def top(self) -> int:
        if len(self.stack) > 0:
            return self.stack[len(self.stack) - 1]

    def getMin(self) -> int:
        return min(self.stack)
```

## 결과

Runtime - Beats 10.90% users<br>
Memory - Beats 88.2% users


## 회고

시간복잡도를 개선하기 위해서는 최소 스택을 추가 선헌하는 방법이 더 빠르다.

하지만 해당 방법을 채택하게 되면, 메모리 사용량이 높아져 하위 50%로 내려가게 된다.

정답은 없지만, 각 상황에 따라 올바른 코드를 짜야할 것 같다.

아래는 최소 스택을 추가 선언한 코드이다.


```
class MinStack:

    def __init__(self):
        self.stack = []
        self.minStack = []

    def push(self, val: int) -> None:
        self.stack.append(val)
        if self.minStack:
            val = min(self.minStack[-1],val)
        self.minStack.append(val)

    def pop(self) -> None:
        self.stack.pop()
        self.minStack.pop()

    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return self.minStack[-1]
```