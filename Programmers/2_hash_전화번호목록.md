## 문제 이름

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42577?language=java)

### java

```java
class Solution {
    public boolean solution(String[] phoneBook) {
        boolean answer = true;
        int bookLength = phoneBook.length;
        for(int i=0; i<bookLength; i++){
            for(int j=0; j<bookLength; j++){
                if(i == j || phoneBook[j].length() < phoneBook[i].length()) continue;
                if(phoneBook[j].startsWith(phoneBook[i])){
                    return false;
                }
            }
        }
        return answer;
    }
}
```

- 소요시간 : 10분

- Hash 사용하지 않음

### 접근방법

1. 전화번호의 수가 1,000,000개 이하이지만 최악의 경우 O(n<sup>2</sup>)이지만 최선의 경우 O(1)이므로 전체 탐색 시도

2. 시간을 줄이기 위해 `i == j`인 경우와 접두어가 포함된 배열의 길이가 더 긴지 확인하여 early return
