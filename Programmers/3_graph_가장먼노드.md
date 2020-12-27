## 문제 이름

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/49189)

## 인접행렬 풀이

```javascript
function solution(n, edge) {
    // edge로부터 그래프를 표현하기 위한 배열
    const graph = Array(n)
        .fill(0)
        .map((el) => []);
    // 방문 여부 확인
    const visited = Array(n).fill(false);
    for (let i = 0; i < edge.length; i++) {
        graph[edge[i][0] - 1][edge[i][1] - 1] = 1;
        graph[edge[i][1] - 1][edge[i][0] - 1] = 1;
    }
    // 1번 노드부터 출발
    const queue = [[graph[0]]];
    visited[0] = true;
    let newNodeCurrentLength = 0;
    while (queue.length > 0) {
        let newNodes = [];
        const nodes = queue.shift();
        // queue에 있는 모든 node들 탐색
        for (let i = 0; i < nodes.length; i++) {
            for (let j = 0; j < nodes[i].length; j++) {
                //방문한 node이거나 연결이 안되어있으면 패스
                if (visited[j] == true || nodes[i][j] != 1) {
                    continue;
                }
                // 큐에 삽입 후 방문 체크
                newNodes.push(graph[j]);
                visited[j] = true;
            }
        }
        // 방문할 노드들의 수가 0이 아닐 경우 큐에 삽입, 최근 길이 최신화
        if (newNodes.length != 0) {
            queue.push(newNodes);
            newNodeCurrentLength = newNodes.length;
        }
    }
    return newNodeCurrentLength;
}
```

-   소요시간 : 40분

### 문제점

-   인접 행렬을 만드는것 자체가 큰 부담, 시간이 매우 오래걸림

    인접 행렬을 초기화 하는것 자체의 로직 `Array(n).fill(0).map(el => Array(n).fill(0));` 자체에서 에러 발생 (core dump)

    `Array(n).fill(0).map(el => []);`로 2차원의 빈 배열을 만들면 에러는 해결되지만 조회하는 시간이 매우 오래걸려 시간초과

-   인접 행렬이 아니라 인접 리스트로 변경

## 인접 리스트 풀이

```javascript
function solution(n, edge) {
    const graph = {};
    const visited = Array(n).fill(false);
    for (let i = 0; i < edge.length; i++) {
        try {
            graph[edge[i][0] - 1] != undefined
                ? graph[edge[i][0] - 1].push(edge[i][1] - 1)
                : (graph[edge[i][0] - 1] = [edge[i][1] - 1]);
            graph[edge[i][1] - 1] != undefined
                ? graph[edge[i][1] - 1].push(edge[i][0] - 1)
                : (graph[edge[i][1] - 1] = [edge[i][0] - 1]);
        } catch (e) {}
    }
    const queue = [[0]];
    visited[0] = true;
    let newNodeCurrentLength = 0;
    while (queue.length > 0) {
        let newNodes = [];
        const nodeIds = queue.shift();
        for (let i = 0; i < nodeIds.length; i++) {
            const nodes = graph[nodeIds[i]];
            for (let j = 0; j < nodes.length; j++) {
                if (visited[nodes[j]] == true) {
                    continue;
                }
                newNodes.push(nodes[j]);
                visited[nodes[j]] = true;
            }
        }
        if (newNodes.length != 0) {
            queue.push(newNodes);
            newNodeCurrentLength = newNodes.length;
        }
    }
    return newNodeCurrentLength;
}
```

### 접근 방법

-   로직은 인접 행렬과 동일하지만 Object를 이용해 인접 리스트를 구현하였다.

    ```json
    {
        "0": [2, 1],
        "1": [2, 0, 3, 4],
        "2": [5, 3, 1, 0],
        "3": [2, 1],
        "4": [1],
        "5": [2]
    }
    ```
