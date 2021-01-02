## 문제 이름

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42626)

### Java

```java
import java.util.PriorityQueue;

class Solution {
    public int solution(int[] scoville, int K) {
        int answer = 0;
        PriorityQueue<Integer> queue = new PriorityQueue<>();
        for(int i=0; i<scoville.length; i++){
            queue.add(scoville[i]);
        }
        while(queue.peek() != null){
            int lowestScoville = queue.remove();
            if(lowestScoville >= K){
                break;
            }
            if(queue.peek() == null){
                return -1;
            }
            int secondLowestScoville = queue.remove();
            queue.add(lowestScoville + secondLowestScoville * 2);
            answer ++;
        }
        return answer;
    }
}
```

-   소요시간 : 15분

### 접근방법

1. 단순하게 LinkedList를 사용해서 매번 연산 때 마다 sort하는 방법

2. Priority Queue를 사용하여 항상 가장 맵지 않은 스코빌 지수를 가진 음식이 나오게 하는 방법

2번이 더 깔끔하고 빠를것 같아서 사용
