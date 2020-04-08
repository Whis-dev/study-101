# N개의 최소공배수

두 수의 최소공배수(Least Common Multiple)란 입력된 두 수의 배수 중 공통이 되는 가장 작은 숫자를 의미합니다. 예를 들어 2와 7의 최소공배수는 14가 됩니다. 정의를 확장해서, n개의 수의 최소공배수는 n 개의 수들의 배수 중 공통이 되는 가장 작은 숫자가 됩니다. n개의 숫자를 담은 배열 arr이 입력되었을 때 이 수들의 최소공배수를 반환하는 함수, solution을 완성해 주세요.<br/>

**제한 사항**

- arr은 길이 1이상, 15이하인 배열입니다.
- arr의 원소는 100 이하인 자연수입니다.

**입출력 예**
| arr | result |
|:---:|:---:|
| [2,6,8,14] | 168 |
| [1,2,3] | 6 |

## Problem-solving process

배열을 돌면서, 이전 수와 다음 수의 최대공약수를 구하고, 그것을 이용하여 최소공배수를 구한 뒤, 만들어진 최소공배수와 그 다음 배열의 수를 비교하고, 최대공약수와 최소공배수를 구하는 로직을 반복하면, 최종적으로 주어진 배열의 원소들 전체의 최소공배수를 구할 수 있다.<br/>
<br/>
최대공약수와, 최소공배수를 구한 로직은 이전과 같으며, 이를 조금 수정하여 문제를 풀었다.

## Problem answer

```javascript
function greatestCommonFactor (a,b) {
    const max = Math.max(a,b);
    const min = Math.min(a,b);
    const remains = max % min;

    return remains === 0 ? min : greatestCommonFactor(min, remains);
}

function solution(arr) {
    return arr.reduce((final, value, index) => {
        let gcf = greatestCommonFactor(final, value);
        return ( final * value) / gcf
    }, 1)
}
```