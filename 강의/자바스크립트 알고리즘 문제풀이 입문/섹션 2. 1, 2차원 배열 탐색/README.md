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

## 2. 보이는 학생

- 앞에 서있는 사람들 보다 크면 보이고, 작거나 크면 보이지 않는다.
    - 이 말은 즉슨 nums[0] 값을 기준으로 다음 값과 비교하여 큰 수면 max에 대입하고 순차적으로 비교하면 된다는 말이다.
- 선생님이 볼 수 있는 최대 학생수를 출력하라.

```javascript
function solution(...nums) {
    let maxNum = nums[0],
        maxArr = [];

    maxArr.push(maxNum);
    for (let i = 1, len = nums.length; i < len; i++) {
        // 130 < 135 / 135 < 148 / 148 < 140(false) / 148 < 145(false) ... / 148 < 150 / 150 < 153
        if (maxNum < nums[i]) {
            maxNum = nums[i];
            maxArr.push(maxNum);
        }
    }
    return maxArr.length;
}

solution(130, 135, 148, 140, 145, 150, 150, 153);
// maxArr output : [130, 135, 148, 150, 153] 
// maxArr length : 5
```
