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

solution('gooG'); //true
```
