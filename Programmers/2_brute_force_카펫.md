## 문제 이름

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42842?language=javascript)

```javascript
function solution(brown, yellow) {
    // 3줄 이상부터 시작, (brown - 2) /2까지
    for(let row = 3; row <= (brown-2)/2; row++){
        //edge 포함 세로 Brown 개수
        const colBrowns = row;
        
        //edge 미포함 가로 Brown 개수
        const rowBrowns = (brown - colBrowns*2) / 2;

        //가로 brown 개수 * row - 2와 yellow가 같으면 정답
        if(rowBrowns*(row-2) == yellow){
            return [rowBrowns+2, colBrowns];
        }
    }
}
```

- 소요시간 : 15분

