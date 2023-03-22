# 문제풀이

## 1. 자리수의 합

- N개의 자연수가 입력되면 각 자연수의 자릿수 합을 구하고 그 합의 최대인 자연수를 출력하는 프로그램을 작성하라
- 자연수의 합이 같은 경우 원래 숫자가 큰 숫자를 답으로 한다.
    - 만약 235와 1234가 동시에 답이 될 수 있다면 1234를 답으로 출력해야한다.
- 반환 값
    - 자릿수의 합이 최대인 자연수를 출력한다.

```javascript
function solution(...nums) {
    let totalArr = nums.map(ele => {
            let eleArr = ele.toString().split('');

            return eleArr.reduce((acc, cur) => {
                return parseInt(acc) + parseInt(cur);
            });
        }),
        totalMaxNum = Math.max(...totalArr),
        numsMaxNum = 0;


    for (let i = 0, len = totalArr.length; i < len; i++) {
        // totalArr[i]와 totalArr의 최대값 비교 후 numsMaxNum값 대입하기 
        if (totalArr[i] === totalMaxNum && numsMaxNum < nums[i]) {
            numsMaxNum = nums[i];
        }
    }

    return numsMaxNum;
}

solution(128, 460, 603, 40, 521, 137, 123); // 137
```

## 2. 뒤집은 소수

- N개의 자연수가 입력되면 각 자연수를 뒤집은 후 그 뒤집은 수가 소수이면 그 소수를 출력하는 프로그램을 작성하라
- 예를 들어 32를 뒤집으면 23, 23은 소수이다. 그럼 23을 출력한다.
  <br>단 910을 뒤집으면 19로 숫자화 해야한다. 첫 자리부터의 연속된 0은 무시한다.

- 반환값
    - 첫 줄에 뒤집은 소수를 출력한다. 출력순서는 입력된 순서대로 출력한다.

```javascript
function solution(...nums) {
    let maxNum = parseInt(Math.max(...nums).toString().split('').reverse().join('')),
        str = '',
        obj = {},
        arr = [];

    nums.map(ele => {
        let num = parseInt(ele.toString().split('').reverse().join(''));

        // 약수 : 어떤 수를 나누어 떨어지게 하는 수 (예를 들어 2x1 = 2 , 2와 1)
        // 소수 : 약수가 1과 자기 숫자인 경우
        // 1제거, 짝수 제거(= 즉 나눴을 때 정수가 아닌 경우의 수를 받아온다)
        // 짝수처리 중 정수 2 에외처리 (2를 제외하고 2의 배수 제거됨) 
        if (num !== 1 && !Number.isInteger(num / 2) || num === 2) {
            for (let i = 1; i <= maxNum; i++) {
                // 나눴을 때 나머지가 0이면 
                // 어떤 수에 나눠진 경우이니, 나눠진 부분의 수를 구하기 
                if (num % i === 0) {
                    // 나눠진 수의 부분을 배열로 저장해 소수를 판별하기 위한 객체로 저장 
                    str += `${i} `;
                    obj[num] = str.trim();
                    if (num === i) {
                        arr.push(Object.assign({}, obj));
                        str = '';
                        obj = {};
                    }
                }
            }
        }
    });

    // 소수 값 구하기
    let primeNumArr = [];
    for (let n = 0, len = arr.length; n < len; n++) {
        let key = Object.keys(arr[n]).join('');

        if (`1 ${key}` === arr[n][key]) {
            primeNumArr.push(key);
        }
    }

    return primeNumArr.join(' ');
}

solution(32, 55, 62, 20, 250, 370, 20, 30, 100); //23, 2, 73, 2, 3
```
