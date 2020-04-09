# 시저암호

어떤 문장의 각 알파벳을 일정한 거리만큼 밀어서 다른 알파벳으로 바꾸는 암호화 방식을 시저 암호라고 합니다. 예를 들어 AB는 1만큼 밀면 BC가 되고, 3만큼 밀면 DE가 됩니다. z는 1만큼 밀면 a가 됩니다. 문자열 s와 거리 n을 입력받아 s를 n만큼 민 암호문을 만드는 함수, solution을 완성해 보세요.<br/>
<br/>

**제한 조건**

- 공백은 아무리 밀어도 공백입니다.
- s는 알파벳 소문자, 대문자, 공백으로만 이루어져 있습니다.
- s의 길이는 8000이하입니다.
- n은 1 이상, 25이하인 자연수입니다.

**입출력 예**

| s | n | result |
|:---:|:---:|:---:|
| "AB" | 1 | "BC" |
| "z" | 1 | a |
| "a B z" | 4 | "e F d" |

## Problem-solving process

이 문제는 아스키코드에 대해서 알아야 풀 수 있는 문제이다.
왜냐하면, string을 숫자로 변환을 하고 주어진 n의 수만큼 이동을 하여 해당하는 수의 string을 다시 반환 해야하기 때문이다.<br/>
아스키코드에서 90이상은 소문자 영역이기 때문에, 이를 기준으로 하여 소문자 영역과 대문자 영역을 나눈 뒤 n을 더한 수에서 소문자인 경우 97('a'의 순번)을, 대문자인 경우 65('A'의 순번)를 빼준뒤 해당하는 수를 26으로 나눈 나머지를 구하면, 해당하는 알파벳의 순서를 알수 있고 이에 다시 아까 빼주었던 수(소문자인 경우 97('a'의 순번)을, 대문자인 경우 65('A'의 순번))를 더해주면 원하는 아스키 코드의 번호를 알 수있다.

if문으로 여러 조건절을 주는 것을 선호하지 않는 편이라, 최대한 삼항 연산자를 사용하려고 했다.

## Problem answer

```javascript
function solution(s, n) {
    return s.split("").reduce((final, value) => {
        const movedNumber = value.charCodeAt() > 90
            ? (value.charCodeAt() + n - 97)%26 + 97
            : (value.charCodeAt() + n - 65)%26 + 65;
        const fromCode = String.fromCharCode(movedNumber);
        return final += value === " " ? " " : fromCode;
    },'');
}
```
