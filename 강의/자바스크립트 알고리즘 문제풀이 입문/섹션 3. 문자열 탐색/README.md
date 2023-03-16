# 문제풀이

## 1.회문문자열

```javascript
function solution(str) {
    let lowerStr = str.toLowerCase();

    // String.prototype.endsWith(searchString) - 어떤 문자열에서 특정 문자열로 끝나는지를 확인할 수 있는 메서드
    // searchString : 이 문자열의 끝이 특정 문자열로 끝나는지를 찾기 원하는 문자열
    return lowerStr.endsWith(lowerStr.split('')[0]) ? "YES" : "NO";
}

solution('goog'); //true
```
