# 문제풀이

## 1. 큰 수 출력하기

- 첫 번째 수는 무조건 출력한다.
- 자신의 바로 앞 수보다 큰 수만 한 줄로 출력한다.

```javascript
function solution(...nums) {
    let numArr = nums,
        maxArr = [];

    for (let i = 0, len = numArr.length - 1; i < len; len--) {
        if (len === 1) maxArr.push(numArr[len - 1]);
        if (len !== 1 && numArr[len - 1] < numArr[len]) maxArr.push(numArr[len]);
    }

    return maxArr.reverse();
}

solution(7, 3, 9, 5, 6, 12);
// [7, 9, 6, 12]
```
