# 문제풀이

## 1. 큰 수 출력하기

- 첫 번째 수는 무조건 출력한다.
- 자신의 바로 앞 수보다 큰 수만 한 줄로 출력한다.

```javascript
// case 1
function solution(...nums) {
    let numArr = nums,
        maxArr = [];

    for (let i = 0, len = numArr.length - 1; i < len; len--) {
        if (numArr[len - 1] < numArr[len]) maxArr.push(numArr[len]);
        if (len === 1) maxArr.push(numArr[len - 1]);
    }

    return maxArr.reverse();
}

solution(7, 8, 9, 5, 6, 12);
// [7, 8, 9, 6, 12]

// case 2 
function solutionTwo(...nums) {
    let maxArr = [];

    maxArr.push(nums[0]);

    for (let i = 1, len = nums.length; i < len; i++) {
        if (nums[i - 1] < nums[i]) maxArr.push(nums[i]);
    }

    return maxArr;
}

solutionTwo(7, 8, 9, 5, 6, 12);
// [7, 8, 9, 6, 12]
```
