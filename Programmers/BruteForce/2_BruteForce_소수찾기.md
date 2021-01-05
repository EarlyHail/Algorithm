## 문제 이름

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42839?language=javascript)

### JavaScript

```javascript
const makeNum = (number, numberArr, visited, numberObj) => {
    for (let i = 0; i < numberArr.length; i++) {
        if (visited[i] == true) continue;
        const newVisied = [...visited];
        const currentNum = number * 10 + numberArr[i];
        numberObj[currentNum] = currentNum;
        newVisied[i] = true;
        makeNum(currentNum, numberArr, newVisied, numberObj);
    }
};

function isPrimeUnder(num) {
    const numbers = Array(num + 1)
        .fill(0)
        .map((val, index) => index);
    numbers[0] = -1;
    numbers[1] = -1;
    for (let i = 2; i <= Math.sqrt(numbers.length); i++) {
        if (numbers[i] != -1) {
            for (let j = i + 1; j < numbers.length; j++) {
                if (numbers[j] == -1) continue;
                if (numbers[j] % numbers[i] == 0) {
                    numbers[j] = -1;
                }
            }
        }
    }
    return numbers;
}

function solution(numbers) {
    const numberObj = {};
    const numberArr = [...numbers].map((num) => parseInt(num));
    for (let i = 0; i < numberArr.length; i++) {
        const visited = [];
        numberObj[numberArr[i]] = numberArr[i];
        visited[i] = true;
        makeNum(numberArr[i], numberArr, visited, numberObj);
    }
    let answer = 0;
    const uniqueNum = Object.keys(numberObj)
        .sort()
        .map((num) => parseInt(num));
    const isPrimes = isPrimeUnder(uniqueNum[uniqueNum.length - 1]);
    for (let i = 0; i < uniqueNum.length; i++) {
        if (isPrimes[uniqueNum[i]] != -1) {
            answer++;
        }
    }
    return answer;
}
```

-   소요시간 : 50 분

### 접근방법

1. 입력 `numbers`로 만들 수 있는 숫자들의 배열을 만든다.

    visited를 사용하여 재귀 호출로 전체 탐색

2. 만들 수 있는 숫자들의 최대값 이하의 모든 소수를 구한다.

    이 때 찾은 소수를 찾을 때 마다 또는 소수가 아닌 수를 배열에서 제거하면 시간이 많이걸리므로 `index : 숫자, value : 소수여부`로 하고 소수가 아닐 경우 -1로 변경한다.

3. 만들 수 있는 숫자들의 값을 소수 배열에 참조하여 -1이 아닐 경우 소수이므로 카운트를 추가한다.
