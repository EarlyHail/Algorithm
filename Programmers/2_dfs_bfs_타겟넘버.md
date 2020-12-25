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

## BFS

- 풀이 1

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

- 풀이 2

  ```javascript
  function solution(numbers, target) {
    let answer = 0;
    const queue = [numbers[0], -numbers[0]];
    const endIndex = numbers.length;
    let currentIndex = 0;
    while (queue.length > 0) {
      let siblingJobs = [];
      currentIndex++;
      while (queue.length > 0) {
        let job = queue.shift();
        if (currentIndex == endIndex) {
          if (job == target) {
            answer++;
          }
        } else {
          siblingJobs.push(
            job + numbers[currentIndex],
            job - numbers[currentIndex]
          );
        }
      }
      queue.push(...siblingJobs);
    }
    return answer;
  }
  ```

  - 인덱스를 삭제

    첫 번째 while은 각 level의 breath를 탐색

    두 번째 while은 같은 level의 breath를 탐색

  - 시간은 줄었지만 런타임 오류 발생

- 풀이 3

  ```javascript
  function solution(numbers, target) {
    let answer = 0;
    const queue = [[numbers[0], -numbers[0]]];
    const endIndex = numbers.length;
    let currentIndex = 0;
    for (let i = 0; i < numbers.length; i++) {
      let siblingJobs = queue.shift();
      const siblings = [];
      currentIndex++;
      for (let i in siblingJobs) {
        if (currentIndex == endIndex) {
          if (siblingJobs[i] == target) {
            answer++;
          }
        } else {
          siblings.push(
            siblingJobs[i] + numbers[currentIndex],
            siblingJobs[i] - numbers[currentIndex]
          );
        }
      }
      if (siblings.length != 0) {
        queue.push(siblings);
      }
    }
    return answer;
  }
  ```

  - 같은 depth (같은 numbers index)일 경우 하나의 배열로 관리

    push, shift를 numbers의 길이 만큼 하기 때문에 배열 삽입 / 삭제 시간 줄어듬

  - 풀이 2보다 1/6 ~ 1/5의 시간 단축

## 소요 시간 줄이기

- `===`보다 `==`가 더 빠르다.

- 배열 구조분해 할당은 그때그때 접근하는것보다 속도가 느리다????

  ```javascript
  const [a, b] = arr;
  ```

- 구조분해 할당보다 배열의 원소를 변수로 저장하면 속도가 빠르다.

  ```javascript
  const a = arr[0];
  const b = arr[1];
  ```

- 배열에 push / shift 연산은 비용이 매우 크다
