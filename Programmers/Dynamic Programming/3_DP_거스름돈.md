## 문제 이름

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12907)

### Java

```java
import java.util.Arrays;
class Solution {
    public int solution(int n, int[] money) {
        int answer = 0;
        int mod = 1000000007;
        int[][] dp = new int[money.length+1][n+1];
        Arrays.sort(money);

        for(int i=0; i<money.length; i++){
            for(int j=1; j<n+1; j++){
                if(j < money[i]){
                    dp[i+1][j] = dp[i][j];
                }else if(j == money[i]){
                    dp[i+1][j] = dp[i][j] + 1;
                }else{
                    dp[i+1][j] = dp[i][j] + dp[i+1][j-money[i]];
                }
            }
        }
        return dp[money.length][n] % mod;
    }
}
```

- 소요시간 : 70분

### 접근방법

|       | 1   | 2   | 3   | 4   | 5   |
| ----: | --- | --- | --- | --- | --- |
| **1** | 1   | 1   | 1   | 1   | 1   |
| **2** | 1   | 2   | 2   | 3   | 3   |
| **5** | 1   | 2   | 2   | 3   | 4   |

`dp[i][j] = dp[i-1][j] + dp[i]j-money[i-1]]`

=> 가격으로 정렬된 동전의 i까지의 사용해서 j원을 만들 수 있는 가지의 수

예를 들어, `dp[1][4]` 는 2원까지 사용 (1, 2원 사용)해서 4원을 만드는 방법의 갯수 이다.

방법의 개수를 구하기 위한 경우의 수를 나누면

1. 사용할 동전의 값보다 현재 값 (j)이 더 작을 때

   예를 들어, 5원 까지 사용해서 2원의 거스름돈을 주는 경우이므로 5원을 사용 안했을 때의 개수가 그대로 반영된다.

   `dp[i+1][j] = dp[i][j];`

2. 사용할 동전의 값과 현재 값이 같을 때

   예를 들어, 5원 까지 사용해서 5원의 거스름돈을 주는 경우이므로 5원 이전 동전까지 사용했을 때의 개수보다 1개 더 늘어난다.

   `dp[i+1][j] = dp[i][j] + 1;`

3. 사용할 동전의 값보다 현재 값 (j)가 더 클 때

   예를 들어, 5원의 동전으로 7원의 거스름돈을 주는 경우이다.

   이 때 경우의 수는 5원 이전 동전까지 사용했을 때의 개수 + 5원을 사용했을 때 (7-5)원의 개수이다.

   `dp[i+1][j] = dp[i][j] + dp[i+1][j-money[i]];`
