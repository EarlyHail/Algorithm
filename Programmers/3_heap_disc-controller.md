[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42627?language=javascript#)

```javascript
function solution(jobs) {
  let totalWaitingTime = 0;
  let currentClock = 0;
  const jobsLength = jobs.length;
  while (jobs.length > 0) {
    jobs.sort((job, nextJob) => {
      if (job[0] <= currentClock && nextJob[0] <= currentClock) {
        return job[1] > nextJob[1] ? 1 : -1;
      }
      if (job[0] === nextJob[0]) {
        return job[1] > nextJob[1] ? 1 : -1;
      }
      return job[0] - nextJob[0];
    });
    const runningJob = jobs.shift();
    if (runningJob[0] >= currentClock) {
      currentClock = runningJob[0] + runningJob[1];
    } else {
      currentClock += runningJob[1];
    }
    totalWaitingTime += currentClock - runningJob[0];
  }
  return Math.floor(totalWaitingTime / jobsLength);
}
```

- 소요시간 : 1시간 10분

### 접근 방법

1. `jobs`에서 실행할 것 1개를 뽑아내고, 작업이 끝날 시간까지 들어오는 job들을 배열로 뽑아내서 반복문으로 처리

   `currentClock`에 요청 시간을 더하여 새로운 currentClock을 만들고

   `waitingTime`은 새로운 currentClock에서 입력 시간을 빼주도록 구현

   —> 시간을 구하는 로직은 사용가능하지만

   —> 반복문 내에서 작업이 진행되면서 들어올 새로운 작업들에 대한 고려 X

2. `jobs`를 삽입 순으로 정렬하되, 시간이 같은 경우 소요시간이 적은 job 순서로 정렬 후 계산 (`if(job[0] === nextJob[0])`)
3. `jobs`를 정렬할 때 입력 시간이 현재 시간보다 작으면 소요시간으로 정렬되도록 구현

   (`if(job[0] <= currentClock && nextJob[0] <= currentClock)`)

   빨리 들어왔다고 해도 cpu가 busy일 때 들어오는 작업들에게는 입력 시간은 순서에 영향을 미치지 않기 때문

4. cpu가 lazy한 상태 고려

   —> 아예 작업이 존재하지 않는 경우를 고려해야함.

   —> ex) 100ms에 100ms의 job이 하나만 들어올 경우 대기시간은 100ms임.

   —> 입력 시간이 기존 currentClock보다 클 경우, currentClock은 `currentClock + runningJob[0]`이 아니라 `currentClock = runningJob[0] + runningJob[1]` 이어야함.
