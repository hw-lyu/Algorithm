# 릿코드
- 릿코드 문제를 풀고 올립니다. 

## 13 . 로마에서 정수로

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var romanToInt = function(s) {
        let arr = s.split(''), 
        obj = {
            I : 1,
            V : 5,
            X : 10,
            L : 50,
            C : 100,
            D : 500,
            M : 1000
        },
        count = 0; 

    for(let i = 0, len = arr.length; i < len; i++) {
        for(const num in obj) {
            if(arr[i] === num) {
                let nowNextStr = `${arr[i] + arr[i+1]}`;

                count += obj[num];

                // 예외값
                if(nowNextStr === 'IV') {
                    count -= 2;
                }
                if(nowNextStr === 'XL') {
                    count -= 20;
                }
                if(nowNextStr === 'CD') {
                    count -= 200;
                }
                if(nowNextStr === 'IX') {
                    count -= 2;
                }
                if(nowNextStr === 'XC') {
                    count -= 20;
                }
                if(nowNextStr === 'CM') {
                    count -= 200;
                }
            }
        }
    }
    
    return count; 
};
```
