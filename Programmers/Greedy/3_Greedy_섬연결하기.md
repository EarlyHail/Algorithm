## 문제 이름

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42861?language=javascript)

### JavaScript

```javascript
class DisjointSet {
    constructor(size) {
        this.groups = Array(size)
            .fill(0)
            .map((data, index) => index);
    }
    union(base, target) {
        const baseGroupId = this.find(base);
        const targetGroupId = this.find(target);
        this.groups = this.groups.map((group, node) => {
            if (group == targetGroupId) return (group = baseGroupId);
            else return group;
        });
    }
    find(node) {
        return this.groups.find((_, nodeNumber) => node == nodeNumber);
    }
    isSame(base, target) {
        const baseGroupId = this.find(base);
        const targetGroupId = this.find(target);
        return baseGroupId == targetGroupId;
    }
}

function solution(n, costs) {
    costs.sort((prev, next) => prev[2] - next[2]);
    const set = new DisjointSet(n);
    let answer = 0;
    for (let i = 0; i < costs.length; i++) {
        const [node1, node2, cost] = costs[i];
        if (!set.isSame(node1, node2)) {
            set.union(node1, node2);
            answer += cost;
        }
    }
    return answer;
}
```

-   소요시간 : 25 분

### 접근방법

1. 노드와 간선의 배열인 `costs` 배열을 비용으로 오름차순 정렬

2. Disjoint Set 자료구조 생성

    - 배열을 이용하여 Disjoint Set 구현

    - `index : 노드의 번호`, `value : 집합 번호`

3. `costs` 배열을 순회하며

    - 노드 2개가 같은 집합에 속해있는지 확인하고

    - 같은 집합이 아니라면 연결한 뒤 비용을 정답에 추가한다.

    - 같은 집합이라면 연결하지 않고 다음 비용의 그래프로 넘어간다.
