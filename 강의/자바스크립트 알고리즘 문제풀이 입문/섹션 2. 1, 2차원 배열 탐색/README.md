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

- 앞에 서있는 사람들 보다 크면 보이고, 작거나 같으면 보이지 않는다.
    - 이 말은 즉슨 nums[0] 값을 기준으로 다음 값과 비교하여 큰 수면 maxNum에 대입하고 순차적으로 비교하면 된다는 말이다.
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

## 3. 가위바위보

- 1: 가위, 2: 바위, 3:보
- A가 이기면 A 출력, B가 이기면 B 출력, 숫자가 같으면 비김 D
- 경우의 수 비교
    - a === b “D”
    - 가위1 < 바위2 / 1가위 && 보3
        - (1 < 3 으로 조건식으론 B가 true 이지만 가위바위보 규칙에 따라 A 이김으로 예외처리)
    - 바위2 > 가위1 / 바위2 < 보3
    - 보3 && 가위1(예외처리 - 위와 같은 규칙으로 3 > 1 이지만 B이김) / 보3 > 바위2

```javascript
function solution(a, b) {

    for (let i = 0, len = a.length; i < len; i++) {
        if (a[i] === b[i]) {
            console.log(a[i], b[i], "D");
        } else if (a[i] < b[i]) {
            // 1가위, 보3인 경우 에외처리
            if (a[i] === 1 && b[i] === 3) {
                console.log(a[i], b[i], "A");
            } else {
                console.log(a[i], b[i], "B");
            }
        } else {
            // 보3, 1가위인 경우 예외처리
            if (a[i] === 3 && b[i] === 1) {
                console.log(a[i], b[i], "B");
            } else {
                console.log(a[i], b[i], "A");
            }
        }
    }
}

solution([2, 3, 3, 1, 3, 1], [1, 1, 2, 2, 3, 3]);
/* 
2 1 'A'
3 1 'B'
3 2 'A'
1 2 'B'
3 3 'D'
1 3 'A'
* */
```

## 4. 점수 계산

- 조건
    - 0은 문제의 답이 틀린 경우 , 1은 문제의 답이 맞는 경우
    - 연속으로 문제의 답이 맞는 경우 두번째 문제는 2점, 세번째 문제는 3점, K번째 문제는 K점 으로 계산.
- 채점 결과에 대하여 가산점을 고려한 총 점수 출력

```javascript
function solution(...nums) {
    let sum = 0,
        total = 0;

    for (let i = 0, len = nums.length; i < len; i++) {
        if (nums[i] === 0) {
            sum = 0;
        } else {
            total += ++sum;
        }
    }

    return total;
}

solution(1, 0, 1, 1, 1, 0, 0, 1, 1, 0); // 10
```

## 5. 등수 구하기

- 조건
    - 같은 점수가 입력될 경우 높은 등수로 동일 처리
    - 가장 높은 점수가 92점이고 1등이 3명이면 그 다음 학생은 4등이 된다.
- 각 학생의 등수를 입력된 순서대로 출력

```javascript
// case 1 
function solution(...nums) {
    // 해당 배열을 sort
    let sort = [...nums].sort(function (a, b) {
            return b - a;
        }),
        rank = nums.map(ele => {
            return sort.indexOf(ele) + 1;
        });
    // 현재 입력된 순서의 배열(nums)을 loop 돌림
    // nums ele을 통해 sort index를 가져와 매칭하고 값 반환
    // indexOf()는 배열에서 지정된 요소를 찾을 수 있는 첫번째 index만 반환하여 가져오기 때문에 등수 처리 동일하게 가능 

    return rank.join(' ');
}

solution(87, 89, 92, 100, 76); // '4 3 2 1 5'
// solution(87, 100, 89, 92, 100, 76, 99, 85, 87) -> '6 1 5 4 1 9 3 8 6' 반환 

// case 2
function solutionTwo(...nums) {
    let n = nums.length,
        rank = Array.from({length: n}, () => 1);
    // 1 값을 반환한 배열 (갯수는 length n개) 

    for (let i = 0; i < n; i++) {
        for (let j = 0; j < n; j++) {
            // nums[i]보다 nums[j]이 크면 rank[i]의 값 증가 
            if (nums[i] < nums[j]) rank[i]++;
        }
    }

    return rank.join(' ');
}

solutionTwo(87, 100, 89, 92, 100, 76, 87);
// '5 1 4 3 1 7 5'
```

