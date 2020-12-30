## 문제 이름

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42842?language=javascript)

### 풀이 1

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

- brute force 이용

### 풀이 2
```javascript
function solution(brown, yellow) {
    const x = (4 + brown + Math.sqrt(brown * brown - 8 * brown - 16 * yellow + 16))/4;
    const y = (brown + yellow)/x
    return [x,y]
}
```
x : 카펫의 가로길이

y : 카펫의 세로 길이 라고 하면 다음의 두 방정식

x*y = brown + yellow

2x + 2y - 4 = brown 이 성립한다.

위 식을 정리하면 이차방정식

2x^2 - (brown - 4)x + 2(brown + yellow) = 0을 유도할 수 있다.

이차방정식의 근의 공식에 의해 위 방정식의 해

x = (4 + brown + sqrt(brown^2 - 8brown + 16yellow + 16))/4 이다.