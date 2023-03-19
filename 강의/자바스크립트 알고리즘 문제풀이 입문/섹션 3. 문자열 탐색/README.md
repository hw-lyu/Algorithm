# 문제풀이

## 1.회문문자열

- 회문 문자열 : 앞에서 읽을 때나 뒤에서 읽을 때나 같은 문자열
- 조건
    - 회문을 검사할 때 대소문자 구분하지 않는다.
- 반환값
    - 회문 문자열이면 :  “YES”
    - 회문 문자열이 아니면 : “NO”

```javascript
function solution(str) {
    let lowerStr = str.toLowerCase();

    // String.prototype.endsWith(searchString) - 어떤 문자열에서 특정 문자열로 끝나는지를 확인할 수 있는 메서드
    // searchString : 이 문자열의 끝이 특정 문자열로 끝나는지를 찾기 원하는 문자열
    return lowerStr.endsWith(lowerStr.charAt(0)) ? "YES" : "NO";
}

solution('gooG'); // "YES"
```

## 2.팰린드롬

- 팰린드롬 : 앞에서 읽을 때나 뒤에서 읽을 때나 같은 문자열
- 회문을 검사할 때 알파벳만 가지고 회문을 검사하며, 대소문자 구분하지 않는다.
- 알파벳 이외의 문자들은 무시합니다.
- 첫 번째 줄에 팰린드롬인지의 결과를 YES 또는 NO로 출력합니다.
- 반환 값
    - 해당 문자열이 팰린드롬이면 : “YES”
    - 아니면 : “NO”

```javascript
// case 1 
function solution(str) {
    let strRegExp = str.toLowerCase().match(/[a-z]+/g),
        strOriginalArr = strRegExp.slice(0, strRegExp.length / 2),
        strReverseArr = strRegExp.slice(strRegExp.length / 2).reverse();

    for (let i = 0, len = strReverseArr.length; i < len; i++) {
        let strReverse = strReverseArr[i].split('').reverse().join('');

        strReverseArr[i] = strReverse;
    }

    return strOriginalArr.join(' ') === strReverseArr.join(' ') ? "YES" : "NO";
}

solution('found7, time: study; Yduts; emit, 7Dnuof'); // YES

// case 2
function solutionTwo(str) {
    let strRegExp = str.toLowerCase().replace(/[^a-z]/g, '');

    if (strRegExp.split('').reverse().join('') !== strRegExp) {
        return "NO";
    }

    return "YES";
}

solutionTwo('found7, time: study; Yduts; emit, 7Dnuof'); // YES
```

### 3. 숫자만 추출

- 문자와 숫자가 섞여있는 문자열이 주어지면 그 중 숫자만 추출하여 그 순서대로 자연수를 만든다. <br>
  만약 “tae0a1h205er”에서 숫자만 추줄하면 0,1,2,0,5이고 이것을 자연수로 만들면 1205가 된다.
- 첫 줄에 자연수를 출력합니다.

```javascript
// case 1 
function solution(str) {
    let arr = str.split(''),
        numArr = arr.filter(ele => {
            return !isNaN(ele);
        });

    return parseInt(numArr.join(''));
}

solution('g0en2T0s8eSOft'); //208

// case 2
function solutionTwo(str) {
    return parseInt(str.match(/\d/g).join(''));
}

solutionTwo('g0en2T0s8eSOft'); //208
```

## 4. 문자거리

- 한 개의 문자열 s와 문자 t가 주어지면 문자열 s의 각 문자가 문자 t와 떨어진 최소거리를 출력하는 프로그램을 작성
- 반환 값
    - 첫번 째 줄에 각 문자열 s의 각 문자가 문자 t와 떨어진 거리를 순서대로 출력한다.

```javascript
function solution(str) {
    let arr = str.split(' '),
        standardStr = arr[1],
        strArr = arr[0].split(''),
        lenLeftArr = [],
        lenRightArr = [],
        num = 0;

    // 정방향과 반대방향을 비교하여 최소 거리를 구해준다. 
    strArr.map(ele => {
        if (ele === standardStr) {
            num = 0;
            lenLeftArr.push(num);
        } else {
            lenLeftArr.push(++num);
        }
    });


    strArr.reverse().map(ele => {
        if (ele === standardStr) {
            num = 0;
            lenRightArr.push(num);
        } else {
            lenRightArr.push(++num);
        }
    });

    // lenLeftArr를 기준으로 값을 비교해 최소 거리를 구한다. 
    lenRightArr.reverse().map((ele, idx) => {
        if (ele < lenLeftArr[idx]) {
            lenLeftArr[idx] = ele;
        }
    });

    return lenLeftArr.join(' ');
}

solution('teachermode e'); //'1 0 1 2 1 0 1 2 2 1 0'
```
