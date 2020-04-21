# 가운데 글자 가져오기

단어 s의 가운데 글자를 반환하는 함수, solution을 만들어 보세요. 단어의 길이가 짝수라면 가운데 두글자를 반환하면 됩니다.<br/>
<br/>

**제한사항**

- s는 길이가 1 이상, 100이하인 스트링입니다.

**입출력 예**
| s | return |
|:---:|:---:|
| abcde | c |
| qwer | we |

## Problem-solving process

이전에 자바스크립트로 푼 문제를 파이썬으로 풀었다.<br/>
이번에는 조금더 파이썬에 있는 기능들로 구현하는데에 집중했으나 잘 되었는지는 모르겠다.<br/>
구현방법은, 주어진 string의 길이를 구해서 2로 나눴을 때의 나머지가 있는지 없는지에 따라서 분기를 태웠다.<br/>
자바스크립트는 이전에 풀었던 방법을 조금 고쳤다.

## Problem answer

```javascript
function solution(s) {
    // var answer = '';
    // var temp = s.split("");
    // var parse = parseInt(temp.length /2);
    // if (temp.length % 2 == 0) {
    //     answer = temp[parse-1] + temp[parse];
    // } else {
    //     answer = temp[parse];
    // }
    // return answer;
    const temp = s.split("");
    const parse = parseInt(temp.length / 2);
    return temp.length % 2 === 0 ? temp[parse - 1] + temp[parse] : temp[parse];
}
```

```python
def solution(s):
    return s[int(len(s) / 2 -1) : int(len(s) / 2 + 1)] if len(s) % 2 is 0 else s[int(len(s) / 2 ) : int(len(s) / 2 + 1)]
```