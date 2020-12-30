## 문제 이름

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42895)

### Java

```java
class Solution {
    int answer = 9;
    public int solution(int N, int number) {
        calc(N, number, 0, 0);
        return answer > 8? -1 : answer;
    }
    public void calc(int N, int number, int count, int currentNum){
        if(count > 8){
            return;
        }
        if(number == currentNum){
            answer = Math.min(answer, count);
            return;
        }
        int increasedNum = N;
        for(int i = 1; i <= 8-count; i++){
            calc(N, number, count+i, currentNum+increasedNum);
            calc(N, number, count+i, currentNum-increasedNum);
            calc(N, number, count+i, currentNum*increasedNum);
            calc(N, number, count+i, currentNum/increasedNum);
            increasedNum = increasedNum*10 + N;
        }
    }
}
```

- 소요시간 : 50분

### 접근방법

1. DP 문제이지만 DFS로 접근

2. N, number, count(5의 갯수), currentNum(이전 탐색에서 계산한 값)을 인자로 dfs 검색

3. count가 8보다 클 경우 리턴, number == currentNum일 경우 값 저장 후 리턴

4. 탐색을 계속할 경우 count가 8이 될 때 까지 dfs 검색

   count를 증가시키면서 인자로 받았던 값에 N만으로 이루어진 값을 더해줌

   ```
   count = 0 => 0
   count = 1 => +5 -5 *5 /5
   count = 2 => (count=1의 값) + (+5 -5 *5 /5) // count = 1에서 탐색
                (count=0의 값) + (+55 -55 *55 /55) // count = 0에서 탐색
   ```
