## 문제 이름

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42584)

### Java

```java
class Solution {
    public int[] solution(int[] prices) {
        int priceLength = prices.length;
            int answer[] = new int[priceLength];
        for(int i=0; i<priceLength; i++){
            answer[i] = priceLength - i - 1;
        }
        for(int i=0; i<priceLength; i++){
            for(int j=i+1; j<priceLength; j++){
                if(prices[i] > prices[j]){
                    answer[i] = j-i;
                    break;
                }
            }
        }
        return answer;
    }
}
```

- 소요시간 : 10분

### 접근방법

1. 시간 복잡도 최악의 경우 O(n<sup>2</sup>) 이지만 break가 걸려있으므로 2중 포문을 시도

2. 처음에 가격이 끝까지 내려가지 않는다는 조건으로 `배열의 길이 - index`로 배열 초기화

3. 이후 배열을 순회하며 가격이 처음 내려갔을 때의 index를 이용하여 가격 유지 기간 측정
