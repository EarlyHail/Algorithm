## 문제 이름

[문제 링크](https://app.codility.com/programmers/lessons/1-iterations/binary_gap/start/)

A binary gap within a positive integer N is any maximal sequence of consecutive zeros that is surrounded by ones at both ends in the binary representation of N.

For example, number 9 has binary representation 1001 and contains a binary gap of length 2. The number 529 has binary representation 1000010001 and contains two binary gaps: one of length 4 and one of length 3. The number 20 has binary representation 10100 and contains one binary gap of length 1. The number 15 has binary representation 1111 and has no binary gaps. The number 32 has binary representation 100000 and has no binary gaps.

Write a function:

class Solution { public int solution(int N); }

that, given a positive integer N, returns the length of its longest binary gap. The function should return 0 if N doesn't contain a binary gap.

For example, given N = 1041 the function should return 5, because N has binary representation 10000010001 and so its longest binary gap is of length 5. Given N = 32 the function should return 0, because N has binary representation '100000' and thus no binary gaps.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [1..2,147,483,647].
Copyright 2009–2020 by Codility Limited. All Rights Reserved. Unauthorized copying, publication or disclosure prohibited.

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
