## 문제 이름

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42628)

### Java

```java
import java.util.LinkedList;
import java.util.Collections;

class Solution {
    public int[] solution(String[] operations) {
        LinkedList<Integer> doublyPriorityQueue = new LinkedList<>();
        for(String operation: operations){
            String[] operationInput = operation.split(" ");
            String operator = operationInput[0];
            int value = Integer.parseInt(operationInput[1]);
            if(operator.equals("I")){
                doublyPriorityQueue.add(value);
            }else if(doublyPriorityQueue.size() > 0){
                if(value == -1){
                    doublyPriorityQueue.remove(0);
                }else{
                    doublyPriorityQueue.remove(doublyPriorityQueue.size()-1);
                }
            }
            Collections.sort(doublyPriorityQueue);
        }
        if(doublyPriorityQueue.size() == 0){
            int[] result = {0, 0};
            return result;
        }else{
            int[] result = {doublyPriorityQueue.get(doublyPriorityQueue.size()-1), doublyPriorityQueue.get(0)};
            return result;
        }
    }
}
```

-   소요시간 : 15분

### 접근방법

1. 데이터가 저장된 자료구조에서 가장 큰 값, 가장 작은 값을 삭제할 수 있어야 한다.

2. PriorityQueue를 생각했지만 트리구조에서는 최댓값 최솟값 중 한개만 빠르게 얻을 수 있으므로 배열 형태의 자료구조를 선택

3. LinkedList에 삽입하고 매번 정렬하면 시간 초과가 날것 같았는데 일단 구현해봤더니 통과했다.
