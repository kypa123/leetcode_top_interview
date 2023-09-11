# 208. Implement Trie (Prefix Tree)

[문제 링크](https://leetcode.com/problems/implement-trie-prefix-tree/description/?envType=study-plan-v2&envId=top-interview-150)

`Trie` 클래스의 스켈레톤 코드가 주어진다.

이를 완성하라.



## 접근법

1.  배열을 선언하고 `insert`, `search`, `startsWith`를 구현해준다.
2. `startsWith`같은 경우, 단어의 시작점이 `prefix`와 같아야만 함으로 이를 유념해서 구현해준다.

## 코드

TC - O(n)<br>
SC - O(n)

```
class Trie:

    def __init__(self):
        self.array = []

    def insert(self, word: str) -> None:
        self.array.append(word)

    def search(self, word: str) -> bool:
        return word in self.array

    def startsWith(self, prefix: str) -> bool:
        l = len(prefix)
        for word in self.array:
            if len(word) >= l and word[:l] == prefix:
                return True
        return False
```

## 결과

Runtime - Beats 5.01% users<br>
Memory - Beats 22.96% users


## 회고

가장 직관적인 방식으로 문제를 풀었다. 

결과적으로 문제를 빠르게 고민없이 해결할 수 있었으나, 문제의 취지는 Trie 자료구조를 실제로 구현하는 것이라고 생각하여 관련 Soluion을 찾아보고, 내 것으로 만들고자 하였다.

여러개의 `TrieNode`를 Python3의 `Dictionary` 자료구조를 활용해 해시맵의 형태를 선언해주었다.

각 레벨이 증가할 떄마다 TrieNode.children:TrieNode.children 의 형식으로 상위에서 하위 소유형태를 나타내주었다.

```
class TrieNode:
    def __init__(self):
        self.children = {}
        self.end_char = False
class Trie:
    def __init__(self):
        self.root = TrieNode()
    def insert(self, word: str) -> None:
        curr = self.root
        for c in word:
            if c not in curr.children:
                curr.children[c] = TrieNode()
            curr = curr.children[c]
        curr.end_char = True

    def search(self, word: str) -> bool:
        curr = self.root
        for c in word:
            if c not in curr.children:
                return False
            curr = curr.children[c]
        return curr.end_char        

    def startsWith(self, prefix: str) -> bool:
        curr = self.root
        for c in prefix:
            if c not in curr.children:
                return False
            curr = curr.children[c]
        return True       
```

이런 방식으로 짜게 되면, 단일 배열을 선언한 방법보다 훨씬 많은 메모리가 필요하게 되나, 매 해시맵의 키워드를 검색하는 데 O(1)의 시간복잡도를 가지게 된다.

