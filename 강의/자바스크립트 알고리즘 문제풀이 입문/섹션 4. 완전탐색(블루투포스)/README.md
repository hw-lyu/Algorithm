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