## 6. 격자판 최대합

- 조건
    - N*N 격자판이 주어지면 각 행의 합, 각 열의 합, 두 대각선의 합중 가장 큰 합을 출력하라
- 경우의 수 구하기
    - 각 행의 합
        - 00 01 02 03 04 ... -> 포문으로 각 행 더하기
    - 각 열의 합
        - 00 10 20 30 40
        - 01 11 21 31 41
        - 02 12 22 32 42
        - 03 13 23 33 43
        - 04 14 24 34 44
    - 두 대각선의 합
        - 00 11 22 33 44
        - 40 31 22 13 04

```javascript
function solution(arr) {
    let arrLen = arr.length,
        leftDiagonalSum = 0,
        rightDiagonalSum = 0,
        columnSumArr = Array.from({length: arrLen}, () => 0),
        rowSumArr = Array.from({length: arrLen}, () => 0),
        colMaxNum = 0,
        rowMaxNum = 0;


    for (let i = 0, len = arrLen; i < len; i++) {
        let reverseOrder = (arrLen - 1) - i;

        // 대각선 
        leftDiagonalSum += arr[i][i];
        rightDiagonalSum += arr[reverseOrder][i];

        for (let o = 0; o < arrLen; o++) {
            // 열과 행의 합 구하기
            columnSumArr[i] += arr[o][i];
            rowSumArr[i] += arr[i][o];
        }

        if (colMaxNum < columnSumArr[i]) colMaxNum = columnSumArr[i];
        if (rowMaxNum < rowSumArr[i]) rowMaxNum = rowSumArr[i];
    }

    return Math.max(leftDiagonalSum, rightDiagonalSum, colMaxNum, rowMaxNum);
}

solution([
    [10, 13, 10, 12, 15],
    [12, 39, 30, 23, 11],
    [11, 25, 50, 53, 15],
    [19, 27, 29, 37, 27],
    [19, 13, 30, 13, 19]
]);
// 155 
```

## 7. 봉우리

- 조건
  - 지도 정보가 N*N 격자판에 주어진다. 각 격자에는 지역의 높이가 쓰여있다.
  - 각 격자판의 숫자 중 자신의 상하좌우 숫자보다 큰 숫자는 봉우리 지역이다.
  - 격자의 가장자리는 0으로 초기화 되었다 가정한다.
  - 만약 N=5이고, 격자판의 숫자가 다음과 같다면 봉우리의 개수는 10개이다.
  - 봉우리 지역이 몇개인지 알아내는 프로그램을 작성하라.

```javascript
function solution(arr) {
    let arrLen = arr.length,
        standardArr = [];

    for (let i = 0; i < arrLen; i++) {
        for (let o = 0; o < arrLen; o++) {
            // 0은 제외하고 숫자 있는 부분만 남겨둔다. 
            if (arr[i][o] === 0 || arr[o][i] === 0) continue;
            // 순서의 기준 : 상 하 좌 우 | 숫자의 기준 : arr[i][o]
            let positionArr = [arr[i - 1][o], arr[i + 1][o], arr[i][o - 1], arr[i][o + 1]],
                standardNum = arr[i][o];

            // positionArr의 최대 숫자와 기준점이 되는 standardNum 숫자 비교 
            if (Math.max(...positionArr) < standardNum) {
                standardArr.push(standardNum);
            }
        }
    }

    return standardArr.length;
}

solution([
    [0, 0, 0, 0, 0, 0, 0],
    [0, 5, 3, 7, 2, 3, 0],
    [0, 3, 7, 1, 6, 1, 0],
    [0, 7, 2, 5, 3, 4, 0],
    [0, 4, 3, 6, 4, 1, 0],
    [0, 8, 7, 3, 5, 2, 0],
    [0, 0, 0, 0, 0, 0, 0]
]);
// 10
```
