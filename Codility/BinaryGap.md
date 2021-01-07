## 문제 이름

[문제 링크](https://app.codility.com/programmers/lessons/1-iterations/binary_gap/start/)

### JavaScript

```javascript
function solution(N) {
    const binaryStr = N.toString(2);
    let maxLength = -1;
    let currentLength = 0;
    for (let i = 0; i < binaryStr.length; i++) {
        if (binaryStr[i] == 1) {
            if (maxLength < currentLength) {
                maxLength = currentLength;
            }
            currentLength = 0;
        } else {
            if (maxLength != -1) currentLength++;
        }
    }
    return maxLength;
}
```

-   소요시간 : 12 분

### 접근방법

-   이진수로 변환 후 가장 긴 0의 갯수를 반환하는 간단한 문제

-   하지만 오랜만에 보는 영어는 간단하지 않았다.

-   결과는 [이렇게](https://app.codility.com/demo/results/training4Z68HS-BP4/) 신기하게 나온다.
