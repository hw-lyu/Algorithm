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
function solution(A,B,C) {
    let maxNum = Math.max(A,B,C),
        triangleArr = [A,B,C];
    
    let twoSides = triangleArr.reduce((acc, cur) => {
       return acc + cur
    });

    // 삼각형의 세 변의 길이를 합산해서 제일 긴 변의 길이를 뺀다. 
   twoSides -= maxNum;

   if(maxNum < twoSides) {
        return "yes";
    } else {
        return "no";
    }
}

solution(6,7,11);
```

## 3. 연필개수 

### 조건
- 연필  1 다스 = 12자루
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

### 4. 1부터 N까지 합 출력하기
- 1부터 N까지의 합을 출력한다.

```javascript
function solution(n) {
    let num = 0;
    for(let i = 1; i <= n; i++) {
        num+=i;
    }

    return num;
}

solution(6);
```

### 5. 최솟값 구하기 
- 가장 작은 값을 출력한다.

```javascript
function solution(...num) {
    let arr = num,
        minNum = 100;
    
    arr.forEach((ele) => {
        // 100을 기준으로 ele의 첫번째 값 5를 값에 대입하고 
        // 그 후로 3<5,7<3.. 이런식으로 값을 비교하고 최소값을 대입해준다. 
        if(ele < minNum) minNum = ele;
    });

    return minNum;
}

solution(5,3,7,11,2,15,17);
```
