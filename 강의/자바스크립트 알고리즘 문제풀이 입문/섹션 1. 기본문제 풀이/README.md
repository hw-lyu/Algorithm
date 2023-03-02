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

## 2. 삼각형 판별하기

### 삼각형의 결정조건

- 가장 긴변의 길이가 다른 두변의 길이의 합보다 크거나 같으면 삼각형으로 그릴 수 없다.
- 세 변의 길이를 줬을 때 길이가 가장 긴 변의 길이는 다른 두변의 길이의 합보다 작아야 삼각형을 그릴 수 있다.
  <br>( 1cm, 2cm, 2.99cm는 삼각형 가능)
  <br>[삼각형의 결정조건 - 글 출처](https://mathbang.net/92)

### 코드

- 첫변째 줄에 'yes', 'no'를 출력한다.

```javascript
function solution(A, B, C) {
    let maxNum = Math.max(A, B, C),
        triangleArr = [A, B, C];

    let twoSides = triangleArr.reduce((acc, cur) => {
        return acc + cur
    });

    // 삼각형의 세 변의 길이를 합산해서 제일 긴 변의 길이를 뺀다. 
    twoSides -= maxNum;

    if (maxNum < twoSides) {
        return "yes";
    } else {
        return "no";
    }
}

solution(6, 7, 11);
```

## 3. 연필개수

### 조건

- 연필 1 다스 = 12자루
- 학생 1인당 연필 1자루
- n명 = 학생수 입력 -> 필요한 연필의 다스 수 계산하는 프로그램

### 코드

- 첫번째 줄에 필요한 다스 수를 출력한다.

```javascript
function solution(n) {
    // 총 연필 갯수
    let pencilOneCount = 12;
    // (학생수 * 학생 1인당 연필 1자루 = 1) / 총 연필 갯수 
    return Math.ceil((n * 1) / pencilOneCount);
}

solution(25);
```

## 4. 1부터 N까지 합 출력하기

- 1부터 N까지의 합을 출력한다.

```javascript
function solution(n) {
    let num = 0;
    for (let i = 1; i <= n; i++) {
        num += i;
    }

    return num;
}

solution(6);
```

## 5. 최솟값 구하기

- 가장 작은 값을 출력한다.

```javascript
function solution(...num) {
    let arr = num,
        minNum = 100;

    arr.forEach((ele) => {
        // 100을 기준으로 ele의 첫번째 값 5를 값에 대입하고 
        // 그 후로 3<5,7<3.. 이런식으로 값을 비교하고 최소값을 대입해준다. 
        if (ele < minNum) minNum = ele;
    });

    return minNum;
}

solution(5, 3, 7, 11, 2, 15, 17);
```

## 6. 홀수

- 홀수들의 합 / 홀수들 중 최소값을 출력한다.

```javascript
function solution(...num) {
    let arr = num,
        oddArr = [],
        oddNum = 0,
        oddMinNum = 100;

    arr.forEach(ele => {
        if (ele % 2 === 1) {
            oddArr.push(ele);

            oddNum += ele;

            if (ele < oddMinNum) oddMinNum = ele;
        }
    });

    return '홀수 리스트 : ' + oddArr + ', 총합 : ' + oddNum + ', 홀수 최소값 : ' + oddMinNum;
}

solution(12, 77, 38, 41, 53, 92, 85);
// 홀수 리스트 : 77,41,53,85
// 총합 : 256, 홀수 최소값 : 41
```

## 7. 10부제

### 조건

- 자동차 10부제
- 조건 : 자동차 번호의 일의 자리 숫자와 날짜의 일의 자리 숫자가 일치하면 해당 자동차의 운행을 금지
  <br> ex. 자동차 번호의 일의 자리 숫자가 7이면 7일, 17일, 27일 운행 금지
  <br> 자동차 번호의 일의 자리 숫자가 0이면 10일,20일,30일 금지

### 코드

- 날짜의 일의 자리 숫자가 주어지고 7대의 자동차 번호의 끝 두자리 수가 주어졌을 때 위반하는 자동차의 대수를 출력하라

```javascript
function solution(day, ...carNum) {
    let carNumArr = carNum,
        carArr = [];

    carNumArr.forEach(ele => {
        // 날짜의 일의 자리와 자동차 번호의 일의 자리가 일치하면 자동차 운행을 금지하므로
        // day에 맞는 배열의 자동차 번호를 찾아 위반하는 자동차 대수를 찾음 
        if (String(ele).includes(day)) {
            carArr.push(ele);
        }
    })

    return carArr.length;
}

solution(0, 12, 20, 54, 30, 87, 91, 30);

// case
function solutionTwo(day, ...carNum) {
    let carNumArr = carNum;

    // filter로 나머지 연사자를 이용해 해당 일에 해당하는 배열을 구한다. 
    return carNumArr.filter(ele => {
        return ele % 10 === day
    }).length
}

solutionTwo(0, 12, 20, 54, 30, 87, 91, 30);
```

## 8. 일곱난쟁이

### 조건

- 조건 : 아홉 난쟁이의 키, 합 100이 나와야 한다.

### 코드

- 일곱 난쟁이의 키 출력

```javascript
function solution(...nums) {
    let arr = nums,
        sum = arr.reduce((a, b) => a + b);

    // 총합을 구하고 이중 포문을 돌려 arr 배열의 값(arr[i] + arr[j])을 더한다. 
    // 100의 합계가 맞으면 splice로 해당 index를 제거한다.
    // ⭐ 경우의 수는 이렇게 이중 포문으로 각각의 값을 구하여 더할 수 있다.
    // 항상 경우의 수를 더할 때 생각해봐야할 것 같다.

    for (let i = 0; i < 8; i++) {
        for (let j = i + 1; j < 9; j++) {
            if ((sum - (arr[i] + arr[j])) === 100) {
                arr.splice(j, 1);
                arr.splice(i, 1);
            }
        }
    }

    return arr;
}

solution(20, 7, 23, 19, 10, 15, 25, 8, 13);

// case
function solutionTwo(...nums) {
    let total = nums.reduce((a, b) => a + b),
        arr = nums;

    // 재귀함수를 통해 일곱 난쟁이의 키 출력하는 함수를 구현해보았다.
    // 이중 포문 말고도 다른 방법이 무엇이 있을까 찾아보다가 구현 해보았다. 
    function recursion(n = 0, s = n + 1) {
        if (n === 9) return;

        for (let i = s; i < 9; i++) {
            if ((total - (arr[n] + arr[i])) === 100) {
                if (n < i) {
                    arr.splice(i, 1);
                    arr.splice(n, 1);
                } else {
                    arr.splice(n, 1);
                    arr.splice(i, 1);
                }
            }
        }

        return recursion(++n, n + 1);
    }

    recursion();

    return arr;
}

solutionTwo(20, 7, 23, 19, 10, 15, 25, 8, 13);
```

## 9. A를 #으로

```javascript
// case 1 
function solution(str) {
    let string = [...str];

    for (let i = 0, len = string.length; i < len; i++) {
        if (string[i] === 'A') {
            string[i] = '#';
        }
    }

    return string.join('');
}

solution('BANANA');

// case 2
function solutionTwo(str) {
    let string = str;

    return string.replaceAll('A', '#');
}

solutionTwo('BANANA');

// case 3

function solutionThree(str) {
    let string = [...str];

    let s = string.map((ele, idx) => {
        return ele === 'A' ? '#' : ele;
    });

    return s.join('');
}

solutionThree('BANANA');
```

## 10. 문자 찾기

### 조건

- 한 개의 문자열 입력, 특정 문자를 입력 받아 해당 특정 문자가 입력받은 문자열에 몇개 존재하는지 알아내자

### 코드

- 해당 문자의 개수를 출력

```javascript
// case 1
function solution(character, string) {
    let char = character,
        re = new RegExp(`${char}`, 'g'),
        str = string.match(re);

    return str.length;
}

solution('R', 'COMPUTERPROGRAMMING');

// case 2 
function solutionTwo(character, string) {
    let char = character,
        str = string.split(''),
        strLenArr = str.filter(ele => {
            return ele === char;
        });

    return strLenArr.length;
}

solutionTwo('R', 'COMPUTERPROGRAMMING');
```

## 11.대문자 찾기

```javascript
function solution(string) {
    let str = string;

    return str.match(/[A-Z]/g).length;
}

solution('KoreaTimeGood');
```
