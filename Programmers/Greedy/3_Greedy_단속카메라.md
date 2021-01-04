## 문제 이름

[문제 링크](URL)

### JavaScript

```javascript
function solution(routes) {
    let answer = 0;
    routes.sort((a, b) => a[0] - b[0]);

    let prevCarLeave = routes[0][1];
    for (let i = 1; i < routes.length - 1; i++) {
        const thisCarLeave = routes[i][1];
        const nextCarEnter = routes[i + 1][0];
        if (thisCarLeave < prevCarLeave) {
            prevCarLeave = thisCarLeave;
        }
        if (prevCarLeave < nextCarEnter) {
            prevCarLeave = routes[i + 1][1];
            answer++;
        }
    }
    return answer + 1;
}
```

-   소요시간 : 30 분

### 접근방법

1. `prevCarLeave`에 처음 차량이 나갈 시점을 저장해놓는다. (차량이 나가는 가장 빠른 시간 저장)

2. 새로운 차가 들어올 때 마다

    1. `prevCarLeave`가 새로 들어온 차가 나갈 시간보다 작으면 새로 들어온 차의 나갈 시간으로 `prevCarLeave`를 변경

    2. `prevCarLeave`가 다음 차량(현재 iteration의 다음 차량, `i+1`)의 진입 시간보다 작으면 하나의 CCTV로 처리가 불가능하니 cctv의 갯수를 하나 더해준다.

    이 때, i번째 까지의 차량은 CCTV에 찍힌 상태이므로, `prevCarLeave`를 다음 차량이 나가는 시간으로 변경한다.

-   위 2 조건을 반대로 써서 찾느라 오래걸렸다....
