# 두 정수 사이의 합

두 정수 a, b가 주어졌을 때 a와 b 사이에 속한 모든 정수의 합을 리턴하는 함수, solution을 완성하세요.<br/>
예를 들어 a = 3, b = 5인 경우, 3 + 4 + 5 = 12이므로 12를 리턴합니다.<br/>
<br/>
**제한 조건**

- a와 b가 같은 경우는 둘 중 아무 수나 리턴하세요.
- a와 b는 -10,000,000 이상 10,000,000 이하인 정수입니다.
- a와 b의 대소관계는 정해져있지 않습니다.

**입출력 예**
| a | b | return |
|:---:|:---:|:---:|
| 3 | 5 | 12 |
| 3 | 3 | 3 |
| 5 | 3 | 12 |

## Problem-solving process

해당 문제도 이전에 자바스크립트로 푼 문제를 파이썬에 익숙해지기 위해서 다시 푼 문제이다.<br/>
간단하게, 주어진 두 수중 어떤 것이 큰 수이고, 작은 수인지 확인한 뒤, 작은 수 에서부터 큰 수까지 루프를 돌면서 합계를 구하면 된다.

## Problem answer

```javascript
function solution(a, b) {
    // 옛날에 푼 방법
    // var answer = 0;
    // var array  = [a , b].sort((a,b) => a-b);
    // if(array[0] == array[1]) {
    //     return array[0];
    // }else {
    //     let i = array[0];
    //     while( i <= array[1]) {
    //         answer += i;
    //         i++;
    //     }
    //     return answer;
    // }

    let answer = 0

    for (let i = Math.min(a,b); i <= Math.max(a,b); i++) {
        answer += i
    }

    return answer;
}
```

```python
def solution(a, b):
    answer = 0
    max_number = max(a, b)
    min_number = min(a, b)

    for n in range(min_number, max_number + 1):
        answer += n
    return answer
```

초창기에 푼 문제다 보니, javascript 풀 때 var를 쓴게 조금 충격이었다. 일단 급한대로 수정을 했지만, for문 안의 조건에 Math를 너무 호출하는 것 같아서 좀 더 개선할 수 있는 방법을 찾아봐야겠다. 파이썬은 이번에 푼 해법인데, 이 해답을 제출 한 후 다른 사람 풀이중에, sum()을 쓴 것이 있어서 좀 반성이 되었다. javascript에는 없다보니 약간 javascript 스럽게 python을 쓰고 있는 것 같아서 좀 더 파이썬 답게 코딩하는 방법에 대해 고민하고 공부해 봐야겠다는 생각이 들었다.