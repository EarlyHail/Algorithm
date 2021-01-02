## 문제 이름

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42579?language=javascript)

### JavaScript

```javascript
function solution(genres, plays) {
    const answer = [];
    // 장르별 play 시간을 가지는 Object
    const playByGenresObj = {};

    // 각 장르의 노래와 index를 가지는 Object of Arrays
    // {
    //  classic: [ [ 3, 800 ], [ 0, 500 ], [ 2, 150 ] ],
    //  pop: [ [ 4, 2500 ], [ 1, 600 ] ]
    // }
    const playEachGenresObj = {};

    for (let i = 0; i < genres.length; i++) {
        playByGenresObj[genres[i]] =
            playByGenresObj[genres[i]] == undefined
                ? plays[i]
                : playByGenresObj[genres[i]] + plays[i];
        playEachGenresObj[genres[i]] == undefined
            ? (playEachGenresObj[genres[i]] = [[i, plays[i]]])
            : playEachGenresObj[genres[i]].push([i, plays[i]]);
    }

    // 장르별 play 시간을 정렬하기 위한 Array of Arrays
    const playByGenres = Object.keys(playByGenresObj)
        .map((genreKey) => {
            return [genreKey, playByGenresObj[genreKey]];
        })
        .sort((before, after) => after[1] - before[1]);

    // 각 장르의 노래와 index를 내림차순으로 정렬
    Object.keys(playEachGenresObj).forEach((genreKey) => {
        playEachGenresObj[genreKey].sort(
            (before, after) => after[1] - before[1]
        );
    });

    // 정렬된 장르별 play 시간을 순회하며
    playByGenres.forEach((genre) => {
        // 각 장르의 play 시간을 순회
        for (let i = 0; i < playEachGenresObj[genre[0]].length; i++) {
            if (i >= 2) return;
            answer.push(playEachGenresObj[genre[0]][i][0]);
        }
    });
    return answer;
}
```

-   소요시간 : 25분

### 접근방법

1. 답을 구할 필요한 자료구조는, 전체 장르에 대한 play와 각 장르에 대한 play이다. 이를 위해선 총 3가지의 자료구조가 필요하다.

    1. 장르별 총 플레이 시간이 나타난 자료구조

        ```json
        { "classic": 1450, "pop": 3000 }
        // Key: genres, Value : Sum of Plays by Genre
        ```

    2. 장르별 총 플레이 시간을 정렬한 자료구조, 1번의 자료구조를 배열로 변환하여 sorting

        ```json
        [
            ["pop", 3100],
            ["classic", 1450]
        ]
        ```

    3. 장르별로 각 곡의 play로 정렬된, play와 index를 가지는 Object of Arrays

        ```json
        {
            "classic": [
                [3, 800],
                [0, 500],
                [2, 150]
            ],
            "pop": [
                [4, 2500],
                [1, 600]
            ]
        }
        ```

2. 위 2번, 3번 자료구조를 가지고 순회하며 최대 2개씩 play가 많은 순으로 노래의 index를 뽑아내면 답이 나온다.
