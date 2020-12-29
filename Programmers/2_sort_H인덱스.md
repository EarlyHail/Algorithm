## 문제 이름

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42747)

### Java

```java
import java.util.Arrays;

class Solution {
    public int solution(int[] citations) {
        int hIndex = 0;
        Arrays.sort(citations);
        for(int i=0; i<citations.length; i++){
            if(citations[i] > citations.length - i){
                hIndex = citations.length - i;
                break;
            }
        }
        return hIndex;
    }
}
```

- 소요시간 : 5분

### 접근방법

1. 문제를 간단하게 쓰면 길이가 n인 숫자의 배열에서 h보다 큰 값이 h개 이상 있을 때의 h를 찾는 문제이다.

2. 배열을 정렬하고 `i번째 원소`가 `n - i`의 값 보다 커지는 순간의 `n - 1`의 값이 `h`이다.
