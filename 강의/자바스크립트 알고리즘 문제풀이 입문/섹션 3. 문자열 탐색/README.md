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
