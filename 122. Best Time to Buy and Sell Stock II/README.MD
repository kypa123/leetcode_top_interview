#122.Best Time To Buy and Sell Stock II

[문제 링크](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description)

매 인덱스 날짜마다 주식의 가격이 적힌 `prices` 배열이 주어진다.

최대 1주를 매수할 수 있고, 원하는 날짜에 해당 날짜의 가격으로 매도할 수 있다.

**같은 날짜에 구매, 판매가 가능하다**

이윤을 최대치로 만들어 리턴하는 문제이다. 

##접근법
```
1. 현재 인덱스값의 바로 다음 인덱스의 값과 비교하여 그때그때마다 이윤을 남긴다.
    1-1. 예시 속에 답이 나와있다. [7,1,5,3,6,4]라면, 2일차에 사서 3일차에, 4일차에 사서 5일차에 파는 것이 최대이윤이다.
    가장 싼 값에 사서 가장 비싼날 한번 파는 것이 아닌, 오늘보다 내일이 비싸다면 그때그때 팔아야 한다.
2. 같은 날짜에 구매, 판매가 가능하다는 것은, 일단 무조건 사고 내일 더 비싸진다면 팔고 그렇지않으면 오늘 되팔 수 있다는 뜻이다.
```

##코드
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

##결과
Runtime - Beats 76.8% users<br>
Memory - Beats 59.32% users

##회고
```
```