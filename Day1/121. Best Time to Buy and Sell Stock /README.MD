# 121.Best Time to Buy and Sell Stock

[문제 링크](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

배열 `prices`가 주어진다. 각 원소는 해당 인덱스값의 날짜의 주식 가격을 나타낸다.

한 번의 매수와 매를 통해 얻을 수 있는 최고의 이윤을 계산해야 한다.

## 접근법

```
1. minPrice, maxProfit 변수를 선언해 매 순회마다 최소값, 최대이윤을 업데이트해준다.
2. 현재 원소가 minPrice보다 더 작다면 minPrice를 업데이트해준다.
3. 현재 원소가 minPrice보다 더 크다면, curr - minPrice가 현재 가질 수 있는 이윤이 된다.
    3-1. 이를 maxProfit과 비교하여, max(maxProfit, curr-minProce)를 하여 업데이트해준다.
```

## 코드

TC - O(n)<br>
SC - O(1)

```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        minPrice = 10001
        maxProfit = 0
        for i in range(len(prices)):
            if prices[i] < minPrice:
                minPrice = prices[i]
            else:
                maxProfit = max(maxProfit, prices[i] - minPrice)
                
        return maxProfit
```

## 결과

Runtime - Beats 71.99% users<br>
Memory - Beats 59.83% users

## 회고

if 조건문을 통해 매 순회마다 max, min 조건을 검사하지 않도록 짰다.

솔루션에서는 실제로 순회마다 max, min 연산을 통해 값을 도출하는 코드들이 많이 있었는데,

분기문을 통해 먼저 조건을 검사함으로서 메모리, 런타임 퍼포먼스를 이길 수 있어서 뿌듯했다.