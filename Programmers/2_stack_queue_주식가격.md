## 문제 이름

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42584)

### Java

### 풀이1 - 2중 반복문

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

### 풀이2 - Stack

```java
import java.util.Stack;
class Stock {
    int time;
    int price;
    Stock(int time, int price){
        this.time = time;
        this.price = price;
    }
    public String toString(){
        return "["+time+", "+price+"]";
    }
}
class Solution {
    public int[] solution(int[] prices) {
        int priceLength = prices.length;
        int answer[] = new int[priceLength];
        Stack<Stock> priceStack = new Stack<>();
        for(int i=0; i<priceLength; i++){
            answer[i] = priceLength - i - 1;
        }
        for(int i=0; i<priceLength; i++){
            //stack size가 0일 경우, 가격이 상승했을 경우 삽입
            if(priceStack.size() <= 0 || priceStack.peek().price <= prices[i]){
                priceStack.push(new Stock(i, prices[i]));
            }else{
                while(true){
                    //stack이 비어있지 않고
                    if(priceStack.size() <= 0) break;
                    Stock stock = priceStack.peek();
                    int time = stock.time;
                    int price = stock.price;
                    //가격이 하락했을 경우
                    if(price > prices[i]){
                        //정답 배열에 현재 시간 - 삽입 시간을 넣어줌
                        answer[time] = i - time;
                        //stock
                        priceStack.pop();
                    }else{
                        break;
                    }
                }
            }
        }
        return answer;
    }
}
```

- 풀이 실패 (이유를 모르겠음....)
