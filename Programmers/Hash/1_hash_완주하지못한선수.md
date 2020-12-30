## 완주하지 못한 선수

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42576?language=javascript)

```javascript
function solution(participant, completion) {
  const participantObj = {};
  participant.forEach((name) => {
    participantObj[name] = participantObj[name] + 1 || 1;
  });
  completion.forEach((name) => {
    if (participantObj[name] === 1) {
      delete participantObj[name];
    } else {
      participantObj[name] = participantObj[name] - 1;
    }
  });
  return Object.keys(participantObj)[0];
}
```

- 소요시간 : 15분

### 접근방법

1.  단순하게 `participant.filter(name => completion.include)`로 생각함

    --> 동명이인이 있을 수 있으므로 불가

2.  participant로 객체를 만들고 선수의 인원 수를 저장함

    completion을 순회하며 객체에서 인원을 제거함
