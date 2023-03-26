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

## 3. 멘토링

멘토링 시스템의 조건

- 멘토링
    - 멘토 : 도와주는 학생 / 멘티 : 도움을 받는 학생
    - 선생님은 M번의 수학테스트 등수를 가지고 멘토와 멘티를 정한다.
    - 만약 A학생이 멘토이고 B학생이 멘티가 되는 짝이 되었다면 A학생은 M번의 테스트에서 모두 B학생보다 등수가 앞서야한다.
    - M번의 수학성적이 주어지면 멘토와 멘티가 되는 짝을 만들 수 있는 경우가 총 몇가지인지 출력하라
    - 테스트 결과가 3 4 1 2로 입력 되었다면 3번 학생이 1등, 4번 학생이 2등, 1번 학생이 3등, 2번 학생이 4등을 의미한다. 3줄에서 4명의 학생수의 등수를 가지고 멘토와 멘티의 짝수를 정하기
      <br><br>
      3 4 1 2<br>
      4 3 2 1<br>
      3 1 4 2<br>

(IF)3번이 기준이면

1번째 줄에서 3이 1등
2번째 줄에서 4가 1등 3이 2등 그러므로 2,1만 멘티 가능
3번째 줄에서 3이 다시 1등 고로 4를 제외하고 1,2만 가능이므로 3,1 3,2만 멘토 멘티 짝 가능

*** A학생은 M번의 테스트에서 모두 B학생보다 등수가 앞서야한다. ***
<br>

- 결과로 나와야하는 값 (*은 멘토 자격이 안됨을 의미)<br>
  1번학생 - *2,*4<br>
  2번학생 - *1<br>
  3번학생 - *4,1,2<br>
  4번학생 - *1,2,*3

```javascript
// case 1 
function solution(test) {
    let obj = {},
        arr = Array.from({
            length: test[0].length
        }, () => {
            return []
        }),
        outArr = [];

    // 1등을 기준으로 멘티가 될 수 있는 값 대입 - 멘토 1,2,3,4를 기준으로 멘티값 slice해서 저장 
    for (let i = 0, tLen = test.length; i < tLen; i++) {
        for (let j = 0, len = test[0].length; j < len; j++) {
            let idx = test[i][j],
                idxStr = test[i].slice(j + 1).join(',');

            if (idxStr === '')
                continue;
            arr[idx - 1].push(idxStr);
        }
    }

    // 저장한 중복되는 멘티값 제거 
    let disArr = arr.map((ele, idx) => {
        return [...new Set(ele.join(',').split(','))];
    });

    // 멘티값(=nowNum)을 기준으로 disArr 값을 불러오고
    // 학생 값(=i)을 대입해서 indexOf로 중복되는 값을 제거한다.
    // 그러니까 1번의 2번 array에서 1번이 있으면 index가 있으므로 제거  
    for (let i = 0, len = disArr.length; i < len; i++) {
        for (let j = 0, jLen = disArr[i].length; j < jLen; j++) {
            let nowNum = disArr[i][j],
                nowArr = disArr[i],
                studentNum = i + 1,
                valArr = disArr[nowNum - 1];

            // 멘티 값에 studentNum이 있으면 제거 
            if (valArr.indexOf(`${studentNum}`) === -1) {
                outArr.push(`멘토는 : ${studentNum}, 멘티는 : ${nowNum}`);
            }
        }
    }

    return outArr;
}

solution([
    [3, 4, 1, 2],
    [4, 3, 2, 1],
    [3, 1, 4, 2]
]);

// case 2
function solutionTwo(test) {
    let arr = test,
        lineLen = arr[0].length,
        studentArr = Array.from({
            length: lineLen
        }, (v, i) => {
            return i + 1
        }),
        listArr = [];

    /*
        1. 학생명 - 1,2,3,4 
        2. 멘티가 될 수 있는 경우의 m번의 케이스 구하기 
        1은 몇명의 멘티 ~~ 4는 몇명의 멘티
        3. 멘토가 될 학생은 M번의 테스트에서 멘티를 다 앞서야한다 
        즉 3번의 시험 -> 3번 다 멘티보다 앞에 있어야한다는 것
    */

    for (let i = 0, len = arr.length; i < len; i++) {
        for (let j = 0; j < lineLen; j++) {
            let student = arr[i].indexOf(studentArr[j]),
                studentList = arr[i].slice(student + 1);

            if (i === 0) {
                listArr[j] = studentList;
            } else {
                listArr[j].push(studentList);
            }
        }
    }

    let studentFinalList = [];
    listArr.map((ele, idx) => {
        let list = ele.flat(),
            studentNum = idx + 1;
        for (let i = 0, len = list.length; i < len; i++) {
            let item = list[i],
                name = String(studentNum) + item;

            if (list.join('').match(new RegExp(`${item}`, 'g')).length === arr.length) {
                if (studentFinalList.indexOf(name) === -1) {
                    studentFinalList.push(name);
                }
            }
        }
    })

    return studentFinalList.length;
}

solutionTwo([
    [3, 4, 1, 2],
    [4, 3, 2, 1],
    [3, 1, 4, 2]
]) //3
```
