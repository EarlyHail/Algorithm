## 문제 이름

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/43162?language=javascript)

```javascript
const dfs = (n, computers, visited, currentNode) => {
    for(let j = 0; j<n; j++){
        // 자기 자신과 연결되거나, 방문한 노드이거나, 연결되있지 않은 노드는 Pass
        if(currentNode == j || visited[j] == true || computers[currentNode][j] != 1) continue;
        // 노드 방문 표시 후 dfs 알고리즘 실행
        visited[j] = true;
        dfs(n, computers, visited, j);
    }
}

function solution(n, computers) {
    // 방문한 node인지 여부를 저장하기 위한 visited 배열
    const visited = Array(n).fill(false);
    let answer = 0;
    for(let i = 0; i<n; i++){
        // 각 노드를 처음 방문할 때만 군집의 개수 증가
        if(visited[i] == false){
            answer ++;
            visited[i] = true;
        }
        // 현재 노드와 이어진 노드들을 찾기 위한 로직
        dfs(n, computers, visited, i);
    }
    return answer;
}
```

- 소요시간 : 50분

### 접근방법

- 그래프 상에서 연결된 노드들의 묶음(군집) 개수를 찾는 문제

- 방문 노드를 저장하여 새롭게 방문할 때(새로운 군집)마다 카운트를 세기 위한 visited 배열 사용

- 하나의 그래프를 방문할 때, 그것과 연결된 모든 그래프를 탐색하는 dfs 로직 구현

