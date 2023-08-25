# 122.Best Time To Buy and Sell Stock II

[문제 링크](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description)

매 인덱스 날짜마다 주식의 가격이 적힌 `prices` 배열이 주어진다.

최대 1주를 매수할 수 있고, 원하는 날짜에 해당 날짜의 가격으로 매도할 수 있다.

**같은 날짜에 구매, 판매가 가능하다**

이윤을 최대치로 만들어 리턴하는 문제이다. 

## 접근법

```
1. 현재 인덱스값의 바로 다음 인덱스의 값과 비교하여 그때그때마다 이윤을 남긴다.
    1-1. 예시 속에 답이 나와있다. [7,1,5,3,6,4]라면, 2일차에 사서 3일차에, 4일차에 사서 5일차에 파는 것이 최대이윤이다.
    가장 싼 값에 사서 가장 비싼날 한번 파는 것이 아닌, 오늘보다 내일이 비싸다면 그때그때 팔아야 한다.
2. 같은 날짜에 구매, 판매가 가능하다는 것은, 일단 무조건 사고 내일 더 비싸진다면 팔고 그렇지않으면 오늘 되팔 수 있다는 뜻이다.
```

## 코드

TC - O(n)<br>
SC - O(1)

```
class Solution:
    def maxProfit(self, prices) -> int:
        answer = 0
        for i in range(len(prices)-1):
            answer += max(prices[i+1]-prices[i], 0)
        return answer
```

## 결과

Runtime - Beats 76.8% users<br>
Memory - Beats 59.32% users

## 회고

다양한 방법으로 풀 수 있는 문제지만, 해당 경우에는 모든 경우에서 i-1과 비교하여 더 크다면 판매하는 그리디 풀이법이 가장 퍼포먼스 측면에서 우수했다.

dp 풀이를 한 것이 있어서, 아직 미숙한 dp알고리즘에 익숙해질 겸 코드를 가져왔다.

```
class Solution3:
    def maxProfit(self, prices: List[int]) -> int:
        n=len(prices)
        dp=[[-1, -1] for _ in range(n+1)]
        dp[n][0]=dp[n][1]=0
        for ind in range(n-1,-1,-1):
            for buy in range(2):
                profit=0
                if buy==0:
                    take=-prices[ind]+dp[ind+1][1]
                    not_take=0+dp[ind+1][0]
                    profit=max(take,not_take)
                else:
                    take=prices[ind]+dp[ind+1][0]
                    not_take=0+dp[ind+1][1]
                    profit=max(take,not_take)
                dp[ind][buy]=profit
        return dp[0][0]
```

바텀업 방식으로, 2차원 dp 배열을 선언하여 현재 값을 가졌을 떄와 포기했을 때를 각각 계산하고, 두개를 max함수로 profit을 책정하여 쌓아올리는 방법이다.

해당 문제같은 간단한 조건인 경우에는 이러한 풀이법이 오히려 더 느리지만, 한 주만 매수할 수 있는 것이 아닌 여러 주를 가질 수 있다거나, 사용금액이 한정된다거나 하는 다양한 조건 상에서는 dp알고리즘이 더 빠르게 동작할 것이다.

늘 다양한 풀이법을 염두에 두고 최적의 풀이를 할 수 있도록 노력해야겠다. 