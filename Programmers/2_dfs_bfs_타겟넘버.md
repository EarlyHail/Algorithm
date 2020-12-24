## 타겟 넘버

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/43165?language=javascript)

## DFS

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

## DFS

```javascript
function solution(numbers, target) {
  const queue = [
    [0, numbers[0]],
    [0, -numbers[0]],
  ];
  let answer = 0;
  const endJobIndex = numbers.length - 1;
  while (queue.length > 0) {
    const job = queue.shift();
    if (job[0] == endJobIndex) {
      if (job[1] == target) {
        answer++;
      }
      continue;
    }
    const newIndex = job[0] + 1;
    queue.push(
      [newIndex, job[1] + numbers[newIndex]],
      [newIndex, job[1] - numbers[newIndex]]
    );
  }
  return answer;
}
```

- 시간 초과로 해결하지 못함

## 소요 시간 줄이기

- `===`보다 `==`가 더 빠르다.

- 배열 구조분해 할당은 그때그때 접근하는것보다 속도가 느리다????

- 정수의 갯수가 많아질 때 배열에 push / shift하는 비용이 많아 시간이 오래걸리는걸로 예측
