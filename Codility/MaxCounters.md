## 문제 이름

[문제 링크](https://app.codility.com/programmers/lessons/4-counting_elements/max_counters/)

You are given N counters, initially set to 0, and you have two possible operations on them:

increase(X) − counter X is increased by 1,
max counter − all counters are set to the maximum value of any counter.
A non-empty array A of M integers is given. This array represents consecutive operations:

if A[K] = X, such that 1 ≤ X ≤ N, then operation K is increase(X),
if A[K] = N + 1 then operation K is max counter.
For example, given integer N = 5 and array A such that:

    A[0] = 3
    A[1] = 4
    A[2] = 4
    A[3] = 6
    A[4] = 1
    A[5] = 4
    A[6] = 4

the values of the counters after each consecutive operation will be:

    (0, 0, 1, 0, 0)
    (0, 0, 1, 1, 0)
    (0, 0, 1, 2, 0)
    (2, 2, 2, 2, 2)
    (3, 2, 2, 2, 2)
    (3, 2, 2, 3, 2)
    (3, 2, 2, 4, 2)

The goal is to calculate the value of every counter after all operations.

Write a function:

function solution(N, A);

that, given an integer N and a non-empty array A consisting of M integers, returns a sequence of integers representing the values of the counters.

Result array should be returned as an array of integers.

For example, given:

    A[0] = 3
    A[1] = 4
    A[2] = 4
    A[3] = 6
    A[4] = 1
    A[5] = 4
    A[6] = 4

the function should return [3, 2, 2, 4, 2], as explained above.

Write an efficient algorithm for the following assumptions:

N and M are integers within the range [1..100,000];
each element of array A is an integer within the range [1..N + 1].
Copyright 2009–2020 by Codility Limited. All Rights Reserved. Unauthorized copying, publication or disclosure prohibited.

### JavaScript - 풀이2

```javascript
function solution(N, A) {
    let answer = Array(N).fill(0);
    let maxCount = 0;
    for (let i = 0; i < A.length; i++) {
        const index = A[i] - 1;
        if (index == N) {
            answer = Array(N).fill(maxCount);
            continue;
        }
        answer[index]++;
        if (maxCount < answer[index]) maxCount = answer[index];
    }
    return answer;
}
```

-

### 접근방법

1. 반복문을 돌며 나온 `A[i]의 값을 answer의 인덱스로 참조해 1씩 더해줌

2. `N+1` 값(`A[i] -1 == N`) 일 경우 모든 원소가 maxCount인 배열을 만들어줌

-   시간 초과 오류 발생

    ![MaxCount-timeout](img/MaxCounters-1.png)

-   for문에 Arrays.fill()이 있으므로 시간복잡도는 O(N\*M)

-   참고로 `answer = Array(N).fill(maxCount);` 가 `answer = answer.map(x => maxCount)`보다 더 **`빠르다`**

### JavaScript - 풀이2

```javascript
function solution(N, A) {
    let answer = Array(N).fill(0);
    let currentMaxCount = 0;
    let maxCount = 0;
    for (let i = 0; i < A.length; i++) {
        const index = A[i] - 1;
        if (index == N) {
            maxCount = currentMaxCount;
            continue;
        }
        if (answer[index] < maxCount) {
            answer[index] = maxCount;
        }
        answer[index]++;
        if (currentMaxCount < answer[index]) currentMaxCount = answer[index];
    }
    for (let i = 0; i < answer.length; i++) {
        if (answer[i] < maxCount) {
            answer[i] = maxCount;
        }
    }
    return answer;
}
```

### 접근 방법

![MaxCount-timeout](img/MaxCounters-2.png)

-   시간복잡도를 줄이기 위해 반복문 내에 반복 작업을 삭제

-   각 값이 1씩 더해질 때 currentMaxCount를 최댓값으로 업데이트

-   N+1값이 나왔을 때 `maxCount`를 currentMaxCount로 업데이트

-   값을 1씩 더해주기 전, maxCount와 비교 후 작을 경우 maxCount로 먼저 만들어줌

-   값이 갱신이 안될 수도 있으니 뒤에 모든 `answer`에 대해 maxCount 이상으로 값을 만들어줌
