# 문제풀이

## 1. 세 수 중 최솟값

- 가장 작은 수 출력하기

```javascript
function solution(A, B, C) {
    return Math.min(A, B, C);
}

solution(6, 5, 11);

// 나머지 매개변수 및 전개구문을 활용하여 
// 확장성 있게 최대 값을 구할 수도 있다. 
function solutionTwo(...nums) {
    return Math.max(...nums);
}

solutionTwo(11, 8, 3, 5, 25, 6, 7, 8);
```
