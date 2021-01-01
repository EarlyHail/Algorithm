## 문제 이름

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42885)

### Java

```java
import java.util.Arrays;
class Solution {
    public int solution(int[] people, int limit) {
        Arrays.sort(people);
        int answer = 0;
        int front = 0;
        int rear = people.length - 1;
        while(front <= rear){
            int boatWeight = people[rear];
            while(boatWeight <=limit){
                boatWeight += people[front];
                front ++;
            }
            front--;
            rear--;
            answer++;
        }
        return answer;
    }
}
```

- 소요시간 : 10분

### 접근방법

1. 가장 무거운 사람을 추가 하고, 가장 가벼운 사람을 보트의 한계 무게가 넘기 전까지 계속 추가한다.
