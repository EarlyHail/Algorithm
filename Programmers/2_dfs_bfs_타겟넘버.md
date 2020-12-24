## 타겟 넘버

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/43165?language=javascript)

```javascript
const calc = ({ base, index, numbers, target }) => {
  if (index === numbers.length - 1) {
    return target === base ? 1 : 0;
  }
  const newIndex = index + 1;
  const subAnswer =
    calc({ base: base + numbers[newIndex], index: newIndex, numbers, target }) +
    calc({ base: base - numbers[newIndex], index: newIndex, numbers, target });
  return subAnswer;
};

function solution(numbers, target) {
  const base = numbers[0];
  const index = 0;
  const answer =
    calc({ base, index, numbers, target }) +
    calc({ base: -base, index, numbers, target });
  return answer;
}
```

- 소요시간 : 35분

### 접근방법

1. 재귀적인 방법으로 DFS를 구현

   현재까지 더해진 값 `base`와 지금까지 더해진 배열의 위치 `index`를 사용하여 계산

   간단한 로직이지만 배열의 index를 애매하게 설정하여 시간을 많이 소모했음.
