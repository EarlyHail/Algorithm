## 문제 이름

[문제 링크](URL)

```javascript
function solution(numbers) {
  const answer = numbers
    .map((num) => num.toString())
    .sort((numStr, nextNumStr) => nextNumStr + numStr - (numStr + nextNumStr))
    .join("");
  return parseInt(answer) == 0 ? "0" : answer;
}
```

- 소요시간 : 15분

### 접근방법

1. 숫자를 문자로 바꿔서 비교하면 첫 번째 숫자만 비교할 수 있다.

2. `Array.sort()`의 callback 함수에 숫자의 string값이 더 큰 수가 먼저 오도록 정렬하면 항상 최대값을 보장한다.

3. 모두 결과 문자열이 전부 0일 경우 0을 반환해야 한다.

   이 `edge case`를 생각해내는데 좀 걸렸다.
