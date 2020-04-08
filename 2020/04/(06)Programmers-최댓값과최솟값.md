# 최댓값과 최솟값

문자열 s에는 공백으로 구분된 숫자들이 저장되어 있습니다. str에 나타나는 숫자 중 최소값과 최대값을 찾아 이를 (최소값) (최대값)형태의 문자열을 반환하는 함수, solution을 완성하세요.<br/>
예를들어 s가 1 2 3 4라면 1 4를 리턴하고, -1 -2 -3 -4라면 -4 -1을 리턴하면 됩니다.<br/>
<br/>
**제한 조건**
- s에는 둘 이상의 정수가 공백으로 구분되어 있습니다.

입출력 예
| s | return|
|:---:|:---:|
| "1 2 3 4" | "1 4" |
| "-1 -2 -3 -4" | "-4 -1" |
| "-1 -1" | "-1 -1" |

## Problem-solving process

input으로 들어온 숫자로 된 string을 공백으로 쪼갠뒤, map을 이용해서 각 배열의 string 숫자를 number 형식으로 변환 시켜주고 sort를 해준뒤 답에 맞춰서 최솟값 최댓값으로 이루어진 string을 반환하도록 하면 된다.

## Problem answer

```javascript
function solution(s) {
    const answer = s.split(" ").map(n => +n).sort((a,b) => a - b);
    return `${answer[0]} ${answer[answer.length - 1]}`
}
```